# Demo Script

## Let's make a single request to the MCP Server
```sh
# Fire a single call to the flaky server and inspect the response body
curl -si -X POST http://localhost:9000/mcp-stable \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call",
       "params":{"name":"query_db","arguments":{}}}'
```


```sh
# Terminal A: what NGINX's access log sees (HTTP layer)
docker compose logs -f nginx | grep -E "POST|status"

# Terminal B: what the mcp-client itself reports (MCP layer)  
docker compose logs -f mcp-client | grep Errors
```

query the demo's actual data with a curl while it's running:
```sh
# Fire a single call to the flaky server and inspect the response body
curl -si -X POST http://localhost:9000/mcp-flaky \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call",
       "params":{"name":"query_db","arguments":{}}}'

# Run it 20 times. About 1 in 10 responses will come back like:
HTTP/1.1 200 OK              ← NGINX is happy
Content-Type: text/event-stream

event: message
data: {"jsonrpc":"2.0","id":1,"result":{
  "content":[{"type":"text","text":"database timeout"}],
  "isError":true             ← the actual failure, buried
}}
```
## Let's make one complete MCP session from cURL
Here's the full sequence. I'll walk you through each step, what to expect, and why each part exists. We'll use `mcp-stable` because it's the one that won't randomly fail on you.

### Step 1 — Initialize the session

This is the handshake. You're introducing yourself as a client and getting a session ID back.

```bash
curl -si -X POST http://localhost:9000/mcp-stable \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "initialize",
    "params": {
      "protocolVersion": "2025-03-26",
      "capabilities": {},
      "clientInfo": {
        "name": "curl-human",
        "version": "1.0.0"
      }
    }
  }'
```

**What you'll see back:**
```
HTTP/1.1 200 OK
Mcp-Session-Id: <some-uuid-string>
Content-Type: text/event-stream
...

event: message
data: {"jsonrpc":"2.0","id":1,"result":{"protocolVersion":"2025-03-26",
       "capabilities":{"tools":{}},
       "serverInfo":{"name":"mcp-stable","version":"..."}}}
```

**Copy that `Mcp-Session-Id` value** — you'll paste it into every subsequent request. Let's call it `$SID` from here on. You can also do it in one shot:

```bash
SID=$(curl -s -D - -o /tmp/init.txt -X POST http://localhost:9000/mcp-stable \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"curl-human","version":"1.0"}}}' \
  | grep -i '^mcp-session-id:' | awk '{print $2}' | tr -d '\r\n')

echo "Session ID: $SID"
cat /tmp/init.txt
```

**What just happened behind the scenes:** the server allocated a session, and `mcp.js`'s `mcp_header_filter` captured `clientInfo.name = "curl-human"` and stored it in the `mcp_clients` shared dict under this session ID. The `mcp_response_filter` then read the response body, extracted `serverInfo.name = "mcp-stable"`, and stored it in `mcp_servers` under the same key. Your identity is now known to NGINX for the duration of this session.

### Step 2 — Send the `initialized` notification

The spec requires this. It's how the client says "handshake complete, I'm ready." Notifications don't have an `id` field and don't get a response body — just a `202 Accepted`.

```bash
curl -si -X POST http://localhost:9000/mcp-stable \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -H "Mcp-Session-Id: $SID" \
  -d '{
    "jsonrpc": "2.0",
    "method": "notifications/initialized"
  }'
```

**Expect:**
```
HTTP/1.1 202 Accepted
Content-Length: 0
```

If you skip this step, some servers will reject subsequent calls with "session not initialized." The `mcp-stable` demo server almost certainly enforces this — you saw it earlier when your first curl got `"method \"tools/call\" is invalid during session initialization"`.

### Step 3 — Discover what tools exist

Now you can start doing real work. First, ask the server what it offers:

```bash
curl -si -X POST http://localhost:9000/mcp-stable \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -H "Mcp-Session-Id: $SID" \
  -d '{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "tools/list"
  }'
```

**Expect** an SSE response with a list of tool descriptors — something like:

```
data: {"jsonrpc":"2.0","id":2,"result":{"tools":[
  {"name":"get_forecast","description":"...","inputSchema":{...}},
  {"name":"get_stock_price","description":"...","inputSchema":{...}},
  {"name":"search_web",...},
  ...
]}}
```

This is where a real agent would learn what it can invoke. For your purposes it also confirms the demo's 8-tool catalog.

### Step 4 — Call a tool

Pick one from the list and invoke it. `get_forecast` is safe:

```bash
curl -si -X POST http://localhost:9000/mcp-stable \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -H "Mcp-Session-Id: $SID" \
  -d '{
    "jsonrpc": "2.0",
    "id": 3,
    "method": "tools/call",
    "params": {
      "name": "get_forecast",
      "arguments": {
        "city": "Tokyo"
      }
    }
  }'
```

**Expect:**
```
HTTP/1.1 200 OK
Content-Type: text/event-stream

event: message
data: {"jsonrpc":"2.0","id":3,"result":{
  "content":[{"type":"text","text":"..."}],
  "isError":false
}}
```

**This is the interesting request from `mcp.js`'s perspective.** All four span attributes get populated for this one call:

- `mcp.tool.name = "get_forecast"` — read from the request body by `mcp_tool_name()`.
- `mcp.tool.status = "ok"` — because `has_error()` looks at the response body's first message and finds no `error` and `isError` is not true.
- `mcp.client.name = "curl-human"` — looked up from the shared dict by session ID.
- `mcp.server.name = "mcp-stable"` — likewise.

If you refresh Grafana around now, you should be able to filter on `mcp_client_name="curl-human"` and see your one lonely call sitting there among all the load generator traffic.

### Step 5 — Call a few more, for good measure

Fire off a couple more with different tools to make yourself easier to spot in the dashboard:

```bash
# Repeat a few times with different tools/arguments
for tool in get_stock_price search_web calculate_sum; do
  curl -s -o /dev/null -w "$tool: HTTP %{http_code}\n" \
    -X POST http://localhost:9000/mcp-stable \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d "{\"jsonrpc\":\"2.0\",\"id\":4,\"method\":\"tools/call\",
         \"params\":{\"name\":\"$tool\",\"arguments\":{}}}"
done
```

### Step 6 — (Optional) Close the session

MCP defines an explicit termination with an HTTP DELETE on the endpoint carrying the session ID:

```bash
curl -si -X DELETE http://localhost:9000/mcp-stable \
  -H "Mcp-Session-Id: $SID"
```

Not all servers enforce or even implement this; the demo may just let sessions expire. But it's the spec-compliant way to say goodbye.

### Bonus — try it against `mcp-flaky` to see the failure modes

Now that you know the full dance, repeat steps 1–4 against `/mcp-flaky` instead of `/mcp-stable`. About one in ten `tools/call` requests will come back with:

```
event: message
data: {"jsonrpc":"2.0","id":3,"result":{
  "content":[{"type":"text","text":"..."}],
  "isError":true                              ← this is the killer
}}
```

The HTTP status: **200**. The body: tool-level failure. Exactly the case `mcp.js` catches that a plain access log cannot.

And roughly 2% of the time you'll get the other failure mode — the JSON-RPC `error` object at the top level:

```
data: {"jsonrpc":"2.0","id":3,"error":{"code":-32603,"message":"..."}}
```

Also HTTP 200. Also invisible to NGINX at the transport layer. Also caught by `has_error()`'s first check.

### One-command wrapper if you want to loop it

Once you've got the flow working manually, here's a script version that does a full session end-to-end and can be run repeatedly:

```bash
mcp_session() {
  local BACKEND=$1
  local TOOL=${2:-get_forecast}

  # Init
  local SID=$(curl -s -D - -o /dev/null -X POST http://localhost:9000/$BACKEND \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-03-26","capabilities":{},"clientInfo":{"name":"curl-human","version":"1.0"}}}' \
    | grep -i '^mcp-session-id:' | awk '{print $2}' | tr -d '\r\n')

  [ -z "$SID" ] && { echo "no session"; return 1; }

  # Initialized notification
  curl -s -o /dev/null -X POST http://localhost:9000/$BACKEND \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d '{"jsonrpc":"2.0","method":"notifications/initialized"}'

  # Tool call
  curl -s -X POST http://localhost:9000/$BACKEND \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d "{\"jsonrpc\":\"2.0\",\"id\":2,\"method\":\"tools/call\",\"params\":{\"name\":\"$TOOL\",\"arguments\":{}}}"
  echo
}

# Usage:
mcp_session mcp-stable get_forecast
mcp_session mcp-flaky  query_db
```

That's the whole MCP lifecycle: **initialize → initialized → (optional discover) → invoke → (optional close)**. Try Step 1 first, confirm you got a session ID back, and let me know if anything comes back looking different from what I described — that would be interesting to dig into.

# Send 50 requests to flaky mcp server
Flaky server is with 2% protocol + 10% tool error rates
```sh
for i in {1..50}; do
  # Step 1: initialize a session, capture the Mcp-Session-Id header
  SID=$(curl -s -D - -o /dev/null -X POST http://localhost:9000/mcp-flaky \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -d '{"jsonrpc":"2.0","id":1,"method":"initialize",
         "params":{"protocolVersion":"2025-03-26","capabilities":{},
                   "clientInfo":{"name":"curl-test","version":"1.0"}}}' \
    | grep -i '^mcp-session-id:' | awk '{print $2}' | tr -d '\r\n')

  if [ -z "$SID" ]; then
    echo "attempt $i: no session id returned, skipping"
    continue
  fi

  # Step 2: send the initialized notification (MCP requires this)
  curl -s -o /dev/null -X POST http://localhost:9000/mcp-flaky \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d '{"jsonrpc":"2.0","method":"notifications/initialized"}'

  # Step 3: the actual tool call using the real session id
  RESP=$(curl -s -w "|HTTP:%{http_code}" -X POST http://localhost:9000/mcp-flaky \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d '{"jsonrpc":"2.0","id":2,"method":"tools/call",
         "params":{"name":"query_db","arguments":{}}}')

  HTTP=$(echo "$RESP" | grep -oE 'HTTP:[0-9]+' | cut -d: -f2)
  MCP="ok"
  if echo "$RESP" | grep -q '"isError":true'; then MCP="TOOL_ERR"; fi
  if echo "$RESP" | grep -q '"error":{'; then MCP="PROTO_ERR"; fi
  echo "http=$HTTP  mcp=$MCP"
done | sort | uniq -c
```
## Lets do the same to the stable server
```sh
for i in {1..50}; do
  # Step 1: initialize a session, capture the Mcp-Session-Id header
  SID=$(curl -s -D - -o /dev/null -X POST http://localhost:9000/mcp-stable \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -d '{"jsonrpc":"2.0","id":1,"method":"initialize",
         "params":{"protocolVersion":"2025-03-26","capabilities":{},
                   "clientInfo":{"name":"curl-test","version":"1.0"}}}' \
    | grep -i '^mcp-session-id:' | awk '{print $2}' | tr -d '\r\n')

  if [ -z "$SID" ]; then
    echo "attempt $i: no session id returned, skipping"
    continue
  fi

  # Step 2: send the initialized notification (MCP requires this)
  curl -s -o /dev/null -X POST http://localhost:9000/mcp-stable \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d '{"jsonrpc":"2.0","method":"notifications/initialized"}'

  # Step 3: the actual tool call using the real session id
  RESP=$(curl -s -w "|HTTP:%{http_code}" -X POST http://localhost:9000/mcp-stable \
    -H "Content-Type: application/json" \
    -H "Accept: application/json, text/event-stream" \
    -H "Mcp-Session-Id: $SID" \
    -d '{"jsonrpc":"2.0","id":2,"method":"tools/call",
         "params":{"name":"query_db","arguments":{}}}')

  HTTP=$(echo "$RESP" | grep -oE 'HTTP:[0-9]+' | cut -d: -f2)
  MCP="ok"
  if echo "$RESP" | grep -q '"isError":true'; then MCP="TOOL_ERR"; fi
  if echo "$RESP" | grep -q '"error":{'; then MCP="PROTO_ERR"; fi
  echo "http=$HTTP  mcp=$MCP"
done | sort | uniq -c
```


## Extra

3. Making "HTTP 200 hides tool errors" tangible
This is the money shot of the whole project and yes — you can make it viscerally visible. Two ways, one quick and one thorough.
The quick way — docker logs diff. With the demo running, open two terminals side by side and compare what each layer sees:
bash
### Terminal A: what NGINX's access log sees (HTTP layer)
docker compose logs -f nginx | grep -E "POST|status"

### Terminal B: what the mcp-client itself reports (MCP layer)  
docker compose logs -f mcp-client | grep Errors
Terminal A will show a firehose of 200 OK responses. Terminal B will show Errors: (0/55/0/0) climbing. Same requests. Two completely different accounts of what happened.
To make this even sharper, you can query the demo's actual data with a curl while it's running:
bash# Fire a single call to the flaky server and inspect the response body
curl -si -X POST http://localhost:9000/mcp-flaky \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call",
       "params":{"name":"query_db","arguments":{}}}'
Run it 20 times. About 1 in 10 responses will come back like:
HTTP/1.1 200 OK              ← NGINX is happy
Content-Type: text/event-stream

event: message
data: {"jsonrpc":"2.0","id":1,"result":{
  "content":[{"type":"text","text":"database timeout"}],
  "isError":true             ← the actual failure, buried
}}
The HTTP status is 200. The tool failed. No amount of standard HTTP monitoring will ever catch this. That's the point of mcp.js reading the body.
The thorough way — a side-by-side Grafana panel. In Grafana, create one panel that queries the raw NGINX HTTP status metric (nginx_http_requests_total{status="5xx"}) and one that queries the mcp.js-derived metric (traces_spanmetrics_calls_total{mcp_tool_status="error"}). Put them next to each other. The first stays at zero forever. The second climbs steadily on flaky traffic. That's the visual proof that observability at the transport layer is blind and observability at the payload layer sees the truth. If I were pitching this internally, this is the single screenshot I'd use.

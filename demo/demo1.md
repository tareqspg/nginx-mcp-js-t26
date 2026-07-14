# Demo Script



```sh
# Terminal A: what NGINX's access log sees (HTTP layer)
docker compose logs -f nginx | grep -E "POST|status"

# Terminal B: what the mcp-client itself reports (MCP layer)  
docker compose logs -f mcp-client | grep Errors
```





3. Making "HTTP 200 hides tool errors" tangible
This is the money shot of the whole project and yes — you can make it viscerally visible. Two ways, one quick and one thorough.
The quick way — docker logs diff. With the demo running, open two terminals side by side and compare what each layer sees:
bash
# Terminal A: what NGINX's access log sees (HTTP layer)
docker compose logs -f nginx | grep -E "POST|status"

# Terminal B: what the mcp-client itself reports (MCP layer)  
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

# mcp.js
Thank you for adding that! Having the actual `mcp.js` code reveals exactly how NGINX handles the parsing under the hood, and it corrects some general assumptions about how the metadata is extracted. 

Now that we can see the code, we can observe that NGINX is doing something much smarter and more efficient than just brute-force parsing every single JSON response. Here is exactly how the `njs` script handles the traffic:

**1. Tool Name Extraction (Parsing the Request, Not the Response)**
To find out which tool the AI is calling, NGINX does not wait for the server's response. Instead, it inspects the incoming client request payload using `JSON.parse(r.requestText || '{}')`. It checks if the JSON-RPC `method` is set to `tools/call`; if it is, it instantly extracts the tool name from `body.params.name`. 

**2. Client and Server Identities (Using Headers and Shared Memory)**
Brilliantly, the code does not parse the JSON payload for identities. Instead, it looks at the HTTP headers for an `Mcp-Session-Id` (`r.headersIn['Mcp-Session-Id']`). It then takes this ID and does a lightning-fast lookup against NGINX's built-in shared memory zones (`ngx.shared.mcp_clients` and `ngx.shared.mcp_servers`) to match the session ID with the exact client and server names. This avoids heavy JSON processing for every single request.

**3. Handling the SSE Stream and Responses**
For the responses coming back from the server, the script uses an `mcp_response_filter`. As data streams back, it buffers the chunks of data (`_mcp_buffer += data`) and simultaneously passes them along to the client (`r.sendBuffer(data, flags)`). 
To parse the Server-Sent Events (SSE) specifically, it uses a function called `parse_sse_first_json` which takes that buffered stream and splits it by `\n\n`—the standard delimiter used to separate blocks of SSE messages. 

**4. Tracking Error Statuses**
The script utilizes an internal `has_error(r)` function that evaluates the parsed messages (checking if `_mcp_messages.length === 0`). The `mcp_tool_status(r)` function relies on this evaluation to return an `'error'` string if the backend AI application failed to execute the tool. 

**5. Header Manipulation for Streaming**
Because the script intercepts and inspects streaming SSE responses, it includes an `mcp_header_filter` function that explicitly deletes the `Content-Length` header (`delete r.headersOut['Content-Length'];`). This is a critical requirement when a proxy deals with chunked or streaming data, as the final length isn't known upfront.

**Why this is great for your tech talk:**
You can actually use this to highlight NGINX's efficiency! You can tell the audience: *"NGINX isn't just doing heavy, brute-force JSON parsing on every byte. It smartly extracts the tool name from the request payload, manages the streaming SSE chunks by splitting the `\n\n` delimiters, and tracks client identity instantly using HTTP session headers and native NGINX shared memory."*

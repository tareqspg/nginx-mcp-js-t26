# startup log
```sh
ubuntu@ip-10-1-1-4:~/nginx-mcp-js/demo$ docker compose up --build
[+] Building 2.0s (25/25) FINISHED                                                                                                                                                                                                                                                                                     
 => [internal] load local bake definitions                                                                                                                                                                                                                                                                        0.0s
 => => reading from stdin 1.86kB                                                                                                                                                                                                                                                                                  0.0s
 => [mcp-stable internal] load build definition from Dockerfile                                                                                                                                                                                                                                                   0.0s
 => => transferring dockerfile: 577B                                                                                                                                                                                                                                                                              0.0s
 => [mcp-sluggish internal] load metadata for docker.io/library/alpine:latest                                                                                                                                                                                                                                     0.3s
 => [mcp-stable internal] load metadata for docker.io/library/golang:1.25-alpine                                                                                                                                                                                                                                  0.3s
 => [mcp-stable internal] load .dockerignore                                                                                                                                                                                                                                                                      0.0s
 => => transferring context: 2B                                                                                                                                                                                                                                                                                   0.0s
 => [mcp-sluggish builder 1/8] FROM docker.io/library/golang:1.25-alpine@sha256:56961d79ea8129efddcc0b8643fd8a5416b4e6228cfd477e3fd61deb2672c587                                                                                                                                                                  0.1s
 => => resolve docker.io/library/golang:1.25-alpine@sha256:56961d79ea8129efddcc0b8643fd8a5416b4e6228cfd477e3fd61deb2672c587                                                                                                                                                                                       0.1s
 => [mcp-stable stage-1 1/3] FROM docker.io/library/alpine:latest@sha256:28bd5fe8b56d1bd048e5babf5b10710ebe0bae67db86916198a6eec434943f8b                                                                                                                                                                         0.1s
 => => resolve docker.io/library/alpine:latest@sha256:28bd5fe8b56d1bd048e5babf5b10710ebe0bae67db86916198a6eec434943f8b                                                                                                                                                                                            0.1s
 => [mcp-sluggish internal] load build context                                                                                                                                                                                                                                                                    0.1s
 => => transferring context: 16.16kB                                                                                                                                                                                                                                                                              0.1s
 => CACHED [mcp-stable builder 2/8] RUN apk add --no-cache git                                                                                                                                                                                                                                                    0.0s
 => CACHED [mcp-stable builder 3/8] WORKDIR /build                                                                                                                                                                                                                                                                0.0s
 => CACHED [mcp-stable builder 4/8] COPY go.mod go.sum ./                                                                                                                                                                                                                                                         0.0s
 => CACHED [mcp-stable builder 5/8] COPY mcp_server.go mcp_client.go ./                                                                                                                                                                                                                                           0.0s
 => CACHED [mcp-stable builder 6/8] COPY go-sdk/ ./go-sdk/                                                                                                                                                                                                                                                        0.0s
 => CACHED [mcp-stable builder 7/8] RUN go mod tidy                                                                                                                                                                                                                                                               0.0s
 => CACHED [mcp-stable builder 8/8] RUN CGO_ENABLED=0 go build -o mcp_server mcp_server.go  && CGO_ENABLED=0 go build -o mcp_client mcp_client.go                                                                                                                                                                 0.0s
 => CACHED [mcp-stable stage-1 2/3] COPY --from=builder /build/mcp_server /mcp_server                                                                                                                                                                                                                             0.0s
 => CACHED [mcp-client stage-1 3/3] COPY --from=builder /build/mcp_client /mcp_client                                                                                                                                                                                                                             0.0s
 => [mcp-client] exporting to image                                                                                                                                                                                                                                                                               0.5s
 => => exporting layers                                                                                                                                                                                                                                                                                           0.0s
 => => exporting manifest sha256:7eaf5503b04ae963b60eaa0a118e81331f959ec7291580ce2d76c1c8dd1ae0e7                                                                                                                                                                                                                 0.0s
 => => exporting config sha256:2c225530b5d561e768c51fa45061b97b20bbf30fed7e0ef98724176044212c37                                                                                                                                                                                                                   0.0s
 => => exporting attestation manifest sha256:be14087c5f20b3648d50cbae14ca3fada5d51d50bd3d1c3a7a1999d77203fc96                                                                                                                                                                                                     0.2s
 => => exporting manifest list sha256:bbb28322740d190f87e9ad39c55241db59a30f12b7315a371fa9d15ad03f1b88                                                                                                                                                                                                            0.1s
 => => naming to docker.io/library/demo-mcp-client:latest                                                                                                                                                                                                                                                         0.0s
 => => unpacking to docker.io/library/demo-mcp-client:latest                                                                                                                                                                                                                                                      0.0s
 => [mcp-stable] exporting to image                                                                                                                                                                                                                                                                               0.5s
 => => exporting layers                                                                                                                                                                                                                                                                                           0.0s
 => => exporting manifest sha256:8489ed5712ade4decbfe3aaac80f0ea4f23ac281c0c437d816ce2a540793587d                                                                                                                                                                                                                 0.0s
 => => exporting config sha256:a0436082f32d0ee75e2ec7e1b9fadda3c3c24854ab23328369aa88f845ac8d74                                                                                                                                                                                                                   0.0s
 => => exporting attestation manifest sha256:f631eee947500feee4decc75f32e57cb0069bcfa7e8a193b936e5e2b38544c24                                                                                                                                                                                                     0.1s
 => => exporting manifest list sha256:dc94669442333ba1f012477c0337d9327ff1b9ab5b9a4b74ae84ec84f1d3a026                                                                                                                                                                                                            0.1s
 => => naming to docker.io/library/demo-mcp-stable:latest                                                                                                                                                                                                                                                         0.0s
 => => unpacking to docker.io/library/demo-mcp-stable:latest                                                                                                                                                                                                                                                      0.0s
 => [mcp-sluggish] exporting to image                                                                                                                                                                                                                                                                             0.6s
 => => exporting layers                                                                                                                                                                                                                                                                                           0.0s
 => => exporting manifest sha256:cce6c2f7559052abf308087b881f109ade45a0c950fc583ed5fc4dad895bde6f                                                                                                                                                                                                                 0.0s
 => => exporting config sha256:8521dda5988e3de28b71347fe3cd7737eb51a74f3fb9609eed510254c7f464d7                                                                                                                                                                                                                   0.0s
 => => exporting attestation manifest sha256:ae3c0a4ca2f4f1a5cfd353820010bd23a1780ba601366e0d9cf189d2fd8adf7c                                                                                                                                                                                                     0.2s
 => => exporting manifest list sha256:7a0e38ccfe60ef33dd7f68c7d981beff74422f9d997ac4d8969de68b54c39db8                                                                                                                                                                                                            0.1s
 => => naming to docker.io/library/demo-mcp-sluggish:latest                                                                                                                                                                                                                                                       0.0s
 => => unpacking to docker.io/library/demo-mcp-sluggish:latest                                                                                                                                                                                                                                                    0.0s
 => [mcp-flaky] exporting to image                                                                                                                                                                                                                                                                                0.6s
 => => exporting layers                                                                                                                                                                                                                                                                                           0.0s
 => => exporting manifest sha256:47dee1d042ed0c87afdb5d4a9f77d78dea3855f429375bd16d85cb8ae604948a                                                                                                                                                                                                                 0.0s
 => => exporting config sha256:423dbc3fb13ffcee6aef13601a3ccb424fee84131059c73e2bcbe0b1d4f93d42                                                                                                                                                                                                                   0.0s
 => => exporting attestation manifest sha256:4ff52bfae8d81636e7d8c3487bb0ce5729f594df9551aed84434ca1fcdabc7c9                                                                                                                                                                                                     0.2s
 => => exporting manifest list sha256:6961139b5987c759f02205fd3b2d4919fce02b96742978d23fc7185ad732824d                                                                                                                                                                                                            0.1s
 => => naming to docker.io/library/demo-mcp-flaky:latest                                                                                                                                                                                                                                                          0.0s
 => => unpacking to docker.io/library/demo-mcp-flaky:latest                                                                                                                                                                                                                                                       0.1s
 => [mcp-stable] resolving provenance for metadata file                                                                                                                                                                                                                                                           0.2s
 => [mcp-client] resolving provenance for metadata file                                                                                                                                                                                                                                                           0.2s
 => [mcp-sluggish] resolving provenance for metadata file                                                                                                                                                                                                                                                         0.1s
 => [mcp-flaky] resolving provenance for metadata file                                                                                                                                                                                                                                                            0.0s
[+] up 8/8
 ✔ Image demo-mcp-stable         Built                                                                                                                                                                                                                                                                             2.1s
 ✔ Image demo-mcp-flaky          Built                                                                                                                                                                                                                                                                             2.1s
 ✔ Image demo-mcp-sluggish       Built                                                                                                                                                                                                                                                                             2.1s
 ✔ Image demo-mcp-client         Built                                                                                                                                                                                                                                                                             2.1s
 ✔ Container demo-mcp-stable-1   Recreated                                                                                                                                                                                                                                                                         0.4s
 ✔ Container demo-mcp-flaky-1    Recreated                                                                                                                                                                                                                                                                         0.4s
 ✔ Container demo-mcp-sluggish-1 Recreated                                                                                                                                                                                                                                                                         0.3s
 ✔ Container demo-mcp-client-1   Recreated                                                                                                                                                                                                                                                                         0.3s
Attaching to grafana-1, mcp-client-1, mcp-flaky-1, mcp-sluggish-1, mcp-stable-1, nginx-1, otel-collector-1, prometheus-1
mcp-sluggish-1  | Starting MCP Mock Server 'mcp-sluggish' on :9003
mcp-sluggish-1  |   Protocol Error Rate: 0.00
mcp-sluggish-1  |   Tool Error Rate: 0.00
mcp-sluggish-1  |   Long Response Rate: 0.10
mcp-stable-1    | Starting MCP Mock Server 'mcp-stable' on :9001
mcp-stable-1    |   Protocol Error Rate: 0.00
mcp-stable-1    |   Tool Error Rate: 0.00
mcp-stable-1    |   Long Response Rate: 0.00
mcp-flaky-1     | Starting MCP Mock Server 'mcp-flaky' on :9002
mcp-flaky-1     |   Protocol Error Rate: 0.02
mcp-flaky-1     |   Tool Error Rate: 0.10
mcp-flaky-1     |   Long Response Rate: 0.00
prometheus-1    | time=2026-07-14T09:25:04.064Z level=INFO source=main.go:1589 msg="updated GOGC" old=100 new=75
prometheus-1    | time=2026-07-14T09:25:04.106Z level=INFO source=main.go:704 msg="Leaving GOMAXPROCS=2: CPU quota undefined" component=automaxprocs
prometheus-1    | time=2026-07-14T09:25:04.106Z level=INFO source=memlimit.go:198 msg="GOMEMLIMIT is updated" component=automemlimit package=github.com/KimMachineGun/automemlimit/memlimit GOMEMLIMIT=3657417523 previous=9223372036854775807
prometheus-1    | time=2026-07-14T09:25:04.106Z level=INFO source=main.go:752 msg="No time or size retention was set so using the default time retention" duration=15d
prometheus-1    | time=2026-07-14T09:25:04.106Z level=INFO source=main.go:803 msg="Starting Prometheus Server" mode=server version="(version=3.9.1, branch=HEAD, revision=9ec59baffb547e24f1468a53eb82901e58feabd8)"
prometheus-1    | time=2026-07-14T09:25:04.106Z level=INFO source=main.go:808 msg="operational information" build_context="(go=go1.25.5, platform=linux/amd64, user=root@61c3a9212c9e, date=20260107-16:08:09, tags=netgo,builtinassets)" host_details="(Linux 5.19.0-1026-aws #27~22.04.1-Ubuntu SMP Mon May 22 15:57:16 UTC 2023 x86_64 28b6bae5e8d5 (none))" fd_limits="(soft=524287, hard=524288)" vm_limits="(soft=unlimited, hard=unlimited)"
prometheus-1    | time=2026-07-14T09:25:04.123Z level=INFO source=web.go:684 msg="Start listening for connections" component=web address=0.0.0.0:9090
prometheus-1    | time=2026-07-14T09:25:04.124Z level=INFO source=main.go:1331 msg="Starting TSDB ..."
prometheus-1    | time=2026-07-14T09:25:04.124Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782097906354 maxt=1782100800000 ulid=01KVSNZJ7HCNNCGF7A8TWMACD1
prometheus-1    | time=2026-07-14T09:25:04.125Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782196001355 maxt=1782259200000 ulid=01KW3JVG4Y1YMC7V96BH8BRWT6
prometheus-1    | time=2026-07-14T09:25:04.125Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782259200000 maxt=1782273600000 ulid=01KW3Y1RT4QRA9HA7PWWV4NHCH
prometheus-1    | time=2026-07-14T09:25:04.125Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782540001356 maxt=1782547200000 ulid=01KW44XFTXG0BGSY5T4EQ5YDZ8
prometheus-1    | time=2026-07-14T09:25:04.125Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782547201354 maxt=1782554400000 ulid=01KW4BS72YX90TBEPH4BTYWQGC
prometheus-1    | time=2026-07-14T09:25:04.125Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782528266354 maxt=1782540000000 ulid=01KW4BS78J61DPC4MDESFT9M56
prometheus-1    | time=2026-07-14T09:25:04.125Z level=INFO source=repair.go:54 msg="Found healthy block" component=tsdb mint=1782554400000 maxt=1782561600000 ulid=01KXFYQDY22R0V9FPNXCDXW3CZ
nginx-1         | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
nginx-1         | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
nginx-1         | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
nginx-1         | 10-listen-on-ipv6-by-default.sh: info: IPv6 listen already enabled
nginx-1         | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
nginx-1         | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
nginx-1         | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
prometheus-1    | time=2026-07-14T09:25:04.247Z level=INFO source=tls_config.go:354 msg="Listening on" component=web address=[::]:9090
prometheus-1    | time=2026-07-14T09:25:04.247Z level=INFO source=tls_config.go:357 msg="TLS is disabled." component=web http2=false address=[::]:9090
prometheus-1    | time=2026-07-14T09:25:04.254Z level=INFO source=head.go:681 msg="Replaying on-disk memory mappable chunks if any" component=tsdb
prometheus-1    | time=2026-07-14T09:25:04.255Z level=INFO source=head.go:767 msg="On-disk memory mappable chunks replay completed" component=tsdb duration=3.69µs
prometheus-1    | time=2026-07-14T09:25:04.255Z level=INFO source=head.go:775 msg="Replaying WAL, this may take a while" component=tsdb
nginx-1         | /docker-entrypoint.sh: Configuration complete; ready for start up
otel-collector-1  | 2026-07-14T09:25:04.271Z    info    spanmetricsconnector@v0.146.0/connector.go:120  Building spanmetrics connector  {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "otelcol.component.id": "spanmetrics", "otelcol.component.kind": "connector", "otelcol.signal": "traces", "otelcol.signal.output": "metrics"}
otel-collector-1  | 2026-07-14T09:25:04.273Z    info    service@v0.146.1/service.go:241 Starting otelcol-contrib...     {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "Version": "0.146.1", "NumCPU": 2}
otel-collector-1  | 2026-07-14T09:25:04.273Z    info    extensions/extensions.go:40     Starting extensions...  {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}}
otel-collector-1  | 2026-07-14T09:25:04.279Z    info    spanmetricsconnector@v0.146.0/connector.go:216  Starting spanmetrics connector  {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "otelcol.component.id": "spanmetrics", "otelcol.component.kind": "connector", "otelcol.signal": "traces", "otelcol.signal.output": "metrics"}
otel-collector-1  | 2026-07-14T09:25:04.280Z    info    otlpreceiver@v0.146.1/otlp.go:120       Starting GRPC server    {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "otelcol.component.id": "otlp", "otelcol.component.kind": "receiver", "endpoint": "[::]:4317"}
otel-collector-1  | 2026-07-14T09:25:04.280Z    info    otlpreceiver@v0.146.1/otlp.go:175       Starting HTTP server    {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "otelcol.component.id": "otlp", "otelcol.component.kind": "receiver", "endpoint": "[::]:4318"}
otel-collector-1  | 2026-07-14T09:25:04.280Z    info    service@v0.146.1/service.go:264 Everything is ready. Begin running and processing data. {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}}
prometheus-1      | time=2026-07-14T09:25:04.317Z level=INFO source=head.go:812 msg="WAL checkpoint loaded" component=tsdb
prometheus-1      | time=2026-07-14T09:25:04.328Z level=INFO source=head.go:848 msg="WAL segment loaded" component=tsdb segment=40 maxSegment=43 duration=10.742032ms
prometheus-1      | time=2026-07-14T09:25:04.334Z level=INFO source=head.go:848 msg="WAL segment loaded" component=tsdb segment=41 maxSegment=43 duration=518.205µs
prometheus-1      | time=2026-07-14T09:25:04.334Z level=INFO source=head.go:848 msg="WAL segment loaded" component=tsdb segment=42 maxSegment=43 duration=243.797µs
prometheus-1      | time=2026-07-14T09:25:04.335Z level=INFO source=head.go:848 msg="WAL segment loaded" component=tsdb segment=43 maxSegment=43 duration=297.308µs
prometheus-1      | time=2026-07-14T09:25:04.335Z level=INFO source=head.go:885 msg="WAL replay completed" component=tsdb checkpoint_replay_duration=47.597927ms wal_replay_duration=17.283297ms wbl_replay_duration=250ns chunk_snapshot_load_duration=0s mmap_chunk_replay_duration=3.69µs total_replay_duration=80.01232ms
prometheus-1      | time=2026-07-14T09:25:04.405Z level=INFO source=main.go:1352 msg="filesystem information" fs_type=EXT4_SUPER_MAGIC
prometheus-1      | time=2026-07-14T09:25:04.405Z level=INFO source=main.go:1355 msg="TSDB started"
prometheus-1      | time=2026-07-14T09:25:04.406Z level=INFO source=main.go:1542 msg="Loading configuration file" filename=/etc/prometheus/prometheus.yml
prometheus-1      | time=2026-07-14T09:25:04.406Z level=INFO source=main.go:1582 msg="Completed loading of configuration file" db_storage=1.79µs remote_storage=2.761µs web_handler=1.06µs query_engine=1.98µs scrape=330.739µs scrape_sd=50.672µs notify=1.93µs notify_sd=1.5µs rules=2.35µs tracing=10.031µs filename=/etc/prometheus/prometheus.yml totalDuration=949.957µs
prometheus-1      | time=2026-07-14T09:25:04.407Z level=INFO source=main.go:1316 msg="Server is ready to receive web requests."
prometheus-1      | time=2026-07-14T09:25:04.407Z level=INFO source=manager.go:202 msg="Starting rule manager..." component="rule manager"
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: js vm init njs: 00007FA5B7385C80
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: using the "epoll" event method
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: nginx/1.29.8
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0) 
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: OS: Linux 5.19.0-1026-aws
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1024:524288
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: start worker processes
nginx-1           | 2026/07/14 09:25:04 [notice] 1#1: start worker process 22
mcp-client-1      | Starting MCP Mock Client
mcp-client-1      | Target: http://nginx:9000
mcp-client-1      | Duration: 2h0m0s
mcp-client-1      | Workers: 6
mcp-client-1      | Tools Variety: 8
mcp-client-1      | --- client-red tools (4/8) ---
mcp-client-1      | --- Tool Frequency Distribution (Deterministic) ---
mcp-client-1      | [get_forecast] Weight: 6 (100.0%)
mcp-client-1      | [get_stock_price] Weight: 9 (60.0%)
mcp-client-1      | [search_web] Weight: 5 (25.0%)

nginx-1           | 2026/07/14 09:25:04 [info] 22#22: *4 client 172.18.0.9 closed keepalive connection
mcp-client-1      | [translate_text] Weight: 2 (9.1%)
nginx-1           | 2026/07/14 09:25:04 [info] 22#22: *5 client 172.18.0.9 closed keepalive connection
mcp-client-1      | ---------------------------------------------------
nginx-1           | 2026/07/14 09:25:04 [info] 22#22: *6 client 172.18.0.9 closed keepalive connection
mcp-client-1      | --- client-green tools (6/8) ---
mcp-client-1      | --- Tool Frequency Distribution (Deterministic) ---

nginx-1           | 2026/07/14 09:25:04 [info] 22#22: *3 client 172.18.0.9 closed keepalive connection
mcp-client-1      | [get_forecast] Weight: 6 (100.0%)
mcp-client-1      | [get_stock_price] Weight: 9 (60.0%)
mcp-client-1      | [search_web] Weight: 5 (25.0%)
mcp-client-1      | [translate_text] Weight: 2 (9.1%)
mcp-client-1      | [calculate_sum] Weight: 8 (26.7%)
nginx-1           | 2026/07/14 09:25:04 [info] 22#22: *1 client 172.18.0.9 closed keepalive connection
mcp-client-1      | [resize_image] Weight: 12 (28.6%)
mcp-client-1      | ---------------------------------------------------
mcp-client-1      | --- client-blue tools (8/8) ---
mcp-client-1      | --- Tool Frequency Distribution (Deterministic) ---
mcp-client-1      | [get_forecast] Weight: 6 (100.0%)
mcp-client-1      | [get_stock_price] Weight: 9 (60.0%)

nginx-1           | 2026/07/14 09:25:05 [info] 22#22: *22 client 172.18.0.9 closed keepalive connection
mcp-client-1      | [search_web] Weight: 5 (25.0%)
mcp-client-1      | [translate_text] Weight: 2 (9.1%)
mcp-client-1      | [calculate_sum] Weight: 8 (26.7%)
mcp-client-1      | [resize_image] Weight: 12 (28.6%)
mcp-client-1      | [send_email] Weight: 17 (28.8%)
mcp-client-1      | [query_db] Weight: 19 (24.4%)
mcp-client-1      | ---------------------------------------------------
mcp-client-1      | --- client-purple tools (8/8) ---
mcp-client-1      | --- Tool Frequency Distribution (Deterministic) ---
mcp-client-1      | [get_forecast] Weight: 6 (100.0%)
mcp-client-1      | [get_stock_price] Weight: 9 (60.0%)
mcp-client-1      | [search_web] Weight: 5 (25.0%)
mcp-client-1      | [translate_text] Weight: 2 (9.1%)
mcp-client-1      | [calculate_sum] Weight: 8 (26.7%)
mcp-client-1      | [resize_image] Weight: 12 (28.6%)
mcp-client-1      | [send_email] Weight: 17 (28.8%)
mcp-client-1      | [query_db] Weight: 19 (24.4%)
mcp-client-1      | ---------------------------------------------------
mcp-client-1      | --- Client Distribution ---
mcp-client-1      | [client-red -> /mcp-stable] Workers: 1
mcp-client-1      | [client-green -> /mcp-flaky] Workers: 1
mcp-client-1      | [client-blue -> /mcp-sluggish] Workers: 2
mcp-client-1      | [client-purple -> /mcp-stable] Workers: 2
mcp-client-1      | ---------------------------
mcp-client-1      | Requests: (4/4/1/7) | Errors: (0/0/0/0) | RPS: (4/4/1/7)
nginx-1           | 2026/07/14 09:25:06 [info] 22#22: *26 client 172.18.0.9 closed keepalive connection
grafana-1         | t=2026-07-14T09:25:06.520058441Z level=warn caller=logger.go:224 time=2026-07-14T09:25:06.520051391Z msg="skipped registering status sub-resource that does not support dual writing" resource=playlists.playlist.grafana.app version=v0alpha1 storagePath=playlists/status
grafana-1         | logger=provisioning.plugins t=2026-07-14T09:25:06.776231159Z level=error msg="Failed to read plugin provisioning files from directory" path=/etc/grafana/provisioning/plugins error="open /etc/grafana/provisioning/plugins: no such file or directory"
grafana-1         | logger=provisioning.alerting t=2026-07-14T09:25:06.776679732Z level=error msg="can't read alerting provisioning files from directory" path=/etc/grafana/provisioning/alerting error="open /etc/grafana/provisioning/alerting: no such file or directory"
mcp-client-1      | Requests: (6/7/3/10) | Errors: (0/0/0/0) | RPS: (3/3/1/5)
nginx-1           | 2026/07/14 09:25:07 [info] 22#22: *65 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:07 [info] 22#22: *45 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:07 [info] 22#22: *80 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:07 [info] 22#22: *19 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (16/13/8/22) | Errors: (0/1/0/0) | RPS: (5/4/3/7)
nginx-1           | 2026/07/14 09:25:07 [info] 22#22: *64 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:07 [info] 22#22: *93 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *125 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *143 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *117 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *170 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *171 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *157 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *190 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *210 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *219 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (40/33/22/51) | Errors: (0/3/0/0) | RPS: (10/8/5/13)
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *237 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *205 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:08 [info] 22#22: *255 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:09 [info] 22#22: *274 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (49/38/35/61) | Errors: (0/4/0/0) | RPS: (10/8/7/12)
nginx-1           | 2026/07/14 09:25:09 [info] 22#22: *289 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:10 [info] 22#22: *307 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:10 [info] 22#22: *28 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:10 [info] 22#22: *20 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:10 [info] 22#22: *323 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:10 [info] 22#22: *345 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (60/45/39/77) | Errors: (0/4/0/0) | RPS: (10/7/6/13)
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *356 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *333 client 172.18.0.9 closed keepalive connection
prometheus-1      | time=2026-07-14T09:25:11.360Z level=INFO source=compact.go:584 msg="write block started" component=tsdb mint=1782561600000 maxt=1782568800000 ulid=01KXFZ3MJ0ZSP10218A38WWHQT
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *375 client 172.18.0.9 closed keepalive connection
prometheus-1      | time=2026-07-14T09:25:11.407Z level=INFO source=compact.go:609 msg="write block resulted in empty block" component=tsdb mint=1782561600000 maxt=1782568800000 duration=46.719483ms
prometheus-1      | time=2026-07-14T09:25:11.410Z level=INFO source=head.go:1422 msg="Head GC started" component=tsdb caller=truncateMemory
prometheus-1      | time=2026-07-14T09:25:11.419Z level=INFO source=head.go:1426 msg="Head GC completed" component=tsdb caller=truncateMemory duration=8.833838ms
prometheus-1      | time=2026-07-14T09:25:11.424Z level=INFO source=checkpoint.go:100 msg="Creating checkpoint" component=tsdb from_segment=40 to_segment=41 mint=1782568800000
prometheus-1      | time=2026-07-14T09:25:11.475Z level=INFO source=head.go:1387 msg="WAL checkpoint complete" component=tsdb first=40 last=41 duration=56.056175ms
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *383 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *24 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *95 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *389 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *427 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *429 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (77/60/53/99) | Errors: (0/8/0/0) | RPS: (11/9/8/14)
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *446 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *465 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *400 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:11 [info] 22#22: *477 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *495 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *509 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *525 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *535 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *490 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *552 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:12 [info] 22#22: *571 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (104/73/72/128) | Errors: (0/8/0/0) | RPS: (13/9/9/16)
nginx-1           | 2026/07/14 09:25:13 [info] 22#22: *585 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (106/77/76/132) | Errors: (0/8/0/0) | RPS: (12/9/8/15)
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *265 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *601 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *565 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *625 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *603 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (113/79/82/144) | Errors: (0/8/0/0) | RPS: (11/8/8/14)
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *641 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:14 [info] 22#22: *417 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (117/83/88/149) | Errors: (0/9/0/0) | RPS: (11/8/8/14)
nginx-1           | 2026/07/14 09:25:16 [info] 22#22: *661 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:16 [info] 22#22: *620 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:16 [info] 22#22: *672 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:16 [info] 22#22: *705 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (124/91/93/162) | Errors: (0/12/0/0) | RPS: (10/8/8/13)
nginx-1           | 2026/07/14 09:25:16 [info] 22#22: *693 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:16 [info] 22#22: *722 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (126/92/93/163) | Errors: (0/12/0/0) | RPS: (10/7/7/13)
mcp-client-1      | Requests: (128/93/98/167) | Errors: (0/12/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:18 [info] 22#22: *740 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *734 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *762 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *670 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *784 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *802 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *785 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *813 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *831 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *849 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *832 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *864 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:19 [info] 22#22: *876 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (153/117/116/197) | Errors: (0/16/0/0) | RPS: (10/8/8/13)
mcp-client-1      | Requests: (153/117/116/197) | Errors: (0/16/0/0) | RPS: (10/7/7/12)
nginx-1           | 2026/07/14 09:25:21 [info] 22#22: *863 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:21 [info] 22#22: *899 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:21 [info] 22#22: *653 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:21 [info] 22#22: *916 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:21 [info] 22#22: *938 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (163/126/122/210) | Errors: (0/16/0/0) | RPS: (10/7/7/12)
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *911 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *953 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *972 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *984 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *793 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *999 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:22 [info] 22#22: *965 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (176/134/132/224) | Errors: (0/17/0/0) | RPS: (10/7/7/12)
nginx-1           | 2026/07/14 09:25:23 [info] 22#22: *1017 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:23 [info] 22#22: *1040 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (180/136/136/234) | Errors: (0/17/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:23 [info] 22#22: *1055 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:24 [info] 22#22: *1025 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:24 [info] 22#22: *1068 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:24 [info] 22#22: *407 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:24 [info] 22#22: *1103 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:24 [info] 22#22: *1085 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:24 [info] 22#22: *1116 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (195/149/145/250) | Errors: (0/19/0/0) | RPS: (10/7/7/12)
nginx-1           | 2026/07/14 09:25:25 [info] 22#22: *336 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (201/153/150/256) | Errors: (0/21/0/0) | RPS: (10/7/7/12)
nginx-1           | 2026/07/14 09:25:25 [info] 22#22: *1157 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:25 [info] 22#22: *1127 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:26 [info] 22#22: *1168 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (204/156/154/264) | Errors: (0/21/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:26 [info] 22#22: *928 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:26 [info] 22#22: *1179 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1176 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1220 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1237 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1254 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1229 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1267 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1136 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:27 [info] 22#22: *1310 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (225/175/169/298) | Errors: (0/29/0/0) | RPS: (10/8/7/13)
mcp-client-1      | Requests: (225/175/169/298) | Errors: (0/29/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:29 [info] 22#22: *1286 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:29 [info] 22#22: *1322 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:29 [info] 22#22: *1343 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:29 [info] 22#22: *1354 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:29 [info] 22#22: *1332 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (235/182/176/310) | Errors: (0/29/0/0) | RPS: (9/7/7/12)
mcp-client-1      | Requests: (236/184/178/312) | Errors: (0/29/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:30 [info] 22#22: *1369 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:31 [info] 22#22: *1396 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:31 [info] 22#22: *1007 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:31 [info] 22#22: *1411 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:31 [info] 22#22: *1432 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (244/190/185/324) | Errors: (0/30/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:31 [info] 22#22: *1435 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:32 [info] 22#22: *1450 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (250/194/188/328) | Errors: (0/31/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:33 [info] 22#22: *1459 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:33 [info] 22#22: *1210 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:33 [info] 22#22: *1410 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (252/197/191/332) | Errors: (0/32/0/0) | RPS: (9/7/7/11)
mcp-client-1      | Requests: (254/199/194/335) | Errors: (0/34/0/0) | RPS: (8/7/6/11)
nginx-1           | 2026/07/14 09:25:34 [info] 22#22: *1478 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1508 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1486 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1532 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1535 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1525 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1561 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1567 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1599 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1601 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (275/221/207/368) | Errors: (0/40/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1620 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1581 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:35 [info] 22#22: *1634 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:36 [info] 22#22: *1650 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:36 [info] 22#22: *1664 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:36 [info] 22#22: *1640 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:36 [info] 22#22: *1679 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (291/234/214/383) | Errors: (0/41/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1695 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1714 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1726 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1689 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1749 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1483 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1762 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:37 [info] 22#22: *1740 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (306/248/226/405) | Errors: (0/42/0/0) | RPS: (9/8/7/12)
nginx-1           | 2026/07/14 09:25:38 [info] 22#22: *1783 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (307/251/228/411) | Errors: (0/42/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:38 [info] 22#22: *1795 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:38 [info] 22#22: *1810 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:38 [info] 22#22: *1834 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:39 [info] 22#22: *1847 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:39 [info] 22#22: *1376 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:39 [info] 22#22: *1871 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (320/256/237/423) | Errors: (0/43/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:40 [info] 22#22: *1870 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:40 [info] 22#22: *1827 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:40 [info] 22#22: *1089 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (326/260/239/430) | Errors: (0/43/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:40 [info] 22#22: *1908 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:41 [info] 22#22: *1917 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:41 [info] 22#22: *1930 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:41 [info] 22#22: *1892 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:41 [info] 22#22: *1771 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:41 [info] 22#22: *1891 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:41 [info] 22#22: *1941 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (342/270/246/442) | Errors: (0/44/0/0) | RPS: (9/7/7/12)
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *1953 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *1983 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2010 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2002 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2025 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2044 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *1939 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2042 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *1294 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (361/291/255/471) | Errors: (0/45/0/0) | RPS: (9/8/7/12)
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2078 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:42 [info] 22#22: *2079 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2115 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2130 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2107 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2141 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2166 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2148 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2080 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2182 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2205 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2192 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (384/315/268/498) | Errors: (0/47/0/0) | RPS: (10/8/7/13)
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2218 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:43 [info] 22#22: *2238 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:44 [info] 22#22: *2252 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:44 [info] 22#22: *2230 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:44 [info] 22#22: *2270 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (393/325/274/511) | Errors: (0/48/0/0) | RPS: (10/8/7/13)
mcp-client-1      | Requests: (394/326/275/513) | Errors: (0/48/0/0) | RPS: (10/8/7/13)
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *2288 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *2306 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *1859 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *2277 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *2325 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (404/334/283/527) | Errors: (0/48/0/0) | RPS: (10/8/7/13)
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *1970 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *2313 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:46 [info] 22#22: *2343 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:47 [info] 22#22: *2385 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (411/340/291/536) | Errors: (0/51/0/0) | RPS: (10/8/7/12)
nginx-1           | 2026/07/14 09:25:47 [info] 22#22: *2375 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:47 [info] 22#22: *2399 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2421 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2433 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2445 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2057 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2466 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2477 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2465 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2509 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (434/357/299/563) | Errors: (0/53/0/0) | RPS: (10/8/7/13)
nginx-1           | 2026/07/14 09:25:48 [info] 22#22: *2203 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:49 [info] 22#22: *2525 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:49 [info] 22#22: *2539 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:49 [info] 22#22: *2555 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:49 [info] 22#22: *2514 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:49 [info] 22#22: *2568 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:49 [info] 22#22: *2586 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (453/370/312/582) | Errors: (0/53/0/0) | RPS: (10/8/7/13)
nginx-1           | 2026/07/14 09:25:50 [info] 22#22: *2362 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:50 [info] 22#22: *2488 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:50 [info] 22#22: *2577 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:50 [info] 22#22: *2623 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:50 [info] 22#22: *2327 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:50 [info] 22#22: *2622 client 172.18.0.9 closed keepalive connection
mcp-client-1      | Requests: (459/378/318/593) | Errors: (0/54/0/0) | RPS: (10/8/7/13)
mcp-client-1      | Requests: (459/378/318/593) | Errors: (0/54/0/0) | RPS: (10/8/7/13)
nginx-1           | 2026/07/14 09:25:51 [info] 22#22: *2645 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:52 [info] 22#22: *2668 client 172.18.0.9 closed keepalive connection
Gracefully Stopping... press Ctrl+C again to force
Container demo-grafana-1 Stopping 
Container demo-mcp-client-1 Stopping 
mcp-client-1      | Requests: (463/382/324/597) | Errors: (0/55/0/0) | RPS: (10/8/7/12)
Container demo-mcp-client-1 Stopped 
Container demo-nginx-1 Stopping 
mcp-client-1 exited with code 2
nginx-1           | 2026/07/14 09:25:53 [notice] 1#1: signal 3 (SIGQUIT) received, shutting down
grafana-1 exited with code 0
Container demo-grafana-1 Stopped 
Container demo-prometheus-1 Stopping 
prometheus-1      | time=2026-07-14T09:25:53.595Z level=WARN source=main.go:1118 msg="Received an OS signal, exiting gracefully..." signal=terminated
prometheus-1      | time=2026-07-14T09:25:53.595Z level=INFO source=main.go:1143 msg="Stopping scrape discovery manager..."
prometheus-1      | time=2026-07-14T09:25:53.595Z level=INFO source=main.go:1157 msg="Stopping notify discovery manager..."
prometheus-1      | time=2026-07-14T09:25:53.595Z level=INFO source=manager.go:216 msg="Stopping rule manager..." component="rule manager"
prometheus-1      | time=2026-07-14T09:25:53.595Z level=INFO source=manager.go:232 msg="Rule manager stopped" component="rule manager"
prometheus-1      | time=2026-07-14T09:25:53.595Z level=INFO source=main.go:1194 msg="Stopping scrape manager..."
prometheus-1      | time=2026-07-14T09:25:53.596Z level=INFO source=main.go:1139 msg="Scrape discovery manager stopped"
prometheus-1      | time=2026-07-14T09:25:53.619Z level=INFO source=main.go:1153 msg="Notify discovery manager stopped"
prometheus-1      | time=2026-07-14T09:25:53.651Z level=INFO source=manager.go:561 msg="Stopping notification manager..." component=notifier
prometheus-1      | time=2026-07-14T09:25:53.672Z level=INFO source=manager.go:301 msg="Draining any remaining notifications..." component=notifier
prometheus-1      | time=2026-07-14T09:25:53.682Z level=INFO source=manager.go:307 msg="Remaining notifications drained" component=notifier
prometheus-1      | time=2026-07-14T09:25:53.682Z level=INFO source=manager.go:234 msg="Notification manager stopped" component=notifier
prometheus-1      | time=2026-07-14T09:25:53.682Z level=INFO source=main.go:1466 msg="Notifier manager stopped"
prometheus-1      | time=2026-07-14T09:25:53.682Z level=INFO source=main.go:1186 msg="Scrape manager stopped"
prometheus-1      | time=2026-07-14T09:25:53.682Z level=INFO source=main.go:1480 msg="See you next time!"
prometheus-1 exited with code 0
Container demo-prometheus-1 Stopped 
nginx-1           | 2026/07/14 09:25:54 [info] 22#22: *2597 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:54 [info] 22#22: *2417 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:54 [info] 22#22: *2648 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:54 [info] 22#22: *2624 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:54 [info] 22#22: *2685 client 172.18.0.9 closed keepalive connection
nginx-1           | 2026/07/14 09:25:54 [info] 22#22: *2665 epoll_wait() reported that client prematurely closed connection, so upstream connection is closed too while connecting to upstream, client: 172.18.0.9, server: , request: "POST /mcp-flaky HTTP/1.1", upstream: "http://172.18.0.4:9002/mcp", host: "nginx:9000"
nginx-1           | 2026/07/14 09:25:54 [notice] 22#22: gracefully shutting down
nginx-1           | 2026/07/14 09:25:54 [notice] 22#22: exiting
nginx-1           | 2026/07/14 09:25:54 [notice] 22#22: exit
nginx-1           | 2026/07/14 09:25:54 [notice] 1#1: signal 17 (SIGCHLD) received from 22
nginx-1           | 2026/07/14 09:25:54 [notice] 1#1: worker process 22 exited with code 0
nginx-1           | 2026/07/14 09:25:54 [notice] 1#1: exit
Container demo-nginx-1 Stopped 
Container demo-otel-collector-1 Stopping 
Container demo-mcp-stable-1 Stopping 
Container demo-mcp-flaky-1 Stopping 
Container demo-mcp-sluggish-1 Stopping 
nginx-1 exited with code 0
otel-collector-1  | 2026-07-14T09:25:54.925Z    info    otelcol@v0.146.1/collector.go:375       Received signal from OS {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "signal": "terminated"}
otel-collector-1  | 2026-07-14T09:25:54.925Z    info    service@v0.146.1/service.go:278 Starting shutdown...    {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}}
otel-collector-1  | 2026-07-14T09:25:54.925Z    info    spanmetricsconnector@v0.146.0/connector.go:236  Shutting down spanmetrics connector     {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "otelcol.component.id": "spanmetrics", "otelcol.component.kind": "connector", "otelcol.signal": "traces", "otelcol.signal.output": "metrics"}
otel-collector-1  | 2026-07-14T09:25:54.925Z    info    spanmetricsconnector@v0.146.0/connector.go:238  Stopping ticker {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}, "otelcol.component.id": "spanmetrics", "otelcol.component.kind": "connector", "otelcol.signal": "traces", "otelcol.signal.output": "metrics"}
otel-collector-1  | 2026-07-14T09:25:54.925Z    info    extensions/extensions.go:68     Stopping extensions...  {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}}
otel-collector-1  | 2026-07-14T09:25:54.925Z    info    service@v0.146.1/service.go:292 Shutdown complete.      {"resource": {"service.instance.id": "1c2eb612-de74-4e1e-a474-b745da1e37d7", "service.name": "otelcol-contrib", "service.version": "0.146.1"}}
Container demo-mcp-sluggish-1 Stopped 
mcp-sluggish-1 exited with code 2
Container demo-otel-collector-1 Stopped 
otel-collector-1 exited with code 0
Container demo-mcp-stable-1 Stopped 
mcp-stable-1 exited with code 2
Container demo-mcp-flaky-1 Stopped 
mcp-flaky-1 exited with code 2
ubuntu@ip-10-1-1-4:~/nginx-mcp-js/demo$ cat docker-compose.yaml 
# Copyright (C) Dmitry Volyntsev
# Copyright (C) F5, Inc.

services:
  # NGINX reverse proxy with njs and OpenTelemetry
  nginx:
    image: nginx:alpine-otel
    ports:
      - "9000:9000"
    volumes:
      - ./nginx/mcp.conf:/etc/nginx/nginx.conf:ro
      - ../mcp.js:/etc/nginx/mcp.js:ro
    depends_on:
      - mcp-stable
      - mcp-flaky
      - mcp-sluggish
      - otel-collector
    networks:
      - mcp-network

  # OpenTelemetry Collector with spanmetrics connector
  otel-collector:
    image: otel/opentelemetry-collector-contrib:0.146.1
    volumes:
      - ./otel/config.yaml:/etc/otelcol-contrib/config.yaml:ro
    networks:
      - mcp-network

  # Prometheus for metrics storage
  prometheus:
    image: prom/prometheus:v3.9.1
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus/prometheus.yaml:/etc/prometheus/prometheus.yml:ro
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/usr/share/prometheus/console_libraries'
      - '--web.console.templates=/usr/share/prometheus/consoles'
    depends_on:
      - otel-collector
    networks:
      - mcp-network

  # Grafana for visualization
  grafana:
    image: grafana/grafana-oss:12.3.3
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
      - GF_AUTH_DISABLE_LOGIN_FORM=false
      - GF_LOG_LEVEL=warn
    volumes:
      - ./grafana/provisioning:/etc/grafana/provisioning:ro
    depends_on:
      - prometheus
    networks:
      - mcp-network

  # MCP Server: stable (no errors, base latency)
  mcp-stable:
    build:
      context: ./mcp
      dockerfile: Dockerfile
    command:
      - "/mcp_server"
      - "--name"
      - "mcp-stable"
      - "--port"
      - "9001"
      - "--error-rate"
      - "0"
      - "--tool-error-rate"
      - "0"
      - "--long-rate"
      - "0"
    networks:
      - mcp-network

  # MCP Server: flaky (~2% protocol errors, ~10% tool errors)
  mcp-flaky:
    build:
      context: ./mcp
      dockerfile: Dockerfile
    command:
      - "/mcp_server"
      - "--name"
      - "mcp-flaky"
      - "--port"
      - "9002"
      - "--error-rate"
      - "0.02"
      - "--tool-error-rate"
      - "0.10"
      - "--long-rate"
      - "0"
    networks:
      - mcp-network

  # MCP Server: sluggish (no errors, elevated latency)
  mcp-sluggish:
    build:
      context: ./mcp
      dockerfile: Dockerfile
    command:
      - "/mcp_server"
      - "--name"
      - "mcp-sluggish"
      - "--port"
      - "9003"
      - "--error-rate"
      - "0"
      - "--tool-error-rate"
      - "0"
      - "--max-latency"
      - "100ms"
    networks:
      - mcp-network

  # MCP Client: traffic generator
  mcp-client:
    build:
      context: ./mcp
      dockerfile: Dockerfile
    command:
      - "/mcp_client"
      - "-url"
      - "http://nginx:9000"
      - "-duration"
      - "2h"
      - "-workers"
      - "6"
    depends_on:
      - nginx
    networks:
      - mcp-network

networks:
  mcp-network:
    driver: bridge
ubuntu@ip-10-1-1-4:~/nginx-mcp-js/demo$
```

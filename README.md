# Docker Fast Reverse Proxy

Server docker:
```
docker build -t docker-frp-server/project:latest-prod .

docker run --log-driver json-file --log-opt max-size=32m --log-opt max-file=1 --restart=always -itd --name docker-frp-server -e MODE=server -e FRP_TOKEN=12345678 -e ALLOW_PORTS_START=6000 -e ALLOW_PORTS_END=6999 -p 7000:7000 -p 6000-6999:6000-6999 --expose=6000-6999 docker-frp-server/project:latest-prod
```

Client docker:
```
docker build -t docker-frp-client/project:latest-prod .

docker run --log-driver json-file --log-opt max-size=32m --log-opt max-file=1 --restart=always -itd --name docker-frp-client -e MODE=client -e FRP_TOKEN=12345678 -e SERVER_ADDR=frp.example.com -e SERVER_PORT=7000 -e PROTO=tcp -e LOCAL_IP=192.168.1.100 -e LOCAL_PORT=22 -e REMOTE_PORT=6000 docker-frp-client/project:latest-prod
```

Parameters:
```
$MODE
$FRP_TOKEN
$LOG_FILE
```

Server parameters:
```
$ALLOW_PORTS_START
$ALLOW_PORTS_END
```

Client parameters:
```
$SERVER_ADDR
$FRP_USER
$PROXY_NAME
$SERVER_PORT
$PROTO
$LOCAL_IP
$LOCAL_PORT
$REMOTE_PORT
```
# Livekit demo app

The Livekit demo application use [Livekit docker](https://docs.livekit.io/oss/deployment/vm/) and [Client-sdk-js](https://github.com/livekit/client-sdk-js) example

## Installation

- Docker and Docker compose
- NodeJS and yarn
- [Livekit-cli](https://docs.livekit.io/getting-started/cli-setup/)
- Generate a API-Key and API-Secret pair and write it into `livekit.yaml` file (configuration file)

```yaml
port: 7880
rtc:
  tcp_port: 7881
  port_range_start: 50000
  port_range_end: 60000
  use_external_ip: true
# redis:
#     address: localhost:6379
#     username: ""
#     password: ""
#     db: 0
turn:
  enabled: false
  # domain: xyz.com
  # cert_file: ""
  # key_file: ""
  # tls_port: 5349
  # udp_port: 443
  # external_tls: true
keys:
  <your-api-key>: <your-api-secret>
```

For the demo purpose, I don't use redis for [Multi-node routing](https://docs.livekit.io/oss/deployment/distributed/)

## Start the demo

### Start Livekit server

```shell
docker compose up -d
```

### Start web client example

- Go to the client directory

```shell
cd client-sdk-js/
```

- Install dependencies

```shell
yarn install
```

- Start the example

```shell
yarn sample
```

The command will open the browser on http://localhost:8080

## Create a conference

- Go to the url http://localhost:8080 and enable your mic and camera.

- Create a token by `livekit-cli` 

```shell
livekit-cli create-token \
    --api-key <your-api-key> --api-secret <your-api-secret> \
    --join --room my-first-room --identity user1 \
    --valid-for 24h
```

- Copy the token and pates to `Token` input. Then click connect.

- For other participants want to join room you need to create another token with the identity specify to them. Ex:

```shell
livekit-cli create-token \
    --api-key <your-api-key> --api-secret <your-api-secret> \
    --join --room my-first-room --identity user2 \
    --valid-for 24h
```

- Open new tab Copy the token and pates to `Token` input. Then click connect.
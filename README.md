# rocketmq-docker-compose

Run minimal RocketMQ in docker with one-line command.

This minimal deployment is only for **local development** use.

## Usage

### Linux

```
mkdir -p volumes/logs volumes/store && chmod -R a+w volumes && curl -sS https://raw.githubusercontent.com/RangerCD/rocketmq-docker-compose/master/docker-compose.yml | docker compose -f - up -d
```

### Windows(PowerShell)

```
(Invoke-WebRequest -URI https://raw.githubusercontent.com/RangerCD/rocketmq-docker-compose/master/docker-compose.yml -UseBasicParsing).Content | docker compose -f - up -d
```

This one-line command will:
- Create a directory named `volumes`, store RocketMQ `logs` and `store` inside.
- Create a minimal RocketMQ with `docker-compose.yml` in this repo.
- Expose these ports through `127.0.0.1`:
  - `9876` for RocketMQ namesrv
  - `10909`/`10911`/`10912` for RocketMQ broker
  - `8080` for RocketMQ dashboard

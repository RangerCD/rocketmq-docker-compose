# rocketmq-docker-compose

Run minimal RocketMQ in docker with one-line command.

This minimal deployment is only for **local development** use.

## TL;DR

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

## Usage

### 1. Get `docker-compose.yml`

Use your favorite tool:

```
curl -O https://raw.githubusercontent.com/RangerCD/rocketmq-docker-compose/master/docker-compose.yml
```

or

```
wget https://raw.githubusercontent.com/RangerCD/rocketmq-docker-compose/master/docker-compose.yml
```

or clone this repo

```
git clone https://github.com/RangerCD/rocketmq-docker-compose.git && cd rocketmq-docker-compose
```

### 2. [Linux] Create volumes directory & grant permissions

Mismatched UID & GID will cause broker exit with code 253, so we have to create volumes and grant permissions in advance.

```
mkdir -p volumes/logs volumes/store && chmod -R a+w volumes
```

This command will create `volumes/logs` and `volumes/store` directories and grant write permission to anyone.

### 3. Start docker compose

```
docker compose up -d
```

Output should be like:

```
[+] Running 4/4
 - Network rocketmq-network      Created                       0.0s 
 - Container rocketmq-broker     Started                       0.9s 
 - Container rocketmq-namesrv    Started                       0.8s 
 - Container rocketmq-dashboard  Started                       1.1s
 ```

 RocketMQ is ready, we can connect to namesrv through `localhost:9876`. Dashboard is also ready at [http://localhost:8080](http://localhost:8080)

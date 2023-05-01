# DemoReplicasDocker

## Build an image

```bash
mvn install
```

```bash
docker build -t trodix/demo-replicas-docker .
```

## Init Swarm

```bash
docker swarm init --advertise-addr 192.168.1.18
```

## With docker command

```bash
docker service create --name "DemoReplicasDocker" -p 7000:7000 --replicas=2 trodix/demo-replicat-docker
```

```bash
docker service logs -f "DemoReplicasDocker"
```

```bash
curl 192.168.1.18:7000/hello
```

## With docker compose file

```yml
services:
  demo-replicas-docker:
    image: trodix/demo-replicas-docker
    ports:
      - "7000:7000"
    deploy:
      replicas: 2
```

```bash
docker stack deploy --compose-file docker-compose.yml DemoReplicasDocker
```

```bash
docker service logs -f DemoReplicasDocker_demo-replicas-docker 
```

```bash
curl 192.168.1.18:7000/hello
```

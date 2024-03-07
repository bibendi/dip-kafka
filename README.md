# Dip Kafka

Apache Kafka configuration for [Dip infra services](https://github.com/bibendi/dip).

## Usage

1. Add a service to the application's `dip.yml`.

```yaml
infra:
  kafka:
    git: https://github.com/bibendi/dip-kafka.git
```

2. Add a network to the application's `docker-compose.yml`.

```yaml
networks:
  kafka-net:
    name: ${DIP_INFRA_NETWORK_KAFKA}
    external: true
```

Where `DIP_INFRA_NETWORK_KAFKA` is a special variable that is set by Dip.

3. Add a `KAFKA_URL` environment variable and the `kafka-net` network to a Docker Compose service.

```yaml
services:
  app:
    environment:
      BROKER_URL: kafka:9092
    networks:
      - default
      - kafka-net
```

4. Start infra services.

```sh
dip infra up
```

5. Start the app

```sh
dip up
```

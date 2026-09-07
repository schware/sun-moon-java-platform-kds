# sun-moon-java-platform-kds

Kitchen Display System (KDS) — part of the `sun-moon-java-platform`
family (alongside [Order](https://github.com/schware/sun-moon-java-platform-order)
and [Delivery](https://github.com/schware/sun-moon-java-platform-delivery),
tied together by the
[umbrella repo](https://github.com/schware/sun-moon-java-platform) via
git submodules).

**Docker-deployed**, one container per service. Replaces
[sun-moon-java-platform-kds-jetty](https://github.com/schware/sun-moon-java-platform-kds-jetty)
(archived, WAR + shared external Jetty).

## Why Redis

Tickets are a small, hot, constantly-updated working set. See the
umbrella repo's `docs/adr/0001`.

## API

- `POST /tickets` — create a kitchen ticket (`{"orderId": "..."}`) in
  `RECEIVED` status.

## Build & run

Requires JDK 21+, and Redis reachable at `localhost:6379`.

```
./gradlew test
./gradlew bootJar
java -jar build/libs/sun-moon-java-platform-kds-0.1.0.jar
```

## Docker

```
docker build -t sun-moon-kds .
docker run --network host sun-moon-kds
```

See [Debian-Setting `docs/docker.md`](https://github.com/schware/Debian-Setting/blob/master/docs/docker.md)
for how this actually runs (docker-compose, alongside Order/Delivery).

Listens on port **8081** (see `application.yml`).

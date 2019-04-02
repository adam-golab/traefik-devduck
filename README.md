# Traefik DevDuck presentation files

## 01 Quick Start

Run without any additional configuration just run the following command:

```
docker-compose up -d traefik
```

to run only Traefik. If you want to run the Hello World application then run:

```
docker-compose up -d hello-world
```

When you have running Traefik you can also any additional container. Remember to provide correct network name.

```
 docker run -d \
   -e PORT=8080 \
   -e WORLD=Adam \
   --network 01-quick-start_default \
   --expose 8080 \
   --label traefik.http.routers.adam-hello-world.rule="Host(\`adam.devduck.ml\`)" adamgolab/hello-world
```

## 02 File Provider

More real world scenario, with configuration provided by config file.

Additionally Traefik provides Web UI for checking added routes and services.

Again everything can be run via simple command:

```
docker-compose up -d
```

When everything is set up and running you can view the dashboard on `treafik.devduck.ml`.

# Traefik DevDuck presentation files

## 01 Quick Start

Run without any additional configuration just run the following command:

```
docker-compose up -d traefik
```

To run only Traefik. If you want to run the Hello World application then run:

```
docker-compose up -d hello-world
```

When you have running Traefik, you can run an additional container. Remember to provide the correct network name.

```
 docker run -d \
   -e PORT=8080 \
   -e WORLD=Adam \
   --network 01-quick-start_default \
   --expose 8080 \
   --label traefik.http.routers.adam-hello-world.rule="Host(\`adam.devduck.ml\`)" adamgolab/hello-world
```

## 02 File Provider

More real-world scenario, with the configuration provided by a config file.

Additionally, Traefik provides Web UI for checking added routes and services.

Again everything can be run via the simple command:

```
docker-compose up -d
```

When everything is set up and running, you can view the dashboard on `traefik.devduck.ml`.

## 03 TLS Support

We are living in 2019 so why the response should not be encrypted? When there is present a flag for enabling TLS support `tls=true`,
Traefik will automatically look for a corresponding certificate and encrypt the response. 

Run everything with the command:

```
docker-compose up -d
```

After that, you can check the encrypted response on `https://tls.devduck.ml`. Check the certificate that is obtained from [Let's Encrypt](https://letsencrypt.org/) service.

## 04 TCP Support

**New Feature available only on 2.0**

In general there are not so many cases where you should expose MongoDB instance publicly. But it will work in the same way for any other TCP service.

Run everything with:

```
docker-compose up -d
```

On `http://devduck.ml/` should be displayed an webpage with a Hello World message, but you are able to hit the MongoDB instance on `devduck.ml:27017`.

## 05 Load Balancing

The load balancers are able to load balance the requests between multiple instances of your programs.

Run everything with:

```
docker-compose up -d
```

On `http://thanos.devduck.ml` should be displayed a message from one of the containers. Every second request should be should be handled by the second container.
Refresh the page a few times to see different results.

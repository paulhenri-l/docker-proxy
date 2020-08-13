# Docker local dev proxy for mac

As this currently is a poc the documentation is not really on point. Feel free 
to open an issue if you're interested in what is going on here :)

*I make the assumption that you have dnsmasq configured to send .test to 127.0.0.1*

## Installation

Clone the repo

## Usage

Create the proxy network.

```
docker network create docker-proxy
```

Start the proxy.

```
cd docker-proxy
docker-compose up
```

Now that the proxy is running you can use it inside your other projects.

```
version: "3"

networks:
  docker-proxy:
    external: true

services:
  some-application:
    image: "nginx:latest"
    networks:
      docker-proxy:
        aliases:
          - some-application.test
```

```
curl some-application.test
```

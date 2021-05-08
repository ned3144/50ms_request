# TCP 40ms

A common problem that can occur while using TCP is a 40ms latency problem caused by the combination of Nagle's algorithm and TCP delayed acknowledgment used by the Linux kernel. The purpose of this repo is to recrate the problem, thus allowing for people to investigate the problem and try to debug it themselves.  
This was inspired by the `The Case of the 50ms request` exercise in [wizardzines's mysteries](https://mysteries.wizardzines.com/).

## Getting started

### Compose container

Build the docker images and run them

```bash
docker-compose up
```

You will see the logs generated by the containers.

### Interactive shell

Run an interactive shell inside either container for investigating

```bash
docker exec -it tcp_40ms_client_1 /bin/sh # For client
docker exec -it tcp_40ms_server_1 /bin/sh # For server
```

> Notice that the hostname of both containers are server/client respectively.

### Server

The server runs a simple [express server](server/server.js) that listens on port `8080`

### Client

The client is just a simple alpine based image containing a script [slow.js](client/slow.js)
that recrates the problem, by posting data to the server and measuring the time it took.

```bash
node server.js
```
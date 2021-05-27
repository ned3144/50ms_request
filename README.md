# The Case of the 50ms request

This repo is a live demo of the puzzle `The Case of the 50ms request` from [wizardzines's mysteries](https://mysteries.wizardzines.com/), thus allowing for people to investigate the problem and try to debug it themselves.

## Problem 
You have a program that uploads very tiny files to a server. You notice in your monitoring that these file uploads are a little slow — maybe about 50ms on average.
The uploading code is in Javascript, so you write a tiny Javascript program called [slow.js](client/slow.js) to reproduce the problem so you can easily investigate it. The program prints out the time elapsed for the request in milliseconds.

You have a choice: you can SSH to the client machine (which is making the requests), or the server machine (which is serving the requests).

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
docker exec -it server /bin/sh # For server
docker exec -it client /bin/sh # For client
```

> Notice that the hostname of both containers are server/client respectively.

### Server

The server runs a simple HTTP server that listens on port `8000`

> IMPORTANT: Do not look at the server implementation (`server.py`) it contains spoilers.

### Client

The client is just a simple alpine based image containing a script [slow.js](client/slow.js)
that recrates the problem, by posting data to the server and measuring the time it took.

```bash
node slow.js
```

You are allowed to examine this script.

## Solution

The solution can be found [here](SOLUTION.md).

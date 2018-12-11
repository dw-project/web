---
title: DWRTC - Distributed WebRTC Signalling
type: docs
---

# DWRTC - Distributed WebRTC Signalling

Hi! Welcome to the Distributed WebRTC project page.

DWRTC extends WebRTC with a decentralized connection setup. Users connect to different nodes on the Internet. These nodes are connected via a P2P network which stores the routing information. The connection setup messages are routed through this network. The WebRTC connection can then be used to send data, audio and video directly from web browser to web browser.

This project implements this idea. As a proof of concept, it also includes a video call application using DWRTC to establish calls to a partner.

## Demo

Go here to start a demo: [demo.dwrtc.net](https://demo.dwrtc.net) or connect to a node directly: [node1.dwrtc.net](https://node1.dwrtc.net), [node2.dwrtc.net](https://node2.dwrtc.net)

## Local Usage

```sh
$ docker-compose up -d
$ docker-compose ps

    Name               Command           State                        Ports
-------------------------------------------------------------------------------------------------
dwrtc_node1_1   java -jar /app/app.jar   Up      0.0.0.0:PORT1->7000/tcp, 0.0.0.0:32770->7532/tcp
dwrtc_node2_1   java -jar /app/app.jar   Up      0.0.0.0:PORT2->7000/tcp, 0.0.0.0:32768->7532/tcp
```

Connect to `localhost:PORT1` for node1 and `localhost:PORT2` for node2 via a web browser. You can also connect to the TomP2P ports (`32768`/`32770` in this case) to bootstrap any instance running outside of this network.

## Options

Options are loaded using [Konfig](https://github.com/npryce/konfig). The priorities are:

1. Command Line Properties overrides
2. Environment Variables overrides
3. Property file `defaults.properties`

Use the "dot"-syntax (`http.port`) for command line and property file, and "underscore"-syntax for environment variables (`HTTP_PORT`).

The options are:

* Peer Port (Int): `peer.port`/`PEER_PORT`: port the TomP2P peer runs on
* Webserver IP (String): `http.ip`/`HTTP_IP`: the IP the web server binds to (e.g. "127.0.0.1", "localhost", "0.0.0.0")
* Webserver Port (Int): `http.port`/`HTTP_PORT`: the port the web server binds to
* Bootstrap Peer (comma-separated list of `HOST:PORT` pairs): `bootstrap.peer`/`BOOTSTRAP_PEER` the list of peers to bootstrap to (e.g. "1.1.1.1:4000,2.2.2.2:3000")

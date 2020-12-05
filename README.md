# docker-iperf2

iPerf2 in an Alpine-based Docker image. Small, lightweight and (most importantly) up-to-date with source.

## Running as a server

To run docker-iperf2 as a server in the foreground:

`docker run -it --rm --network=host ingenieurmt/docker-iperf2 --server`

Or alternatively, you can run it as a daemon in the background:

`docker run -d --name iperf2-server --network=host ingenieurmt/docker-iperf2 --server`

## Running as a client

There's a few ways to do this, but the basic gist is:

`docker run -it --rm --network=host ingenieurmt/docker-iperf2 --client <SERVER_IP> <OPTIONS>`

## Explanatory notes

- iPerf2 has a lot of tunables and options available (especially on the client side). These are all documented [here](https://sourceforge.net/projects/iperf2/files/iperf-manpage.html/download).

- The use of `network=host` is recommended so as to avoid the Docker network proxy and ensure the best possible throughput for test conditions. It is possible to use port forwarding commands for extra security, however performance may be affected. For example, you can run a server like this:

   `docker run -d --name iperf2-server -p 5201:5201/tcp -p 5201:5201/udp ingenieurmt/docker-iperf2 --server`
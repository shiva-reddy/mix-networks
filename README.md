# Mix networks

The goal is to build a simple mix network server using Go, with a suite of mixing strategies. Our inspiration for our project is this work which implements a threshold mix network using an express nodejs server, and our understanding of several mixing strategies as specified by the following papers:
- https://www.freehaven.net/anonbib/cache/trickle02.pdf
- https://www.freehaven.net/anonbib/cache/danezis:wpes2003.pdf
- https://www.freehaven.net/anonbib/cache/loopix2017.pdf

The mixing strategies we implemented are:-
- Threshold mix
- Timed mix
- Timed dynamic pool mix
- Poisson mix
- Red green black mix


Our executables are:

 1. A mock client which sends a series of requests to the routing server. Each request contains the intended recipient address and actual message content. 

	The next recipient address is encrypted with:
	- The routing server’s public key


	The message content of each request is encrypted with:
	- The routing server’s public key.
	- The receiver's public key


2. A mix node which receives requests, decrypts each message’s next recipient address (with its private key) and forwards the message content (which is still encrypted with the receiver's public key) as a new request to its destination. 

	The mixing strategy and configuration decides how the router mixes requests and hence randomizes the order of the requests sent by the router to their corresponding recipients.


3. A mock server which receives the request and logs it to a file.


## Generating key pairs

```bash
openssl genrsa -out private.pem 2048
openssl rsa -in private.pem -outform PEM -pubout -out public.pem
```

## Running tests

```bash
make test
```

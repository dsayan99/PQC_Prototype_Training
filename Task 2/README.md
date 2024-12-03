# Task 2 - Creating a Quantum Safe nginx Server using liboqs, openssl3 and oqs-provider

First, let us create a docker container that will spawn an nginx server using default openssl and will use default key exchange algorithms.

# nginx-default
A nginx demo server on localhost.

1. Navigate to `Task 2\nginx-default`.
2. Run `docker build -t nginx-default .` to build the container. This will open the terminal inside the container.
3. Run `docker run --detach --rm --name nginx-default -p 443:443 nginx-default` to start the server.
3. The server will start on port 443. To edit the port and the server configuration, open a terminal and then navigate to `/etc/nginx/nginx.conf` and change the code for HTTPS Server. The server needs to be restarted after changing the configruation.
4. Open the Browser, open `https://localhost:443`. Right Click -> Inspect -> Security. The Key Exchange Protocol will be visible.

The Key Exchange protocol will most likely show X25519 Key Exchange which is a Pre-Quantum Key Exchange Protocol.

Using `openssl s_client`, a connection can also be established with the server.

1. Run `docker exec -it <container_id> bash` to open a terminal within the container. Replace `<container_id>` with the actual docker container id which can be retrieved from `docker ps -a`.
2. Run `openssl s_client -connect localhost:443 -groups x25519`

A connection will be established with the nginx server and the details about the key used, cipher, certificate information will be available in the terminal.

# oqs-nginx

A pre-requisite to this step is installing a beta version of Chrome 131+ or Firefox 132+.

1. Navigate to `Task 2\oqs-nginx`.
2. `docker build -t oqs-nginx .` This will generate the image with a default rsa:2048 algorithm.
3. Run `docker run --detach --rm --name oqs-nginx -p 4433:4433 oqs-nginx` to start the server.
4. The configuration is defined in the `nginx-conf\nginx.conf` file.
5. Open the Browser, open `https://localhost:4433`. Right Click -> Inspect -> Security. The Key Exchange Protocol will be visible.

The Key Exchange Protocol should reflect X25519MLKEM768 if every step is followed correctly.

Using `openssl s_client`, a connection can also be established with the server.

1. Run `docker exec -it <container_id> /bin/sh` to open a terminal within the container. Replace `<container_id>` with the actual docker container id which can be retrieved from `docker ps -a`.
2. Run `openssl s_client -connect localhost:4433 -groups X25519MLKEM768`

Additionally, the docker image also creates a Certificate using `dilithium3`.

1. `openssl s_server -key pki/server_d3.key -cert pki/server_d3.crt -CAfile cacert/CA_d3.crt -accept 4533` will start a server using openssl with the dilithium3 certificate.
2. `openssl s_client -connect localhost:4533 -groups X25519MLKEM768` will establish a connection with the above server.

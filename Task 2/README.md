# Task 2 - Creating a Quantum Safe nginx Server using liboqs, openssl3 and oqs-provider

First, let us create a docker container that will spawn an nginx server using default openssl and will use default key exchange algorithms.

# nginx-default
A nginx demo server on localhost.

1. Navigate to `Task 2\nginx-default`.
2. Run `docker build -t nginx-rsa .` to build the container. This will open the terminal inside the container.
3. Within the terminal, type `nginx -c /etc/nginx/nginx.conf -g "daemon off;"` The server will start on port 443. To edit the port and the server configuration navigate to `/etc/nginx/nginx.conf` and change the code for HTTPS Server. The server needs to be restarted after changing the configruation.
4. Open the Browser, open `https:localhost:443`. Right Click -> Inspect -> Security. The Key Exchange Protocol will be visible.

The Key Exchange protocol will most likely show X25519 Key Exchange which is a Pre-Quantum Key Exchange Protocol.

# oqs-nginx

A pre-requisite to this step is installing a beta version of Chrome 131+ or Firefox 132+.

1. Navigate to `Task 2\nginx-default`.
2. `docker build -t oqs-nginx .` This will generate the image with a default rsa:2048 algorithm.
3. `docker run -it oqs-nginx` will open the terminal inside the docker container.
4. `nginx -c nginx-conf/nginx.conf -g "daemon off;"` will start the server on the defined port in the `nginx-conf\nginx.conf` file.
5. Open the Browser, open `https:localhost:4433`. Right Click -> Inspect -> Security. The Key Exchange Protocol will be visible.

The Key Exchange Protocol should reflect X25519MLKEM768 if every step is followed correctly.



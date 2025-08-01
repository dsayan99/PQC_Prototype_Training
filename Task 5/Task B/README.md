# proxy-pqs

This is a basic demo of the proxy that has been developed by PQStation Pte Ltd.

The proxy file can be downloaded from `https://drive.google.com/file/d/1hC_U5bPJRACTpcLZj2Yz_1nhq-PBeWfR/view?usp=drive_link`

This is a docker image. After downloading, follow the steps below:

1. Run `docker image load -i proxy.tar` to load the docker image.

2. Run `docker run -it -p <run_port>:<run_port> proxy client <proxy_ip(ip of the proxy server)> <proxy_port(port of the proxy server)> <run_port>(port on which the client proxy will run)` for the proxy client.

For example, the client proxy is running locally on port 9000 and the server proxy is hosted on proxy.qstunnel.pqstation.com on port 443, then run `docker run -it -p 9000:9000 proxy client proxy.qstunnel.pqstation.com 443 9000`.

3. Run `curl -k https://localhost:9000` on another terminal. The webpage should be fetched.

4. Alternatively, one can also go for simply requesting the webpage from the browser by typing `https://localhost:9000` in the search bar. It might provide a prompt that the certificate is invalid, however, the request should go through once it's manually overridden.



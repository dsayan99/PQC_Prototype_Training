# proxy-pqs

This is a basic demo of the proxy that has been developed by PQStation Pte Ltd.

The proxy file can be downloaded from `https://drive.google.com/file/d/1kb4fJqf1ZLSbAOxDfCIV65tMy7LNgcDI/view?usp=sharing`

This is a docker image. After downloading, follow the steps below:

1. Run `docker image load -i proxy-1.tar` to load the docker image.

2. Run `docker run -it -p <run_port>:<run_port> proxy client <proxy_ip(ip of the proxy server)> <proxy_port(port of the proxy server)> <run_port>(port on which the client proxy will run)` for the proxy client.

For example if the client proxy is running locally on port 9000 and server proxy is also running locally on port 9002, then run `docker run -it -p 9000:9000 proxy client 192.168.0.105 9002 9000` where `192.168.0.105` is the local IP of the PC.

It is to be noted that if the proxy client and proxy server are running on different PCs within the same network subnet, then local IP of the server proxy PC will work, while if it's running with static IPs, then the IP of the proxy server needs to be fed in this.

3. Run `docker run -it -p <run_port>:<run_port> proxy server <server_ip>(ip of the server that ) <server_port>(port number of the original server) <run_port>(port on which the server will run)` for the proxy server.

For example if the server proxy is running locally on port 9002 and server is at 3.115.153.86:443, then run `docker run -it -p 9002:9002 proxy server 3.115.153.86 443 9002`.

4. Run the Client.py script `python3 Client.py` to fetch the key from the server through the proxies.



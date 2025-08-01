# How to Run this DEMO

## Step 0: Download the Docker Images

Please download the docker images `my-scg-app.tar`, `microservice1-pqs.tar`, `oqs-curl.tar` from `https://www.dropbox.com/scl/fo/jsyajieoc4336ty2x2uss/AEukQVwwuHUr9HLrf7Jc60c?rlkey=e6v9ncsu4qzm4zaytdftj2jiu&e=1&st=cwk1u73m&dl=0`.

## Step 1: Load Docker Images
docker load -i my-scg-app.tar
docker load -i microservice1-pqs.tar
docker load -i oqs-curl.tar

## Step 2: Start services
docker-compose up -d

## Step 3: Test commands
docker run --network=pqc-test -it oqs-curl curl -k -u p:p https://scg:8081/v1/hi --curves mlkem512

docker run --network=pqc-test -it oqs-curl curl -k -u p:p https://scg:8081/v2/ms1/hi/bye --curves mlkem512

docker run --network=pqc-test -it oqs-curl curl -k -u p:p https://scg:8081/v2/ms1/hello --curves mlkem512

In the above cmds p:p is the username and pwd for the SCG, hardcoded just for demo purposes, will not be used in production

## Step 4: Stop and remove the services
docker-compose down

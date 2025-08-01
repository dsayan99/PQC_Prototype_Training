# 🛡️ Apache with OpenSSL PQC + Test using oqs-curl

This setup demonstrates running an Apache server compiled with **OpenSSL 3.5.1 + Post-Quantum Cryptography (PQC)** support, and testing it using [`oqs-curl`](https://github.com/open-quantum-safe/oqs-curl) with hybrid PQC TLS.

---

## 📦 Prerequisites

- Docker installed (Docker Desktop or Engine)
- Apache image tarball: `apache-openssl-pqc.tar`
- `oqs-curl` image tarball: `oqs-curl.tar`
- Download the above images from `https://www.dropbox.com/scl/fo/jsyajieoc4336ty2x2uss/AEukQVwwuHUr9HLrf7Jc60c?rlkey=e6v9ncsu4qzm4zaytdftj2jiu&e=1&st=cwk1u73m&dl=0`.
- A local `conf/` directory containing:
  - `httpd.conf`
  - `extra/` directory with additional Apache config

---

## 🚀 Steps

### 1. Load Docker Images

docker load -i apache-openssl-pqc.tar
docker load -i oqs-curl.tar

### 2. Run Apache Server
docker run -d -v $(pwd)/conf:/usr/local/apache2/conf -p 8443:443 apache-openssl-pqc

### 3. Test command
docker run -it oqs-curl curl -k https://host.docker.internal:8443/ --curves mlkem512


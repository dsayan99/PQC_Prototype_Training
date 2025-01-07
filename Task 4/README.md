# A Short Demo of PQConnect Software that establishes a Quantum Safe tunnel between the client and server.

## Pre-requisite: The server must be configured with the PQConnect Server Software.

1. The PQConnect software team provides us with a test server that has PQConnect Server software configured, right now if we `curl https://www.pqconnect.net/test.html` we will see that it shows a message `Looks like you aren't connecting with PQConnect.`
2. Open a root shell using `sudo -i`
3. `cd /root`
4. `wget -m https://www.pqconnect.net/pqconnect-latest-version.txt`
5. `version=$(cat www.pqconnect.net/pqconnect-latest-version.txt)`
6. `wget -m https://www.pqconnect.net/pqconnect-$version.tar.gz`
7. `tar -xzf www.pqconnect.net/pqconnect-$version.tar.gz`
8. `cd pqconnect-$version`
9. `scripts/install-pqconnect`
10. `scripts/start-client-under-systemd`
11. Now when we `curl https://www.pqconnect.net/test.html`, it will show `Looks like you are connecting using PQConnect. Congratulations!`. This ensures successful installation of PQConnect.

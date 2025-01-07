curl https://www.pqconnect.net/test.html

sudo -i
cd /root
wget -m https://www.pqconnect.net/pqconnect-latest-version.txt
version=$(cat www.pqconnect.net/pqconnect-latest-version.txt)
wget -m https://www.pqconnect.net/pqconnect-$version.tar.gz
tar -xzf www.pqconnect.net/pqconnect-$version.tar.gz
cd pqconnect-$version
scripts/install-pqconnect
scripts/start-client-under-systemd

curl https://www.pqconnect.net/test.html

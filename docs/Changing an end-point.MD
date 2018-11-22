# Upgrading Primechain-API

Login to the server and execute the following commands:
```
sudo su apiuser
cd ~/primechain-api
pm2 stop 0
git pull
pm2 start 0
```

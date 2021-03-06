# 1. INSTALLATION OF OS
 Create droplet with 2 GB of memory at digital ocean, ubuntu 14.04x64 (other providers of virtual hosts should also be fine however you may need to install additional packages).
 Connect to it.
 
## 2. INSTALLATION OF SYSTEM PACKAGES
```bash
cd ~
locale-gen en_US en_US.UTF-8 
export LC_ALL="en_US.UTF-8"
apt-get update
apt-get install build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libgmp-dev git screen -y
```
## 3. GETTING AND COMPILING THE CODE
```bash
cd ~
git clone https://github.com/eagleflies/noblecoin
cd noblecoin/src
make -f makefile.unix -e USE_UPNP=-
strip noblecoind
./noblecoind  -addnode=104.236.195.137
```
You will get an error saying you need to create your noblecoin.conf file
```bash
vim /root/.noblecoinPOS/noblecoin.conf
```

If you have never used vim before type 'i' then paste the text below, then ':x' and hit Enter
```bash
rpcuser=noblecoinrpc
rpcpassword=some_random_password
```
Here we start screen session. noblecoin daemon will run within this session and you can close your ssh connection.
```bash
screen -S noble
./noblecoind  -addnode=104.236.195.137
```
Press 'Ctrl'+'a' then 'c' this will open another create within your screen session.
Now you can issue additional commands to your noble daemon
Start CPU mining
```bash
./noblecoind  setgenerate true 2
```
Get general information
```bash
./noblecoind  getinfo
```
Get mining info
```bash
./noblecoind  getmininginfo
```
Now you may check logs of daemon to see what it is doing. Open another screen''s tab and type
```bash
tail -f /root/.noblecoinPOS/debug.log
```

You can switch between screen's tabs using 'Ctrl+a', 'n' 
Good luck and have fun!

## 4. UPGRADING DAEMON (SOFT WAY)
If there were some changes you may need to upgrade the daemon.
```bash
./noblecoind  stop
git pull
make -f makefile.unix -e USE_UPNP=-
./noblecoind  -addnode=104.236.195.137
```
## 4.1 UPGRADING DAEMON V.2 (HARD WAY)
If procedure above did not work.
```bash
./noblecoind stop
cd ~
rm -rf noblecoin
rm -rf .noblecoinPOS
```

Proceed to section "3. GETTING AND COMPILING THE CODE"

## 4.2 UPGRADING DAEMON (MIDDLE WAY)
When blockchain needs to deleted.
```bash
./noblecoind  stop
rm -rf ~/.noblecoinPOS
cd ~/m-Noblecoin/src
git pull
make -f makefile.unix -e USE_UPNP=-
./noblecoind  -addnode=104.236.195.137
```

# INSTALLATION
#### Create droplet with 2 GB of memory at digital ocean, ubuntu 14.04x64 (other providers of virtual hosts
should also be fine however you may need to install additional packages).
#### Connect to it.

locale-gen en_US en_US.UTF-8 

apt-get update

apt-get install build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev git screen -y

apt-get autoremove

git clone https://github.com/eagleflies/m-Noblecoin

cd m-Noblecoin/src

make -f makefile.unix -e USE_UPNP=-

./noblecoind -testnet

#### You will get an error saying you need to create your noblecoin.conf file
vim /root/.noblecoin/noblecoin.conf

#### If you have never used vim before type 'i' then paste the text below, then ':x' and hit Enter
rpcuser=noblecoinrpc

rpcpassword=some_random_password

### Here we start screen session. noblecoin daemon will run within this session and you can close your ssh connection. 
screen -S noble

./noblecoind -testnet -addnode=104.236.70.124
### Press 'Ctrl'+'a' then 'c' this will open another create within your screen session.
### Now you can issue additional commands to your noble daemon
### Start CPU mining
./noblecoind -testnet setgenerate true 4

### Get general information
./noblecoind -testnet getinfo

### Get mining info
./noblecoind -testnet getmininginfo

### Now you may check logs of daemon to see what it is doing. Open another screen''s tab and type
tail -f /root/.noblecoin/testnet2/debug.log

### You can switch between screen's tab's using 'Ctrl+a', 'n' 

## Good luck and have fun!

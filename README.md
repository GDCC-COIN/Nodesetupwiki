# How you can setup a GDCC Node!

**## Requirements**
 **OS and Software**

 - OS: Ubutu 18.04 server and above
 -  Software: Geth

 1. Download the [geth](https://github.com/GDCC-COIN/gdcc-chain/releases/download/v1.0.0/gdcc-binary.zip) file.
2. Download [genesis.json](https://github.com/GDCC-COIN/Nodesetupwiki/blob/main/genesis.json). Initialize geth:
```
geth init genesis.json --datadir <Destination Folder>
```
3. Create GDCC.service
```
cd /lib/systemd/system
sudo touch gdcc.service
sudo nano gdcc.service
```

```
[Unit]
Description=GDCC Server
After=syslog.target network.target

[Service]
[Unit]
Description=GDCC
After=syslog.target network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/geth --nousb --datadir=<dir> --port 30312 --miner.gastarget 470000000000 --http --http.addr <Your IP> --http.port 7790 --http.api eth,net,web3,txpool --networkid 7777 --nodiscover  --allow-insecure-unlock  --http.corsdomain=* --http.vhosts=* --nat extip:<Your IP> --syncmode full --gcmode=archive
KillMode=process
KillSignal=SIGINT
TimeoutStopSec=90
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target
```

Replace <YOUR_IP>

This will run a full node, alongwith enabling HTTP and WS servers for that node, exposing the eth, net, web3, and txpool apis. If you require more configuration, kindly refer to the [geth documentation](https://geth.ethereum.org/docs/).

4. Run the service
```
sudo systemctl daemon-reload
sudo systemctl restart gdcc.service
sudo systemctl enable gdcc.service
sudo systemctl status gdcc.service
```

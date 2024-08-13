# Start sunrise testnet

1. Stop and reset chain data

```
# stop chain
sudo systemctl stop sunrised.service

# reset data
sunrised comet unsafe-reset-all

# remove old genesis.json
rm ~/.sunrise/config/genesis.json
```

2. Download and apply new genesis

```
# download genesis.json 
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-test-0.2/genesis.json

# check the sha256 hash of the genesis.json
sha256sum .sunrise/config/genesis.json
049ddb5d68ea22b979ed8b6429a6ec0618f80d653ceeea5cdc40faeb8034e8fc  .sunrise/config/genesis.json
```

3. Download new binary

```
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v0.1.4/sunrised
sudo mv sunrised /usr/bin
```

4. Update seed

Update seed information in config.toml as seeds.txt

```
# edit  .sunrise/config/config.toml
seeds = "0c0e0cf617c1c58297f53f3a82cea86a7c860396@a.sunrise-test-1.cauchye.net:26656,db223ecc4fba0e7135ba782c0fd710580c5213a6@a-node.sunrise-test-1.cauchye.net:26656,82bc2fdbfc735b1406b9da4181036ab9c44b63be@b-node.sunrise-test-1.cauchye.net:26656"
```


5. Restart chain

```
sudo systemctl start sunrised.service
```

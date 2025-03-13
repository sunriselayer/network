# Deprecated: `sunrise-test-0.1`

sunrise-test-0.1 is deprecated; This chain is not used in the public testnet.

## Start sunrise testnet sunrise-test-0.1

1. Stop and reset chain data

```bash
# stop chain
sudo systemctl stop cosmovisor
## If cosmovisor is not used
sudo systemctl stop sunrised

# reset data
sunrised comet unsafe-reset-all

# remove old genesis.json
rm ~/.sunrise/config/genesis.json
```

1. Download and apply new genesis

```bash
# download genesis.json 
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-test-0.1/genesis.json

# check the sha256 hash of the genesis.json
sha256sum .sunrise/config/genesis.json
0249de5c02d7c4791fb14aae556240cfa2acca9549e9217f14d12795e5d480e3  .sunrise/config/genesis.json
```

1. Download new binary

```bash
# download new binary for intel
wget https://github.com/sunriselayer/sunrise/releases/download/v0.1.2/sunrised
sudo mv sunrised /usr/bin
```

1. Update seed

Update seed information in config.toml as seeds.txt

```yml
# edit  .sunrise/config/config.toml
seeds = "27d92a62f64585b995a6a99882cdd3a1a441336d@a.sunrise-test-1.cauchye.net:26656,9cb96bd137c6fab41446f5fa36e17b1f8896b05c@b.sunrise-test-1.cauchye.net:26656,db223ecc4fba0e7135ba782c0fd710580c5213a6@a-node.sunrise-test-1.cauchye.net:26656"
```

1. Restart chain

```bash
sudo systemctl stop cosmovisor
## If cosmovisor is not used
sudo systemctl stop sunrised
```

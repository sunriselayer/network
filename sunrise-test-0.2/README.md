# Start sunrise testnet sunrise-test-0.2

`sunrise-test-0.2` is a hard fork on sunrise testnet. This section describes the steps for existing full nodes and validators to support it.

When setting up a new full node or validator, please follow the guide in [Sunrise doc](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus).

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
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-test-0.2/genesis.json

# check the sha256 hash of the genesis.json
sha256sum ~/.sunrise/config/genesis.json
049ddb5d68ea22b979ed8b6429a6ec0618f80d653ceeea5cdc40faeb8034e8fc  .sunrise/config/genesis.json
```

1. Download new binary

sunrise-test-0.2 uses the sunrise-v0.1.4 binary.

```bash
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v0.1.4/sunrised
sha256sum sunrised
e9abb0bdfb642faae350b47f62fd0c3a54f4ceabb6614f34322133784a0e600a  sunrised

sudo mv sunrised /usr/bin/
## or cosmovisor
sudo mv sunrised ~/.sunrise/cosmovisor/genesis/bin/
```

1. Set seed

Update seeds information in config.toml as seeds.txt

The seeds provides a list of other validators that a newly joining validator should initially connect to.
Once a validator connects to the network, it primarily relies on `persistent_peers` for connections, reducing the importance of `seeds`.

```yml
# edit  .sunrise/config/config.toml
seeds = "0c0e0cf617c1c58297f53f3a82cea86a7c860396@a.sunrise-test-1.cauchye.net:26656"
```

1. Set persistent peers

Update persistent peers information in config.toml as peers.txt

This is a list of trusted validators that the validator should maintain connections with at all times.
Connections to validators listed in persistent_peers are prioritized to maintain network stability.

```yml
# edit  .sunrise/config/config.toml
seeds = "0c0e0cf617c1c58297f53f3a82cea86a7c860396@a.sunrise-test-1.cauchye.net:26656,db223ecc4fba0e7135ba782c0fd710580c5213a6@a-node.sunrise-test-1.cauchye.net:26656,82bc2fdbfc735b1406b9da4181036ab9c44b63be@b-node.sunrise-test-1.cauchye.net:26656,18b9bc3dccfd64dc39459fbac52f7ae7809fd697@c-node.sunrise-test-1.cauchye.net:26656,66d225bb1225c66a8d0ce2f52369a8ba06ebddfc@d-node.sunrise-test-1.cauchye.net:26656"

1. Restart chain

```bash
sudo systemctl start cosmovisor
## If cosmovisor is not used
sudo systemctl start sunrised.service
```

# `sunrise-test-da-2`

sunrise-test-da-2 started on March 13, 2025.

## Start sunrise testnet sunrise-test-da-2

`sunrise-test-da-2` is a sunrise devnet for testing DA functions. This section describes the steps for existing full nodes and validators to support it.

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
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-test-da-2/genesis.json

# check the sha256 hash of the genesis.json
sha256sum ~/.sunrise/config/genesis.json
20b2ab8102b62fea6c668b89521545011fe3d8bc5cb2a08e413fc80c3b0be1f1  .sunrise/config/genesis.json
```

1. Download binary

sunrise-test-da-2 uses the sunrise-v0.4.3 binary.

```bash
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v0.4.3/sunrised
md5sum sunrised
37cb2b1f23b1f5ae7a3924d7dff2b349 sunrised

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
seeds = "b94c27f9718b70d8d4b6ec13df537c282501e8fc@sunrise-test-da-2.cauchye.net:26656"
```

1. Set persistent peers

Update persistent peers information in config.toml as peers.txt

This is a list of trusted validators that the validator should maintain connections with at all times.
Connections to validators listed in persistent_peers are prioritized to maintain network stability.

```yml
# edit  .sunrise/config/config.toml
persistent_peers = "b94c27f9718b70d8d4b6ec13df537c282501e8fc@sunrise-test-da-2.cauchye.net:26656"
```

1. Restart chain

```bash
sudo systemctl start cosmovisor
## If cosmovisor is not used
sudo systemctl start sunrised.service
```

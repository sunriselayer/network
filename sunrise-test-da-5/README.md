# `sunrise-test-da-5`

sunrise-test-da-5 started on Jul 14, 2025.

## Start sunrise testnet sunrise-test-da-5

`sunrise-test-da-5` is a sunrise devnet for testing DA functions and other features. This section describes the steps for existing full nodes and validators to support it.

When setting up a new full node or validator, please follow the guide in [Sunrise doc](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus).
We recommend to use [Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor).

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
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-test-da-5/genesis.json

# check the sha256 hash of the genesis.json
md5sum ~/.sunrise/config/genesis.json
fd912c88c3b5056dbaf1c5538fcc2210 .sunrise/config/genesis.json
```

1. Create binary

sunrise-test-da-4 uses the sunrise-v0.7.1 binary.

```bash
git clone https://github.com/sunriselayer/sunrise.git
git checkout v0.7.1
make install # required go v1.24.2
cp ~/go/bin/sunrised ~/.sunrise/cosmovisor/genesis/bin
```

or download

```bash
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v0.7.1/sunrised
md5sum sunrised
a2dcc3124a9ad7e856b3a724ea64175b sunrised

sudo mv sunrised ~/.sunrise/cosmovisor/genesis/bin/
sudo mv sunrised /usr/bin/
```

1. Set seed

Update seeds information in config.toml as seeds.txt

The seeds provides a list of other validators that a newly joining validator should initially connect to.
Once a validator connects to the network, it primarily relies on `persistent_peers` for connections, reducing the importance of `seeds`.

```yml
# edit  .sunrise/config/config.toml
seeds = "35de66949e50e444d2788733ec8e07f1253922d1@sunrise-test-da-5.cauchye.net:26656"
```

1. Set persistent peers

Update persistent peers information in config.toml as peers.txt

This is a list of trusted validators that the validator should maintain connections with at all times.
Connections to validators listed in persistent_peers are prioritized to maintain network stability.

```yml
# edit  .sunrise/config/config.toml
persistent_peers = "35de66949e50e444d2788733ec8e07f1253922d1@sunrise-test-da-5.cauchye.net:26656"
```

1. Restart chain

```bash
sudo systemctl start cosmovisor
```

# `sunrise-test-da-4`

sunrise-test-da-4 started on Jun 12, 2025.

## Start sunrise testnet sunrise-test-da-4

`sunrise-test-da-4` is a sunrise devnet for testing DA functions and other features. This section describes the steps for existing full nodes and validators to support it.

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
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-test-da-4/genesis.json

# check the sha256 hash of the genesis.json
md5sum ~/.sunrise/config/genesis.json
6dac65c47cb4a0ad1ad221f135a20bf0 .sunrise/config/genesis.json
```

1. Create binary

sunrise-test-da-4 uses the sunrise-v0.6.0 binary.

```bash
git clone https://github.com/sunriselayer/sunrise.git
git checkout v0.6.0
make install # required go v1.24.2
cp ~/go/bin/sunrised ~/.sunrise/cosmovisor/genesis/bin
```

or download

```bash
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v0.6.0/sunrised
md5sum sunrised
774e53297aa5d004dcefd0173c3bfdb4 sunrised

sudo mv sunrised ~/.sunrise/cosmovisor/genesis/bin/
sudo mv sunrised /usr/bin/
```

1. Set seed

Update seeds information in config.toml as seeds.txt

The seeds provides a list of other validators that a newly joining validator should initially connect to.
Once a validator connects to the network, it primarily relies on `persistent_peers` for connections, reducing the importance of `seeds`.

```yml
# edit  .sunrise/config/config.toml
seeds = "e39aeab6182eda29b48effcf73d46677f595867c@sunrise-test-da-4.cauchye.net:26656"
```

1. Set persistent peers

Update persistent peers information in config.toml as peers.txt

This is a list of trusted validators that the validator should maintain connections with at all times.
Connections to validators listed in persistent_peers are prioritized to maintain network stability.

```yml
# edit  .sunrise/config/config.toml
persistent_peers = "e39aeab6182eda29b48effcf73d46677f595867c@sunrise-test-da-4.cauchye.net:26656"
```

1. Restart chain

```bash
sudo systemctl start cosmovisor
```

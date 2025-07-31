# `dawn-1` Testnet

dawn-1 started on Jul 31, 2025.

## Start dawn-1 testnet

`dawn-1` is a sunrise testnet. This section describes the steps for existing full nodes and validators to support it.

If you are a new validator, please see <https://docs.sunriselayer.io/build/validators>.
If simply creating a full node, please see <https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus/full-consensus-node>.

We recommend to use [Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor) to manage the binary.

## Start a full node

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
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/dawn-1/genesis.json
```

1. Create binary

`dawn-1` uses the `sunrised v1.0.0` binary at the genesis.
<https://github.com/sunriselayer/sunrise/releases/tag/v1.0.0>

```bash
git clone https://github.com/sunriselayer/sunrise.git
git checkout v1.0.0
make install # required go v1.24.2
cp ~/go/bin/sunrised ~/.sunrise/cosmovisor/genesis/bin
```

or download

```bash
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v1.0.0/sunrised-linux-amd64

sudo mv sunrised ~/.sunrise/cosmovisor/genesis/bin/
sudo mv sunrised /usr/bin/
```

1. Set seed

Update seeds information in config.toml as seeds.txt

The seeds provides a list of other validators that a newly joining validator should initially connect to.
Once a validator connects to the network, it primarily relies on `persistent_peers` for connections, reducing the importance of `seeds`.

```yml
# edit  .sunrise/config/config.toml
seeds = "b9488ee1f338aae256a3db0ca02e41cc349373db@35.75.8.125:26656"
```

1. Set persistent peers

Update persistent peers information in config.toml as peers.txt

This is a list of trusted validators that the validator should maintain connections with at all times.
Connections to validators listed in persistent_peers are prioritized to maintain network stability.

```yml
# edit  .sunrise/config/config.toml
persistent_peers = "b9488ee1f338aae256a3db0ca02e41cc349373db@35.75.8.125:26656"
```

1. Restart chain

```bash
sudo systemctl start cosmovisor
```

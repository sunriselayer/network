# `sunrise-1` Mainnet

sunrise-1 will be started on Aug 4th, 2025.

## Genesis File

> [!IMPORTANT]
>
> The `genesis.json` located in the `sunrise-1/gentx` directory is **exclusively for creating `gentx` (genesis transactions)**.
>
> For the actual mainnet launch, you **MUST** use the `genesis.json` file located in this `sunrise-1` directory.
>
> Validators who have created a `gentx` **MUST** replace their `config/genesis.json` with the official `genesis.json` from this `sunrise-1` directory.

## Start `sunrise-1` mainnet

This section describes the steps for existing full nodes and validators to support `sunrise-1`.

If you are a new validator, please see <https://docs.sunriselayer.io/build/validators>.
If simply creating a full node, please see <https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus/full-consensus-node>.

We recommend to use [Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor) to manage the binary.

### 1. Stop and reset chain data

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

### 2. Download and apply new genesis

```bash
# download genesis.json
wget -O ~/.sunrise/config/genesis.json https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/genesis.json
# check md5sum
md5sum ~/.sunrise/config/genesis.json
# result: 83023c0bce23b4a28eb21f66753f5f3a genesis.json
```

### 3. Create binary

`sunrise-1` uses the `sunrised v1.0.0` binary at the genesis.
<https://github.com/sunriselayer/sunrise/releases/tag/v1.0.0>

```bash
git clone https://github.com/sunriselayer/sunrise.git
cd sunrise
git checkout v1.0.0
make install # required go v1.24.2
cp ~/go/bin/sunrised ~/.sunrise/cosmovisor/genesis/bin
cd ..
```

or download

```bash
# download new binary for x86
wget https://github.com/sunriselayer/sunrise/releases/download/v1.0.0/sunrised-linux-amd64

mv sunrised-linux-amd64 sunrised
chmod +x sunrised
sudo mv sunrised ~/.sunrise/cosmovisor/genesis/bin/
# or
sudo mv sunrised /usr/local/bin/
```

### 4. Set seed

Update seeds information in `config.toml`.

```yml
# edit  ~/.sunrise/config/config.toml
seeds = ""
```

### 5. Set persistent peers

Update persistent peers information in `config.toml`.

```yml
# edit  ~/.sunrise/config/config.toml
persistent_peers = ""
```

### 6. Restart chain

```bash
sudo systemctl start cosmovisor
```

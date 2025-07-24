# How to create a gentx

This document describes how to create a gentx (genesis transaction).

## Command

```bash
sunrised genesis gentx [validator-key-name] [amount] --home [path-to-home-directory] --chain-id [chain-id] --moniker [your-moniker] --details "[your-details]" --website [your-website]
```

## Parameters

| Parameter              | Description                                                                | Example                   |
| ---------------------- | -------------------------------------------------------------------------- | ------------------------- |
| `[validator-key-name]` | The name of the validator key.                                             | `$VAL1`                   |
| `[amount]`             | The amount of tokens to stake.                                             | `1000000uvrise`           |
| `--home`               | The path to the home directory of the node.                                | `$NODE_HOME`              |
| `--chain-id`           | The chain ID.                                                              | `sunrise-1`               |
| `--moniker`            | The moniker of the node. This is a human-readable name for your validator. | `sunrise-dev`             |
| `--details`            | A description of your validator.                                           | `"sample for gentx"`      |
| `--website`            | The website of your validator.                                             | `https://sunriselayer.io` |

## Example

Here is an example of the command.

```bash
sunrised genesis gentx $VAL 1000000uvrise --home $NODE_HOME --chain-id sunrise-1 --moniker sunrise-dev --details "sample for gentx" --website https://sunriselayer.io
```

## Success Response

If the command is successful, you will see a response like this:

```
Genesis transaction written to "sunrise/config/gentx/gentx-baee32256a6b9d95b00664689f067454fe0b07be.json"
```

# Data Backup

## Backup Keys[​](https://wiki.findora.org/docs/validators/node-backup#backup-keys) <a href="#backup-keys" id="backup-keys"></a>

First, you need to locate the data path of your node. It is `/data/findora/mainnet` or `/data/findora/testnet`, if the node is setup by the auto script.

```bash
export ROOT_DIR=< The data path of your node >
```

Second, please backup the two keys listed below for your validator node. You will need these keys to perform tasks such as moving your validator node to another host machine (e.g. when wanting to upgrade your server hardware).

#### Validator Key

```bash
${ROOT_DIR}/tendermint/config/priv_validator_key.json
```

This key manages the FRA tokens staked on the validator. Make sure you have the same validator address after the transfer. When upgrading your node hardware, place this file in the same directory structure on your new server.

#### Wallet Key

```bash
${ROOT_DIR}/node.mnemonic
```

This key controls the validator’s wallet. When recovering the node on a new server, you should skip the `fn genkey` for generating a new key. Instead, place this file in the same directory structure on your new server when upgrading your node hardware.

## Backup Critical Data[​](https://wiki.findora.org/docs/validators/node-backup#backup-critical-data) <a href="#backup-critical-data" id="backup-critical-data"></a>

Last, please back the following directory which stores critical data

```bash
${ROOT_DIR}/tendermint/config
```

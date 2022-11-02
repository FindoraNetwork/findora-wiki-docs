# Node Backup Guide

### Backup Keys[​](https://wiki.findora.org/docs/validators/node-backup#backup-keys) <a href="#backup-keys" id="backup-keys"></a>

First, you need to locate the data path of your node. It is `/data/findora/mainnet` or `/data/findora/testnet`, if the node is setup by the auto script.

```bash
export ROOT_DIR=< The data path of your node >
```

Second, please backup the two keys listed below for your validator node. You will need these keys to perform tasks such as moving your validator node to another host machine (such as when you want to upgrade your server hardware).

1. The Validator Key

```bash
${ROOT_DIR}/tendermint/config/priv_validator_key.json
```

This key manages the FRA tokens staked on the validator. Make sure you have the same validator address after transfer. Place this file in the same directory structure on your new server when upgrading your node hardware.

1. The wallet key

```bash
${ROOT_DIR}/node.mnemonic
```

This key controls the validator’s wallet. When recovering the node on a new server, you shoould skip the `fn genkey` for generating a new key. Instead, place this file in the same directory structure on your new server when upgrading your node hardware.

### Backup Critical Data[​](https://wiki.findora.org/docs/validators/node-backup#backup-critical-data) <a href="#backup-critical-data" id="backup-critical-data"></a>

Last, please back the following directory which stores critical data

```bash
${ROOT_DIR}/tendermint/config
```

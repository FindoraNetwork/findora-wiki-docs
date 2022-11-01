---
description: >-
  Ganache is a personal blockchain for rapid EVM distributed application
  development.
---

# Ganache

<figure><img src="../../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

Install Ganache CLI

```bash
npm install -g ganache-cli
```

Load Findora networks (local, testnet, mainnet) to ganache-cli

```bash
# Local
ganache-cli -f http://localhost:8545 --networkId 2152

# Testnet
ganache-cli -f https://prod-testnet.prod.findora.org:8545 --networkId 2153

# Mainnet
ganache-cli -f https://rpc-mainnet.findora.org --networkId 2152
```

Use web3.js to interact with the ganache-bound Findora network

```javascript
const web3 = new Web3("http://127.0.0.1:8545");
web3.eth.getBlockNumber().then(console.log)
```

---
description: The Findora Smart Chain is the EVM-compatible layer of Findora blockchain.
---

# EVM Smart Chain

The Findora Smart Chain is the EVM-compatible layer of Findora blockchain (and can connect with the UTXO-based layer of Findora via the Prism feature). With the power of Findora’s EVM, developers have access to building fully compatible EVM apps with Solidity, Web3 tools like Metamask, Truffle, Remix and all Ethereum’s token specifications (e.g. ERC-20, ERC-721, etc.) while they leverage the privacy that Findora offers. The marriage between Findora’s EVM and UTXO models into a single multi-chain architecture ensures that they share the same consensus and storage layer, and even better, all incompatibility between address types are solved through a new atomic transfer model called Prism. This allows users to own and control various assets on Findora with versatile approaches for programmable privacy.

The Findora EVM guides below will walk developers through setting up Findora EVM integration tools, deploying a Findora smart contract and launching FRC-20 tokens on Findora EVM.

Developers who deploy Ethereum's ERC-20 Solidity boilerplate code on the Findora EVM will, in effect, be creating FRC-20 tokens, which are Findora's version of ERC-20 tokens.

#### Setting Up Findora Testnet[​](https://wiki.findora.org/docs/modules/findora-evm/overview#setting-up-findora-testnet) <a href="#setting-up-findora-testnet" id="setting-up-findora-testnet"></a>

Currently, developing on Findora EVM requires developers to connect to the Findora Anvil Testnet.

See the [Networks](../network-settings/network-settings.md) guide for details.

#### Writing and Deploying a Contract[​](https://wiki.findora.org/docs/modules/findora-evm/overview#writing-and-deploying-a-contract) <a href="#writing-and-deploying-a-contract" id="writing-and-deploying-a-contract"></a>

All the best tools available for deploying on Ethereum work just as well here with no hitches and Findora EVM supports most of them.

Hardhat is an Ethereum development environment that helps developers manage and automate repetitive tasks for smart contract and DApp development. Truffle is like Hardhat but on steroids. Leveraging Ganache, its local Ethereum blockchain for testing contracts, Truffle allows you to develop dApps with scriptable migration and deployment, network management, an interactive console, smart contract management and even some automated contract testing.

Please look at the [Truffle](../developers/evm-tools-and-tutorials/contract-deployment/truffle.md), [Hardhat](../developers/evm-tools-and-tutorials/contract-deployment/hardhat.md), [Remix IDE](../developers/evm-tools-and-tutorials/contract-deployment/remix.md) guides for details.

#### Testing and Automation[​](https://wiki.findora.org/docs/modules/findora-evm/overview#testing-and-automation) <a href="#testing-and-automation" id="testing-and-automation"></a>

Waffle is a library for compiling and testing smart contracts and Mars is a deployment manager. Waffle and Mars can be used together to write, compile, test, and deploy Ethereum smart contracts.

See the [Waffle & Mars](../developers/evm-tools-and-tutorials/contract-deployment/waffle.md) guide for details.

#### Other Tools and Integrations[​](https://wiki.findora.org/docs/modules/findora-evm/overview#other-tools-and-integrations) <a href="#other-tools-and-integrations" id="other-tools-and-integrations"></a>

* [Web3.js](https://web3js.readthedocs.io/) is a set of libraries that allow developers to interact with Ethereum nodes using HTTP, IPC, or WebSocket protocols with JavaScript. Findora has an Ethereum-like API which is fully compatible with Ethereum-style JSON RPC invocations. Developers can use the web3.js library to interact with a Findora EVM node using the same process as with Ethereum.
* [Ethers.js](https://docs.ethers.io/v5/) is a set of tools to interact with Ethereum nodes using Javascript. Findora has an Ethereum-like API which is fully compatible with Ethereum-style JSON RPC invocations. Developers can use the Ethers.js library to interact with a Findora EVM node using the same process as with Ethereum.
* [Web3.py](https://web3py.readthedocs.io/) is a set of libraries that allow developers to interact with Ethereum nodes using HTTP, IPC, or WebSocket protocols with Python. Findora has an Ethereum-like API which is fully compatible with Ethereum-style JSON RPC invocations. Developers can use the Web3.py library to interact with a Findora EVM node using the same process as with Ethereum.
* [The Graph](https://thegraph.com/docs/about/introduction#what-the-graph-is) is an indexing protocol that organizes information so that applications can access data very efficiently -- similar to how Google indexes the entire internet to rapidly deliver information for user searches. The graph can be used to build indexes for rapid querying of blockchain network like Ethereum -- allowing Dapps to quickly access blockchain data.

#### Blockchain Bridge[​](https://wiki.findora.org/docs/modules/findora-evm/overview#blockchain-bridge) <a href="#blockchain-bridge" id="blockchain-bridge"></a>

For developers who wish to move tokens from other Layer 1 blockchains, the Findora EVM network will support an open source multi-directional bridge(a fork of [ChainSafe ChainBridge](https://github.com/ChainSafe/ChainBridge)) , called [Rialto bridge](broken-reference).

We have deployed a testnet version of Rialto on our Anvil testnet enabling a Binance Smart Chain Testnet BEP-20 token to be moved to the Findora EVM Devnet as a FRC-20 token.

See our home grown [Rialto bridge](broken-reference) and its guide for details.

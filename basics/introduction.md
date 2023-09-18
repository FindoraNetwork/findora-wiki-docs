# Architecture

Findora is an open, permissionless L1 blockchain featuring a selectively transparent ledger made possible through zero-knowledge cryptography. The blockchain is secured by a decentralized network of global validators running the Tendermint consensus mechanism.

With Findora, developers can create digital assets, applications and smart contracts which can preserve confidential information on-chain. Findora supports zero-knowledge proof cryptography and multi-party computation technologies to enable developers to build zk dApps or integrate zk into their own projects.

In addition to building your own zk applications, Findora’s primitives can be used to create selective transparency on other EVM-compatible L1 chains.

#### What is Selective Transparency? Why Findora?[​](https://wiki.findora.org/docs/findora\_basics/introduction#why-privacy-and-why-findora) <a href="#why-privacy-and-why-findora" id="why-privacy-and-why-findora"></a>

Bitcoin and Ethereum were hugely innovative, applying blockchain technology in novel ways. However, because they both use open and fully transparent ledgers, they publicly broadcast all transaction data when users interact on the chain. Findora is again pushing the boundaries of blockchain technology by introducing the concept of "zk-ledgers." A zkLedger introduces selective transparency to blockchain and will give users and projects more control over what data is visible on-chain.&#x20;

In the world of traditional finance, a fully transparent ledger can be a huge liability. They aren't suitable for many business applications like payroll, IP data, market trading, or any industry with consumer protection laws. Selective transparency makes blockchains, including Ethereum, much more suitable for mainstream adoption.&#x20;

Even in Web3, fully open ledgers have proven to be a limiting factor. For example, on-chain transparency on decentralized exchanges has led to front-running, causing millions of losses for traders. Open ledgers contribute to the vulnerability of Web3 bridges and prevent many different types of games from being built on-chain.&#x20;

Findora’s blockchain technology solves many of these confidentiality-related issues through zero-knowledge cryptography, as Findora was built from the ground up to confidentially compute, transact and store data. Findora offers a suite of SDKs which allow EVM developers to export this paradigm shift to their own ecosystems.

#### Architecture and Key Components <a href="#architecture-and-key-components" id="architecture-and-key-components"></a>

<figure><img src="../.gitbook/assets/image (11) (3).png" alt=""><figcaption><p>Architectural Overview</p></figcaption></figure>

Findora consists of the following key modules:

* UTXO Chain
* EVM Chain
* Cryptography Library (zkSNARK, Bulletproofs, etc.)
* Prism Transfers
* Staking (Tendermint-based Consensus and PoS)

See the `Modules` section of our documentation for the details of each module.

#### Dual-chain Architecture (UTXO and EVM) and Prism++ Transfer[​](https://wiki.findora.org/docs/findora\_basics/introduction#dual-blockchain-architecture-utxo-and-evm-and-prism-transfer) <a href="#dual-blockchain-architecture-utxo-and-evm-and-prism-transfer" id="dual-blockchain-architecture-utxo-and-evm-and-prism-transfer"></a>

A key concept to understand about Findora is that it is composed of two different ledgers (or layers) combined into a single “multi-chain” model. These two ledgers include:

* Findora UTXO Chain - a UTXO-based blockchain
* Findora EVM Chain - an accounts-based blockchain

The _**Prism++**_ transfer feature is what enables users to bridge (aka transfer) assets from Findora UTXO Chain to Findora EVM Chain -- and vice versa.

#### Key Platform Primitives and Developer Tools[​](https://wiki.findora.org/docs/findora\_basics/introduction#key-platform-primitives-and-developer-tools) <a href="#key-platform-primitives-and-developer-tools" id="key-platform-primitives-and-developer-tools"></a>

* **Key Primitives:**
  * Send confidential transfers (hide amount sent, hide asset type sent, etc.)
  * Create tokens
    * UTXO tokens
    * EVM-compatible tokens
  * Deploy EVM-compatible smart contracts
  * Call JSON-RPC methods (all industry-wide EVM methods)
  * Build Zk-Proof Circuits
    * zkSNARK circuits
    * Bulletproofs circuits
* **Key Developer Tools:**
  * UTXO Tools
    * CLI/SDKs to send confidential transfers, create custom tokens, create wallets, delegate tokens for PoS rewards
  * EVM Tools
    * All EVM tools are compatible with Findora (Metamask, Remix, Hardhat, etc.)

#### Findora Ecosystem[​](https://wiki.findora.org/docs/findora\_basics/introduction#findora-ecosystem) <a href="#findora-ecosystem" id="findora-ecosystem"></a>

Finally, to support Findora's ecosystem user growth and total value locked (TVL), key dApps launched on mainnet include:

* [Rialto Bridge](https://rialtobridge.io/) - cross-chain bridge enabling users to move assets from EVM-compatible blockchains to Findora blockchain.
* [Sonic Swap](https://sonicswap.io/exchange/swap) - a third party DEX bringing DeFi to Findora.
* [Lumias](https://www.lumias.io/) - an ambitious project pioneering zk in Web3 gaming.

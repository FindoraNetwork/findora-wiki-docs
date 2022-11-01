# Network Settings

Findora's **Smart Chain** is an EVM-compatible chain that can run all solidity code and can use existing EVM tools while **Native Chain** is a UTXO-based chain with native support for confidential transfers. Both Smart and Native Chain are part of Findora and operate under one consensus.

To connect to the Findora network, use the configuration settings below. Be sure to use the configuration info for the correct chain (Smart Chain or Native Chain) you wish to connect to.

These network settings are commonly used when configuring Metmask, Findora wallet, smart contract files, etc.

#### Smart Chain (EVM)

|          |                Mainnet               |                Anvil Testnet               |               Forge Testnet              |
| -------- | :----------------------------------: | :----------------------------------------: | :--------------------------------------: |
| RPC      | https://rpc-mainnet.findora.org:8545 | https://prod-testnet.prod.findora.org:8545 | https://prod-forge.prod.findora.org:8545 |
| Chain ID |                 2152                 |                    2153                    |                   2154                   |
| Explorer |      https://evm.findorascan.io      |  https://testnet-anvil.evm.findorascan.io  | https://testnet-forge.evm.findorascan.io |

#### Native Chain (UTXO)

|          |                Mainnet                |             Anvil Testnet             |               Forge Testnet              |
| -------- | :-----------------------------------: | :-----------------------------------: | :--------------------------------------: |
| Node     | https://prod-mainnet.prod.findora.org | https://prod-testnet.prod.findora.org |    https://prod-forge.prod.findora.org   |
| Explorer |         https://findorascan.io        |  https://prod-testnet.findorascan.io  | https://testnet-forge.evm.findorascan.io |

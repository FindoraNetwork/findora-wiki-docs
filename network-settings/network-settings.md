# Network Settings

Findora's **Smart Chain** is an EVM-compatible chain that can run all solidity code and can use existing EVM tools while **Native Chain** is a UTXO-based chain with native support for confidential transfers. Both Smart and Native Chain are part of Findora and operate under one consensus.

To connect to the Findora network, use the configuration settings below. Be sure to use the configuration info for the correct chain (Smart Chain or Native Chain) you wish to connect to.

These network settings are commonly used when configuring Metmask, Findora wallet, smart contract files, etc.

#### Smart Chain (EVM)

<table><thead><tr><th width="112.33333333333331"> </th><th width="197" align="center">Mainnet</th><th align="center">Anvil Testnet</th><th width="205.66666666666669" align="center">Forge Testnet</th></tr></thead><tbody><tr><td>RPC</td><td align="center">https://rpc-mainnet.findora.org</td><td align="center">https://prod-testnet.prod.findora.org:8545</td><td align="center">https://prod-forge.prod.findora.org:8545</td></tr><tr><td>Archive</td><td align="center">https://archive.prod.findora.org:8545</td><td align="center">N/A</td><td align="center">N/A</td></tr><tr><td>Chain ID</td><td align="center">2152</td><td align="center">2153</td><td align="center">2154</td></tr><tr><td>Explorer</td><td align="center">https://evm.findorascan.io</td><td align="center">https://testnet-anvil.evm.findorascan.io</td><td align="center">https://testnet-forge.evm.findorascan.io</td></tr></tbody></table>

#### Native Chain (UTXO)

<table><thead><tr><th width="113"> </th><th width="198" align="center">Mainnet</th><th width="222.66666666666666" align="center">Anvil Testnet</th><th width="206.33333333333337" align="center">Forge Testnet</th></tr></thead><tbody><tr><td>Node</td><td align="center">https://prod-mainnet.prod.findora.org</td><td align="center">https://prod-testnet.prod.findora.org</td><td align="center">https://prod-forge.prod.findora.org</td></tr><tr><td>Explorer</td><td align="center">https://findorascan.io</td><td align="center">https://prod-testnet.findorascan.io</td><td align="center">https://testnet-forge.evm.findorascan.io</td></tr></tbody></table>

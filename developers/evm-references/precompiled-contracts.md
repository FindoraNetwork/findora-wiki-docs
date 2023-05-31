# Precompiled Contracts

### Introduction[​](https://wiki.findora.org/docs/developers/evm\_smart\_chain/precompile#introduction) <a href="#introduction" id="introduction"></a>

Similar to Ethereum, in addition to standard opcodes, the EVM offers more advanced functionalities in the form of precompiled smart contracts. These contracts are bundled with the EVM at fixed addresses and can be called like a standard contract.

### Precompiled Contracts[​](https://wiki.findora.org/docs/developers/evm\_smart\_chain/precompile#precompiled-contracts-1) <a href="#precompiled-contracts-1" id="precompiled-contracts-1"></a>

<table><thead><tr><th>Address</th><th width="120">Name</th><th>Features</th></tr></thead><tbody><tr><td>0x0000000000000000000000000000000000000001</td><td>ECRecover</td><td>ECDSA public key recovery</td></tr><tr><td>0x0000000000000000000000000000000000000002</td><td>SHA256</td><td>SHA-2 256-bit hash function</td></tr><tr><td>0x0000000000000000000000000000000000000003</td><td>RIPEMD160</td><td>RIPEMD 160-bit hash function</td></tr><tr><td>0x0000000000000000000000000000000000000004</td><td>Identity</td><td>Identity function</td></tr><tr><td>0x0000000000000000000000000000000000000005</td><td>ModExp</td><td>Big integer modular exponentiation</td></tr><tr><td>0x0000000000000000000000000000000000000006</td><td>BN128Add</td><td>Elliptic curve addition</td></tr><tr><td>0x0000000000000000000000000000000000000007</td><td>BN128Mul</td><td>Elliptic curve scalar multiplication</td></tr><tr><td>0x0000000000000000000000000000000000000008</td><td>BN128Pair</td><td>Elliptic curve pairing check</td></tr><tr><td>0x0000000000000000000000000000000000001000</td><td>FRA (FRC20)</td><td>Implement native token FRA to support IERC20 interface</td></tr></tbody></table>

### FRC20-FRA precompile contract[​](https://wiki.findora.org/docs/developers/evm\_smart\_chain/precompile#frc20-fra-precompile-contract) <a href="#frc20-fra-precompile-contract" id="frc20-fra-precompile-contract"></a>

We have an ERC20 interface compatible implemenation of FRA. We can interact with this address within ERC20 interface to control your evm FRA as if it's an FRC20 token.

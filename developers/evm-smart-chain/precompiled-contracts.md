# Precompiled Contracts

### Introduction[​](https://wiki.findora.org/docs/developers/evm\_smart\_chain/precompile#introduction) <a href="#introduction" id="introduction"></a>

Similar to Ethereum, in addition to standard opcodes, the EVM offers more advanced functionalities in the form of precompiled smart contracts. These contracts are bundled with the EVM at fixed addresses and can be called like a standard contract.

### Precompiled Contracts[​](https://wiki.findora.org/docs/developers/evm\_smart\_chain/precompile#precompiled-contracts-1) <a href="#precompiled-contracts-1" id="precompiled-contracts-1"></a>

| Address                                    | Name        | Features                                               |
| ------------------------------------------ | ----------- | ------------------------------------------------------ |
| 0x0000000000000000000000000000000000000001 | ECRecover   | ECDSA public key recovery                              |
| 0x0000000000000000000000000000000000000002 | SHA256      | SHA-2 256-bit hash function                            |
| 0x0000000000000000000000000000000000000003 | RIPEMD160   | RIPEMD 160-bit hash function                           |
| 0x0000000000000000000000000000000000000004 | Identity    | Identity function                                      |
| 0x0000000000000000000000000000000000000005 | ModExp      | Big integer modular exponentiation                     |
| 0x0000000000000000000000000000000000000006 | BN128Add    | Elliptic curve addition                                |
| 0x0000000000000000000000000000000000000007 | BN128Mul    | Elliptic curve scalar multiplication                   |
| 0x0000000000000000000000000000000000000008 | BN128Pair   | Elliptic curve pairing check                           |
| 0x0000000000000000000000000000000000001000 | FRA (FRC20) | Implement native token FRA to support IERC20 interface |

### FRC20-FRA precompile contract[​](https://wiki.findora.org/docs/developers/evm\_smart\_chain/precompile#frc20-fra-precompile-contract) <a href="#frc20-fra-precompile-contract" id="frc20-fra-precompile-contract"></a>

We have an ERC20 interface compatible implemenation of FRA. We can interact with this address within ERC20 interface to control your evm FRA as if it's an FRC20 token.

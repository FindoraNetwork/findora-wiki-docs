# UTXO Staking and EVM Staking

UTXO Staking (staking using an fra… address) and EVM Staking (staking using an 0x… address) are both still available. Users can use either method to stake tokens and secure the network.

Staking done using an fra… address will not reflect on the [EVM Staking portal](https://staking.findora.org/), which is based on the EVM address. However, Discreet Labs is working on a way to associate an 0x… address with an fra… address so that tokens can be seamlessly transferred from one UTXO address to an EVM address with unbonding and restaking.

### How It Works

All staking logic is now handled by smart contracts on the EVM ledger instead of on the UTXO ledger. Because such a transition has not been done before in Web3, this was a difficult change to make. However, after successfully shifting the network’s security to its EVM layer, the Findora Network is now easier to access, protect, and adjust through community governance in the future.

To synthesize staking on the EVM and UTXO ledgers, an interoperability layer has been installed that handles only staking transactions, making sure all transactions are valid and secure.

\

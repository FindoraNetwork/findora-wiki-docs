# UTXO Native Chain

Findora's UTXO Native Chain, in connection with the Zei cryptography library, offers developers the ability to confidentially transfer tokens on the UTXO Native Chain.

However, please note, there is no smart contract platform or virtual machine to execute business logic that directly calls the APIs in the [UTXO Native Chain SDK](../../developers/sdks/utxo-native-chain-sdk/). Thus, to deploy a decentralized application, developers would need to deploy business logic on Findora's EVM Smart Chain which is 100% EVM compatible. Transactions initiated on EVM Smart Chain can be routed through the UTXO Native Chain to help anonymize the transactions -- See the [Privacy Routing SDK](../../developers/sdks/privacy-routing-sdk.md) for details on this process.

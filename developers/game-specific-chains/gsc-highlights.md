# GSC Highlights

### **Two Second Blocktimes – or faster**&#x20;

Preventing latency through fast block times is essential for Web3 gamers to keep their experience fun. Findora’s first GSC spun up for Ender’s Gate features 2-second block times but GSC block times have been tested to as low as 30 milliseconds. Developers who want to spin up their own GSC can choose their own validators and a block time that will work for them.

### **Built-in ZkGaming**

GSCs come with the [zkGaming SDK](https://github.com/FindoraNetwork/zkcard-mini-sdk) that empowers developers to build games that require on-chain shuffling or hidden state data.

VRFs (variable random functions) are a gaming primitive, but their outputs are public, like dice rolls. On-chain games require more than just a randomization function, they also require private shuffling and hidden cards. For example, poker on an open ledger would be pretty pointless since everyone would know each others’ hands.

ZkShuffling is a function that can keep state data private until the right moment enabling all kinds of new games.&#x20;

### EVM compatible

GSCs, like Findora, are EVM compatible, meaning Solidity developers can easily build games on them. By simply calling functions from the SDK, they can use zk-functions without needing to learn Rust or another programming language.&#x20;

Verifiably Random and Fair

The random function can be verified using zk-proofs so that all players can be assured they are playing on equal footing and gameplay is fair.

### Modular Architecture

GSCs are modular subnets, meaning that the consensus, virtual machine, and execution layers can be customized based on the needs of the community. For example, the consensus module could be switched from Tendermint to Hostfuff or Overlord. It’s also possible to use a different virtual machine that isn’t an EVM. GSC’s zk components are also customizable, with some configurations reaching over 2,000 TPS.

\

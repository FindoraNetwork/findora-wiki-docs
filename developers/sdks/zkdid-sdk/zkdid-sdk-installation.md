# ⚙ zkDID SDK Installation

## Overview

`Special Note`: The initial MVP implementation of Findora’s zkDID currently excludes features expected in the final zkDID design such as i) non-transferable NFT support (to store the DIDs on-chain) and ii) IPFS integration to store credentials (and/or proofs) on-chain.

Findora’s `zkdid-js` SDK consists of a collection of APIs to create decentralized identifiers (DIDs), credentials and proofs to enable DID holders to prove credential data (i.e. private information) about themselves in a [zero-knowledge](https://hackernoon.com/eli5-zero-knowledge-proof-78a276db9eff) (zk) manner.

Zero-knowledge refers to the ability to cryptographically verify data without disclosing the exact credential value (i.e. cryptographically enable the verification that a DID holder’s credential contains credit score is above 700 — without revealing the exact number to the verifier).

For a conceptual overview of DIDs, credentials and the stakeholders in the credentialing and verification processes, visit the [zkDID and Credentials](../../../modules/zkdid-and-credentials.md) modules section of Findora’s documentation. Also, please see the official [W3C DID specification](https://www.notion.so/zkDID-Documentation-a-Modules-zkDID-Credentials-695f80687ec94d2fb32b3159f4ca945f).

The key zkDID APIs are defined in the [zkDID Github repo](https://github.com/FindoraNetwork/zkdid-js/tree/main/src) and the key API definition files include:

* `circuits.ts` - create ZK circuits
* `credential.ts` - create and retrieve credentials
* `did.ts` - create and retrieve DIDs
* `zkproof.ts` - create and verify zkProofs

## Prerequisites

To use the zkDID SDK requires developers to have first installed the `ethers.js` library ([install instructions](https://docs.ethers.io/v5/getting-started/)).

## zkDID SDK Installation

To install the `zkdid-js` SDK, you need to Git clone the [zkDID Github repo](https://github.com/FindoraNetwork/zkdid-js) into your project directory.

## zkDID SDK Usage

Finally, import the `zkDID` package into your project’s javascript codebase (as well as `ethers` package):

```typescript
import zkDID from `zkDID`;
import ethers from `ethers`;
```

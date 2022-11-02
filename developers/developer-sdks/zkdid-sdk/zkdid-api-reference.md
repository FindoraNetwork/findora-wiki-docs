# zkDID API Reference

`Special Note`: The initial MVP implementation of Findora’s zkDID currently excludes features expected in the final zkDID design such as i) non-transferable NFT support (to store the DIDs on-chain) and ii) IPFS integration to store credentials (and/or proofs) on-chain.

The zkDID API source code is available on \[Github]\([https://github.com/FindoraNetwork/zkdid-js.)](https://github.com/FindoraNetwork/zkdid-js.\)). To see examples of how to use these APIs visit our zkDID [example code](zkdid-example-code.md) document. Below are the zkDID APIs (API descriptions are written in the comments of codebase):

## i) DID Setup (did.ts)

* `hasDID`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/did.ts#L11:L18](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/did.ts#L11:L18)
* `getDID`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/did.ts#L20:L24](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/did.ts#L20:L24)
* `createDID`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/did.ts#L33:L40](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/did.ts#L33:L40)

## ii) Credential Setup (credential.ts)

* `hasZKCredential`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L36:L41](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L36:L41)
* `getZKCredential`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L49:L51](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L49:L51)
* `createZKCredential`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L63:L83](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L63:L83)
* Predefined Credentials
  * Created for demonstration purposes only (and used by zkDID code examples document)
    * `GPACredential`
      * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L86:L116](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L86:L116)
    * `CreditScoreCredential`
      * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L119:L148](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L119:L148)
    * `AnnualIncomeCredential`
      * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L151:L180](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/credential.ts#L151:L180)

## iii) Circuits.ts

* `hasCircuit`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/circuit.ts#L70:L75](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/circuit.ts#L70:L75)
* `getCircuit`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/circuit.ts#L83:L88](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/circuit.ts#L83:L88)
* `createCircuit`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/circuit.ts#L96:L101](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/circuit.ts#L96:L101)

## iv) Constraints.ts

* `getKeyOfConstraint`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/constraints.ts#L29:L33](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/constraints.ts#L29:L33)
* `getConstraintByKey`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/constraints.ts#L35:L37](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/constraints.ts#L35:L37)

## V) zkProof.ts

* `generateZKProof`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/zkproof.ts#L31:L48](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/zkproof.ts#L31:L48)
* `verifyZKProof`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/zkproof.ts#L79:L111](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/zkproof.ts#L79:L111)
* `verifySignedZKProof`
  * [https://github.com/FindoraNetwork/zkdid-js/blob/main/src/zkproof.ts#L120:L125](https://github.com/FindoraNetwork/zkdid-js/blob/main/src/zkproof.ts#L120:L125)

\

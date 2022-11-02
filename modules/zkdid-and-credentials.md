# zkDID and Credentials

## Overview

The zkDID SDK allows developers to implement decentralized identifiers (DIDs), zero-knowledge credentials (zkCredentials) and zero knowledge proofs (zkProofs). With these components, developers can enable Dapps (i.e. verifiers) to access private information about DID holders via reading their zkProofs (that is based on information stored in their zkCredentials). The module will provide an overview of the main stakeholders and key flows to implement a credential issuance and verification processes.

Of note, [zero-knowledge](https://hackernoon.com/eli5-zero-knowledge-proof-78a276db9eff) refers to the ability to cryptographically verify data without disclosing the exact credential value (i.e. cryptographically enable the verification that a DID holder’s credential contains credit score is above 700 — without revealing the exact number to the verifier).

For detailed information about DIDs and credential verification, please see the official [W3C DID specification](https://www.w3.org/2019/did-wg/).

To skip directly, to installing the zkDID SDK [click here](../developers/sdks/zkdid-sdk/zkdid-sdk-installation.md).

## Key Stakeholders

Findora’s zero-knowledge decentralized identity (zkDID) SDK is a set of developer tools to generate decentralized identifiers (DIDs) and credentials that contain private data about the DID holder.

The key stakeholders in the zkDID SDK system include:

* **a) Credential Issuer**&#x20;
  * trusted entity that creates DID identifier, zkCircuit, and zkCredential which contains private data (i.e. credit score, university GPA, etc.) about the DID holder
* **b) DID Holder**
  * the owner of a DID identifier (which will be later linked to zkCredentials)
* **c) Verifier**&#x20;
  * typically a Dapp (that the DID holder has logged into via Metamask) that needs to verify private data about a user (that was stored inside a DID holder’s zkCredential)

## Overall Architecture

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption><p>zkDID Process Flow - Overall Flow</p></figcaption></figure>

Overall, the zkDID process consists of:

1. A credential issuer (specifically an identity issuer) who will verify a DID holder's identity and generate a DID for the user (aka DID holder) and possibly a zkCredential with name and date of birth info. Next, other credential issuers will issue zkCredentials for the DID holder (i.e. credit score credential, GPA credential, etc.). The credential issuer will also link a specific zkCircuit to the zkCredential. The zkCircuit enables the creation of zkProofs later on that will reveal information stored in the zkCredential in a zero-knowledge manner to a verifier.
2. A DID holder will generate a zero-knowledge proof (zkProof), and sign this zkProof, using their credential as input.
3. A verifier (aka a Dapp) to whom the DID holder submits a zkProof to. The verifier will verify the zkProof, which reveals private information about the DID holder in a zero knowledge fashion.

## Key Flows

Below are the key flows that developers can build to replicate the web apps/Dapps the main stakeholders (credential issuer and verifier) must provide. Note, the diagrams below is not the only way to architect a DID and credential issuance system.

**i) Credential Issuer - Create ZK Circuit for a Credentials to Issue**

<figure><img src="../.gitbook/assets/image (22) (1).png" alt=""><figcaption><p><strong>Create zkCircuit</strong></p></figcaption></figure>

* Credential Issuers must create a zero-knowledge `circuit` (zkCircuit) which is required to create a zkCredential and, later on, a zkProof. Alternatively, a pre-defined zkCircuit can be used as well (if the credential issuers wishes to outsource the zkCircuit creation process to a trusted third party).

****

**ii) Credential Issuer - DID Credential Creation Flow**

<figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption><p><strong>Credential Issuer - DID Credential Creation Flow</strong></p></figcaption></figure>

* A Credential Issuer will create a new DID identifier for Metamask users who don’t currently have a DID identifier
* Identity Issuer will create the DID identifier and the first identity-related credentials (i.e. name, date of birth, etc.)
* More general credential issuers will create credentials linked to the DID identifier with general credential information such as credit score, university GPA, etc.



**iii) Verifier - User Creates zkProof and Uploads Credential for Dapp to Verify**

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p><strong>Create/Submit zkProof and Verify zkProof</strong></p></figcaption></figure>

* DID Holders must create a zkProof and submit this proof to the verifier
  * To create this proof, the DID holder provides their zkCredential as an input along with the info about the zkCircuit used to originally create the zkCredential
  * The proof is then signed by the DID holder's Metamask wallet
* Finally, the verifier verifies the DID Holder’s zkProof
* Note: The example process flow above shows that the verifier builds a flow (i.e. a GUI screen for DID holders) that enables DID holders to create the zkProofs. However, developer's do not need to follow this flow exactly (i.e. developers can create a separate flow just to enable users to create zkProofs -- outside of the verifier's Dapp flow).


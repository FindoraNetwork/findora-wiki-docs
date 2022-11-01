# zkDID Example Code

## Overview

Below are code examples of how the zkDID API can be used to create DID identifiers, zkCircuits, zkCredentials and zkProofs — as well as verifying zkProofs. To learn more about how DIDs and credentials work in general, visit the [zkDID and Credentials modules section](https://app.gitbook.com/o/-MUwD0X\_8WFGy\_Ynx4KB/s/RzwHg4ShKVrXd4rywBQ8/\~/changes/Qv0dvNWB7ziHTq0rWah0/zkdid-and-credentials).

The full example codebase can be accessed here: [https://zkdid.pages.dev](https://zkdid.pages.dev).

## Example 1

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p><a href="https://zkdid.pages.dev">https://zkdid.pages.dev</a></p></figcaption></figure>

// # Example 1: Use pre-defined zkCircuit and zkCredential to create and verify zkProofs #

// ### Goal ###

// The code example below showcases how to use pre-generated (i.e. mocked up) zero-knowledge (zk) proof circuits that can verify that GPA is above a certain range and related to a zkCredential containing a GPA value.

// ### Use Pre-Defined Objects (to simplify things for demo purposes) ###

// The example code provides a pre-defined wallet address (”address”), a pre-defined did identifier (”did”), a pre-defined zkCredential (”GPACredential()”) representing GPA, and a pre-defined zkCircuit (”CONSTRAINT\_GPA\_35” that checks if GPA is greater than 3.5)

// ### Key SDK APIs Used ###

// For example purposes, the code creates a zkCredential (”createZKCredential()”) for the user with a GPA of 4.0, creates a zkCircuit (”ZKCircuit()”) to check if GPA is greater than 3.5, creates a zkProof (”generateZKProof()” using the zkCredential as the input) and then verifies the credential (”verifyZKProof()”)

// ### Real-World Notes ###

// In real-world, the identity issuer would create the DID identifier and first zkCredential (”createZKCredential()”) with name and perhaps date of birth for the DID holder. The identity issuer would also create their own zkCircuit (”ZKCircuit()”) or have a trusted partner create it to be used to generate a zkProof to prove the date of birth. A 3rd party (or even verifier) Dapp would enable users to create the zkProof (”generateZKProof()”), and the verifier Dapp would verify the proof.

***

## Example 2

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption><p><a href="https://zkdid.pages.dev">https://zkdid.pages.dev</a></p></figcaption></figure>

// # Example 2: Create Custom zkCircuit and zkCredential to create and verify zkProofs #

// ### Goal ###

The code example below showcases how to create your own custom zkCircuit and zkCredential. Later, you will create a zkProof from your custom credential and then verify the zkProof.

// ### Key Code Components ###

// Part a) Create a custom credential (KYC\_Credential). This example chooses to create a custom credential that stores three values a) dateOfBirth and b) name, and c) country

// Part b) Create constraints (which will be used in the zkCircuits later) that allow the zkCircuits to prove specific facts about the DID holder. This examples creates constraints to prove i) born after year 1900 or 2000 (”KYC\_BORN\_in\_the\_20th\_century\_min”/”max”) and ii) country of birth (”KYC\_Country\_ASoutheast\_Asia\_v0001\_range”)

// Part c) Create an array of example wallets addresses (and DID identifiers) — each representing a unique DID holder with a random birthdate and country of birth generated for each of them

// Part d) Create a custom zkCircuit with two constraints — using the constraints defined above for 1) birth date and 2) country

// Part e) Create a zkCredential and zkProof for each DID holder created earlier and then verify the zkProof

***

## Example 3

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption><p><a href="https://zkdid.pages.dev">https://zkdid.pages.dev</a></p></figcaption></figure>

// # Example 3: Use custom credential and multiple circuits to create proofs and verify zkProofs #

// ### Goal ###

// Similar to _**Example 2**_ but creates more zkCircuits for different verifications.

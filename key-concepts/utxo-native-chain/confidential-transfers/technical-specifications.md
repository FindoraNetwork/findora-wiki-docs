---
description: >-
  Let us take a deep dive into some of the concepts involving the cryptography
  under the hood which enables the confidential transfers
---

# Technical Specifications

### Primitives

#### Schnorr's protocol

Schnorr's protocol is a zero-knowledge protocol that allows a Prover to prove that he knows the discrete logarithm between two group elements. It is instantiated with groups such as elliptic curve groups where the discrete logarithm problem is believed to be hard.

Given commitments to pairs representing asset-types and amounts, this protocol can be used to prove that two commitments are to the same asset-type. With minor modifications, the protocol can also be used to prove that the commitments are to distinct asset types if necessary.

For a detailed explanation of the delegated Schnorr protocol, [check this page](../../cryptography/delegated-schnorr.md)

#### Pedersen commitments

The cryptographic commitments are _perfectly hiding_, which makes them distinct from encryptions. They do not contain any information that can be decrypted by someone with a key. Rather, they serve as a hidden fingerprint for the committed information, similar to how a server can send a hash of a file before sharing the file. The hash is a unique fingerprint that can be measured from the file, but the file cannot be obtained from the hash. Cryptographic commitments can only be “opened” or “unblinded” given the unique information that was committed and a secret value called the _blinding factor_. If $$C$$ is a commitment to a message $$m$$ using blinding factor $$r$$, then $$C$$ can be uniquely computed from $$m$$ and $$r$$, and the knowledge of $$r$$ is proof that $$C$$ was a commitment to $$m$$. In Findora’s blinded asset records, the blinding factors are shared with the new asset owner (i.e. transfer recipient) using a method similar to a Diffie-Hellman key exchange. This user derives the blinding factors from blind share and its private key corresponding to public key. The user needs these blinding factors in order to check that the decrypted contents of the record are correct (i.e. as approved by the validators) and will also need to use them to transfer ownership of the asset in a future transaction.

As before, let $$\mathbb{G}$$ denote the Ristretto group, i.e. the group of points on the Ristretto curve. Let $$p$$ be the order of this group. For independent group generators $$g_1,g_2,h\in \mathbb{G}$$ and a pair $$(a,b)\in \mathbb{F}_p^2$$ representing the asset type and amount, the commitment to this pair is given by $$g_1^{a}g_2^{b}h^r$$ where $$r$$ is a random element in $$\mathbb{F}_p$$.

Findora uses the _Ristretto_ group, which is a quotient group built from the elliptic curve group on Curve25519. This group has order $$8p$$ for the prime: $$p =2^{252} +27742317777372353535851937790883648493.$$

The Ristretto quotient group is the unique quotient group of order $$p$$.

#### Bulletproofs

The range proofs are derived from a zero-knowledge proof scheme called _Bulletproofs_. This is an instantiation of a special class of range proofs where the sender proves in zero-knowledge (i.e. without revealing any other information about the transaction) that the masked (or committed) amount falls within a certain range. In particular, a sender can use this scheme to prove that the amount he sent is non-negative and does not exceed his balance, which is necessary to prevent double-spending on the chain. This is a _transparent_ scheme, meaning it does not require any preprocessing phase or trusted setup. The security of Bulletproofs relies on the hardness of the discrete logarithm problem in elliptic curves, which is one of the oldest and most battle-tested assumptions in cryptography.

We first describe a straightforward albeit inefficient way to create a range proof. The Prover decomposes the integer representing the amount into its binary representation. He then creates commitments to each of those bits and then sends a proof attesting to the claim that each of these commitments is to a bit and that the amount is the aggregation of these bits. But this proof size is linear in the bit length of the amount, which is quite inefficient in practice. Bulletproofs is an efficient range proof which is logarithmic in the size of the amount. The core of the bulletproof protocol hinges on a technique called the _recursive inner product argument_.

[Check this link](../../cryptography/bulletproofs.md#bulletproofs-based-mixing-protocol) for details on the Bulletproofs-based mixing protocol

#### Range proofs via inner product arguments

Let $$C_v = g^{v} h^r$$ be a commitment to a value $$v$$. To show that $$v$$ lies in the range $$[0,2^{n}-1]$$, it suffices for the Prover to show that he knows a vector $$\mathbf{a}L = (a_0,\cdots,a{n-1})$$ such that:

* $$\langle \mathbf{a}L;,; \mathbf{2}^n \rangle = v$$_, which shows that_ $$v = \sum{i=0}^n a_i\cdot 2^i$$
* $$\mathbf{a}_L \circ (\mathbf{1}^n - \mathbf{a}_L) = \mathbf{0}^n$$, which shows that the entries of $$\mathbf{a}_L$$ lie in $${0,1 }^n$$.

In other words, this shows that the $n$ entries of $$\mathbb{a}_L$$ represent the bit decomposition of $$v$$.

For randomly generated challenges $$y, z\in \mathbb{F}_p$$, it suffices to show that,

$$z^2 \cdot \langle \mathbf {a}_L \hspace{3pt} , \hspace{3pt} \mathbf {2}^n \rangle + z \cdot \langle \mathbf {a}_L - \mathbf {1}^n - \mathbf {a}_R \hspace{3pt} , \hspace{3pt} \mathbf {y}^n \rangle + \langle \mathbf {a}_L \hspace{3pt} , \hspace{3pt} \mathbf {a}_R \circ \mathbf {y}^n \rangle = z^2 \cdot v \hspace{20pt}$$

where $$\mathbf {a}_R = \mathbf{1}^n - \mathbf{a}_L$$

### Proof Generation

The `XfrProofs` data structure contains a zero-knowledge proof that the blinded output records are valid with respect to the blinded input records. Since the fees are denominated in the FRA token, it is necessary to prove in zero-knowledge that:

* for every asset type other than FRA, the sum of the inputs is the same as the sum of the outputs
* the sum of the inputs corresponding to the FRA asset is the same as the sum of the outputs plus the fees for the transaction.

Note that for some particular asset types, there might be fees, thus for that cases it proves that sum of output amounts for that asset type in the output asset records plus fees equals the sum of input amounts for the same asset type in the input records). To be more precise, if there are n $$(n \geq 1)$$ inputs records and m $$(m \geq 1)$$ output records,

* $$\alpha_i$$ is the amount in the $$i$$th input record
* $$\beta_j$$ is the amount in the $$j$$th output record
* $$Input[\tau]$$ the set of input indices with asset type matching $$\tau$$
* $$Output[\tau]$$ the set of output indices with asset type matching $$\tau$$
* $$\mathcal{T}$$ is the complete set of types other than FRA in output records

Then **XfrProofs** prove that

for all $$\tau \in \mathcal{T} ;; \sum_{i \in Input[\tau]} \alpha_i = \sum_{j \in Output[\tau]} \beta_j$$

when asset type matches $$FRA$$ (i.e $$\tau = FRA$$). Fees must be considered. Hence the equation becomes as follows

$$\sum_{i \in Input[FRA]} \alpha_i = \sum_{j \in Output[FRA]} \beta_j + Fees$$

The randomness in the Pedersen commitments is communicated to the receiver in the form of text encrypted with the receiver's public key. The receiver then decrypts this text using his private key. The security of this scheme hinges on the hardness of the Discrete logarithm problem (DLP). The proof of the amount-sum equality relies on the homomorphic property of Pedersen commitments.

#### Proving Commitment Equality

A confidential transaction can - and usually does - have multiple associated Pedersen commitments to (asset type, amount) pairs. To prove the so-called _amount-sum equality_, it is necessary to _verifiably_ reveal which of the commitments correspond to the same asset type, without actually revealing this asset type. To show that two Pedersen commitments $$C_1 = g_1^{a_1}g_2^{b_1}h^{r_1}$$, $$C_2 = g_1^{a_2}g_2^{b_2}h^{r_2}$$ are such that $$a_1 = a_2$$, it suffices to show that the quotient $$C_1\cdot C_2^{-1}$$ is of the form $$g_2^{x}h^y$$ for some $$x,y$$ known to the Prover. Using an aggregation trick, this proof can be kept constant-sized when the Prover needs to show that the asset type committed in $$C_1$$is the same as the asset type committed in $$C_2,\cdots,C_n$$.

#### Proving the Amount-Sum Equality

Given input commitments $$C_1^{\mathrm{in}},\cdots, C_m^{\mathrm{in}}$$ and output commitments $$C_1^{\mathrm{out}},\cdots, C_n^{\mathrm{out}}$$ verifiably corresponding to the same asset type, a Prover shows that the input and output amounts sum up to the same value by proving in zero-knowledge that the element $$\widetilde{C}:= (\prod_{i=1}^m C_i^{\mathrm{in}})\cdot (\prod_{j=1}^n C_j^{\mathrm{out}})^{-1}$$ is of the form $$g_1^{a(m-n)}h^{r}$$ (or $$g_1^{a(m-n)}g_2^{\mathrm{fees}}h^{r}$$ in case the asset\_type is FRA) where $$r$$ is some integer known to the Prover and $$a$$ is the common asset-type committed in the commitments $$C_i^{\mathrm{in}}, C_j^{\mathrm{out}}$$.

To prevent double-spends on the blockchain in tandem with maintaining confidentiality, it is necessary for the sender of a transaction to prove in zero-knowledge that the amounts committed are all non-negative. This requires a zero-knowledge range proof to convince a Verifier that the amounts are non-negative. Findora's confidential transfer is accompanied by proofs that the committed amounts lie in the range $$[0, 2^{64}-1]$$. These proofs are constructed using the Bulletproofs scheme.

Bulletproofs are particularly suited for range proofs on small ranges: the proof for a $$64$$-bit range is less than 1KB and takes only milliseconds to both create and verify. Bulletproofs have a batching mode where a range proof from $$m$$ points is only $$64\log(m)$$ bytes larger than a range proof for a single point (e.g. a batch proof for 100 points is less than 500 bytes larger). Bulletproofs also have a batch verification mode where the amortized time to verify many range proofs is approximately 0.34 ms per proof.

### Proof Verification

During the verification of confidential transfer at the validators' end, the validity of the `XfrNote` is checked. This is done in batches to increase the efficiency. The following is the hierarchy of the steps:

* Verifying if the signatures associated with the transaction are valid
* Batch verifying the bodies
  * Verifying the Asset Records if the amounts and asset types are correct
    * Verifying the batched range proof for the confidential amounts
    * Verifying the delegated Schnorr proofs for the confidential asset types
    * Verifying the batched asset mixing proofs for checking the amount sum equality for multiple assets
  * Verifying the Asset Tracing proofs

<figure><img src="https://raw.githubusercontent.com/FindoraNetwork/findora-wiki/develop/static/img/proof_verification.jpg" alt=""><figcaption></figcaption></figure>

For the equality of committed asset types, the Verifier's task boils down to verifying Schnorr proofs of knowledge of discrete logarithms. The proofs are batched so that the communication complexity and the verification time stay constant.

To verify the range proofs, the Verifier performs a sequence of inner product checks. The Verifier uses the same hashing algorithm as the Prover to get the independent group generators in $$\mathbb{G}$$. This makes his runtime $$\mathbf{O}(n)$$.

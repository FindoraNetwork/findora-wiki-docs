# TurboPlonk

### Introduction

Findora's "triple masking" payment uses an optimized variant of TurboPlonk. The following equations summarize the structure.

$$
\begin{align} &~~~~q_1(X)\cdot w_1(X) + q_2(X)\cdot w_2(X) + q_3(X)\cdot w_3(X) + q_4(X)\cdot w_4(X)~~~\text{// linear combination} \notag\\ &+q_{m1}(X)\cdot w_1(X)\cdot w_2(X) + q_{m2}(X)\cdot w_3(X)\cdot w_4(X)~~~\text{// multiplication (somewhat)}\notag\\ &+q_c(X)~~~\text{// constants}\notag \\ &+\mathsf{PI}(X)~~~\text{// inputs}\notag\\ &+q_{ecc}(X)\cdot w_1(X)\cdot w_2(X)\cdot w_3(X)\cdot w_4(X)\cdot w_o(X)~~~\text{// operations on twisted Edwards curves}\notag\\ &=q_o(X)\cdot w_o(X)~~~\text{// output}\notag\\[1em] &~~~~q_b(X)\cdot w_2(X) \cdot (w_2(X) - 1) = 0~~~\text{// boolean testing on the second wire}\notag\\ &~~~~q_b(X)\cdot w_3(X) \cdot (w_3(X) - 1) = 0~~~\text{// boolean testing on the third wire}\notag\\ &~~~~q_b(X)\cdot w_4(X) \cdot (w_4(X) - 1) = 0~~~\text{// boolean testing on the fourth wire}\notag\\[1em] &~~~~q_{prk3}(X)\cdot((w_4(X) + g \cdot w_3(X)+ q_{prk3}(X) - w_3(X \omega))^5\notag\\ &~~~~~~~~+ g\cdot (w_4(X) + g \cdot w_3(X) + q_{prk3}(X))^2\notag\\ &~~~~~~~~- (w_1(X) + g\cdot w_2(X) + q_{prk1}(X))) = 0~~\text{// the first equation for Anemoi/Jive}\notag\\[0.5em] &~~~~q_{prk3}(X)\cdot((g \cdot w_4(X) + (g^2+1) \cdot w_3(X)+ q_{prk4}(X) - w_o(X))^5\notag\\ &~~~~~~~~+ g\cdot (g \cdot w_4(X) + (g^2 + 1) \cdot w_3(X) + q_{prk4}(X))^2\notag\\ &~~~~~~~~- (g\cdot w_1(X) + (g^2+1) \cdot w_2(X) + q_{prk2}(X))) = 0~~\text{// the second equation for Anemoi/Jive}\notag\\[0.5em] &~~~~q_{prk3}(X)\cdot((w_4(X) + g \cdot w_3(X)+ q_{prk3}(X) - w_3(X \omega))^5\notag\\ &~~~~~~~~+ g\cdot (w_3(X \omega))^2 + g^{-1} - w_1(X \omega)) = 0~~\text{// the third equation for Anemoi/Jive}\notag\\[0.5em] &~~~~q_{prk3}(X)\cdot((g \cdot w_4(X) + (g^2+1) \cdot w_3(X)+ q_{prk4}(X) - w_o(X))^5\notag\\ &~~~~~~~~+ g\cdot (w_o(X))^2 + g^{-1} - w_2(X \omega)) = 0~~\text{// the fourth equation for Anemoi/Jive}\notag \end{align}
$$

We now describe the indexer, the prover, and the verifier.

### Indexer

The indexer in TurboPlonk computes the commitments and openings for indexer polynomials, which consist of the following:

*   The fourteen selector polynomials:

    $$
    \begin{array}{c} q_1(X), q_2(X), q_3(X), q_4(X), q_o(X), q_{m1}(X), q_{m2}(X), q_c(X), q_{ecc}(X), q_{b}(X),\\ q_{prk1}(X), q_{prk2}(X), q_{prk3}(X), q_{prk4}(X) \end{array}
    $$
*   The five permutation polynomials:

    $$
    S_{\sigma1}(X), S_{\sigma2}(X), S_{\sigma3}(X), S_{\sigma4}(X), S_{\sigma o}(X)
    $$

First of all, let the number of gates be $$n$$, the constraint system should have indicated a permutation $$\sigma: [5n]\rightarrow [5n]$$, which fulfills the following requirements.

* Let $$w(X)$$ be the concatenated witness polynomial of $$w_1(X), w_2(X), w_3(X), w_4(X), w_o(X)$$. The concatenation is over the evaluation representation, not the coefficient representation.
* The evaluation of $$w(X)$$ remains unchanged after applying $$\sigma$$ as a permutation over the evaluation of $$w(X)$$ itself.

Now, given four different quadratic non-residues $$(k_1, k_2, k_3, k_4)$$ and a generator $$\omega$$ with order $$n$$, we define a mapping as follows.

$$
\sigma_0 \left(i\right) = \begin{cases} \omega^{i-1} & i\in \{1,2,...,n\}\\ k_1\cdot \omega^{i -1 - n} & i \in\{n+1, n+2, ..., 2n\}\\ k_2\cdot \omega^{i -1 - 2n} & i \in\{2n+1, 2n+2, ..., 3n\}\\ k_3\cdot \omega^{i -1- 3n} & i \in\{3n+1, 3n+2, ..., 4n\}\\ k_4\cdot \omega^{i -1- 4n} & i \in\{4n+1, 4n+2, ..., 5n\} \end{cases}
$$

where $$i = 1, 2, ..., n$$. And we apply this mapping to each element in $$\sigma$$, obtaining a map $$\sigma^*(x): [5n] \rightarrow\mathbb{F}$$. We split this map into five permutation polynomials, as follows.

* $$S_{\sigma1}(X)$$'s evaluation on $$1,\omega, ..., \omega^{n-1}$$ equals $$\sigma^*(x)$$'s evaluation on $$1, 2, ..., n$$.
* $$S_{\sigma2}(X)$$'s evaluation on $$1, \omega, ..., \omega^{n-1}$$ equals $$\sigma^*(x)$$'s evaluation on $$n+1, n+2, ..., 2n$$.
* $$S_{\sigma3}(X)$$'s evaluation on $$1, \omega, ..., \omega^{n-1}$$ equals $$\sigma^*(x)$$'s evaluation on $$2n+1, 2n+2, ..., 3n$$.
* $$S_{\sigma4}(X)$$'s evaluation on $$1, \omega, ..., \omega^{n-1}$$ equals $$\sigma^*(x)$$'s evaluation on $$3n+1, 3n+2, ..., 4n$$.
* $$S_{\sigma o}(X)$$'s evaluation on $$1, \omega, ..., \omega^{n-1}$$ equals $$\sigma^*(x)$$'s evaluation on $$4n+1, 4n+2, ..., 5n$$.

**Step 1: commit all polynomials**

We first commit all these indexer polynomials. The commitments are included in the verifier parameters. We then perform some precomputation: we prepare a representation of these polynomials that are easy to be use later for proving, by doing a coset FFT over them. The prepared polynomials are included in the prover parameters.

**Step 2: precompute the two helper polynomials**

Compute the following polynomial defined on a domain $$H$$ of size $$n$$:

$$
L_1(X) = \frac{X^n - 1}{X-1}
$$

and store its coset FFT representation. This is done by first observing that $$L_1(X)$$ evaluates to $$n$$ on $$X = 1$$ and $$0$$ otherwise in $$H$$. We can perform an inverse FFT to convert it back to the coefficient representation (which indeed looks nontrivial). Then, we perform a coset FFT, which gives us the prepared version of this polynomial.

Another polynomial we precompute is the vanishing polynomial of domain $$H$$ of size $$n$$:

$$
Z_H(X) = X^n - 1
$$

and we want to store its coset FFT representation. This is done by a coset FFT over the coefficient representation above. The representations for the two helper polynomials are included in the prover parameters.

**Step 3: compute the Lagrange interpolation constants**

Recall that the Lagrange interpolation from $$(1, y_0), (\omega, y_1), ..., (\omega^n, y_n)$$ where $$\omega$$ is the generator for a domain $$H$$, into to a polynomial $$f(X)$$ of degree $$n$$ is as follows:

$$
f(X) = \sum_{j=0}^n~~~y_j~~~\left(\prod_{{\substack{0\leq m \leq n\\ m\neq j}}}~~~\frac{X - \omega^m}{\omega^j - \omega^m}\right)
$$

We can rewrite it as follows.

$$
\begin{align} f(X) &= \sum_{j=0}^n~~~y_j~~~\left(\prod_{{\substack{0\leq m \leq n\\ m\neq j}}}~~~\frac{X - \omega^m}{\omega^j - \omega^m}\right)\notag\\[0.5em] &= \left(\prod_{0\leq m \leq n} (X - \omega^m)\right)~~~\left(\sum_{j=0}^n~~~\frac{y_j}{X - \omega^j}~~~\left(\prod_{{\substack{0\leq m \leq n\\ m\neq j}}}~~~\frac{1}{\omega^j - \omega^m}\right)\right)\notag \end{align}
$$

Now, precompute $$c_j$$ for every $$j\in\{0,1, ..., n\}$$.

$$
c_j = \prod_{{\substack{0\leq m \leq n\\ m\neq j}}}~~\frac{1}{\omega^j - \omega^m}
$$

This allows us to simplify $$f(X)$$ as follows.

$$
\begin{align} f(X) &= \left(\prod_{0\leq m \leq n} (X - \omega^m)\right)~~~\sum_{j=0}^n~~~\frac{c_j\cdot y_j}{X - \omega^j}\notag\\[0.5em] &= (X^n - 1)~~~\sum_{j=0}^n~~~\frac{c_j\cdot y_j}{X - \omega^j}\notag \end{align}
$$

These constants $$c_j$$ $$(j\in\{0,1, ..., n\})$$ are included in the verifier parameters. We conclude the description of the indexer.

### Prover

The prover in TurboPlonk uses the prover parameters from the indexer and a complete constraint system with all the gate values and copy check information ready. It follows the following steps.

**Step 1: assemble public inputs**

The prover parameters have indicated which witness value indeed belongs to public inputs. The prover finds those witness values and stores them in a vector of length $$n_{in}$$, which is the number of field elements in public inputs. This is to enable us to calculate the state of the verifier.

**Step 2: instantiate the verifier**

For the purpose of the Fiat-Shamir transform, we create a cryptographic sponge, which will absorb the verifier's state as well as the messages that the verifier would receive from the prover in an interactive proof protocol.

After we create the sponge, we put the following two things into the sponge: (1) verifier parameters and (2) public inputs.

**Step 3: commit witness polynomials with hiding**

Given the witness polynomials $$w_1(X),\allowbreak w_2(X),\allowbreak w_3(X),\allowbreak w_4(X),\allowbreak w_o(X)$$, we add a random blinding polynomial over each of them. The prover samples $$b_1,\allowbreak b_2,\allowbreak b_3,\allowbreak ...,\allowbreak b_{13}\in \mathbb{F}$$ and computes blinded witness polynomials.

$$
\begin{align} \widetilde{w_1}(X) &= w_1(X) + Z_H(X) \cdot (b_1\cdot X^2 + b_2\cdot X + b_3)\notag\\ \widetilde{w_2}(X) &= w_2(X) + Z_H(X) \cdot (b_4\cdot X^2 + b_5\cdot X + b_6)\notag\\ \widetilde{w_3}(X) &= w_3(X) + Z_H(X) \cdot (b_7\cdot X^2 + b_8\cdot X + b_9)\notag\\ \widetilde{w_4}(X) &= w_4(X) + Z_H(X) \cdot (b_{10}\cdot X + b_{11})\notag\\ \widetilde{w_o}(X) &= w_o(X) + Z_H(X) \cdot (b_{12}\cdot X + b_{13})\notag \end{align}
$$

We commit each of the polynomial above and put the polynomial commitments $$\mathsf{cm}_{w1},\allowbreak \mathsf{cm}_{w2},\allowbreak \mathsf{cm}_{w3},\allowbreak \mathsf{cm}_{w4},\allowbreak \mathsf{cm}_{wo}\in\mathbb{G}_1$$ into the sponge.

**Step 4: build the sigma polynomial, for wiring**

The prover squeezes out two challenges $$\beta, \gamma\in\mathbb{F}$$ from the sponge. We now need to build the sigma polynomial. It helps for us to first compute:

$$
S_i := \frac{\begin{array}{c}(w_i+\beta\cdot\omega^{i-1} + \gamma)\cdot (w_{n+i} + \beta\cdot k_1\cdot\omega^{i-1} + \gamma)\cdot (w_{2n+i} + \beta\cdot k_2\cdot\omega^{i-1} + \gamma)\\\cdot (w_{3n+i} + \beta\cdot k_3\cdot \omega^{i-1} + \gamma)\cdot (w_{4n+i} + \beta\cdot k_4\cdot \omega^{i-1} + \gamma)\end{array}}{\begin{array}{c} (w_i + \sigma^*(i)\cdot\beta + \gamma)\cdot (w_{n+i} + \sigma^*(n+i)\cdot\beta + \gamma)\cdot (w_{2n+i} + \sigma^*(2n+i)\cdot\beta + \gamma)\\ \cdot (w_{3n+i} + \sigma^*(3n+i)\cdot \beta + \gamma)\cdot (w_{4n+i} + \sigma^*(4n+i)\cdot \beta + \gamma) \end{array}}
$$

We can then define the permutation polynomial $$z(X)$$ with the following evaluations:

$$
z(\omega^{i-1}) = \begin{cases} 1 & i = 1\\ \prod_{j=1}^{i-1} S_i & i = 2, 3, ..., n\\ \end{cases}
$$

**Step 5: commit the sigma polynomial, with hiding**

The prover first samples $$b_{14},\allowbreak b_{15},\allowbreak b_{16}\in\mathbb{F}$$ and apply them as blinding factors to the polynomial $$z(X)$$.

$$
\widetilde{z}(X) = z(X) + Z_H(X)\cdot (b_{14} X^2 + b_{15} X + b_{16})
$$

We commit this polynomial and put the polynomial commitment $$\mathsf{cm}_{z}\in\mathbb{G}_1$$ into the sponge.

**Step 6: compute the quotient polynomial**

The prover squeezes out a challenge $$\alpha$$ from the sponge. This is used to construct the following polynomial.

$$
\begin{align} t(X) &= t_\mathsf{sat}(X)\cdot \frac{1}{Z_H(X)} + t_{\sigma 1}(X)\cdot \frac{\alpha}{Z_H(X)} - t_{\sigma 2}(X)\cdot \frac{\alpha}{Z_H(X)}+ t_{\sigma 3}(X)\cdot \frac{\alpha^2}{Z_H(X)}\notag\\ &+ t_{b1}(X) \cdot \frac{\alpha^3}{Z_H(X)} + t_{b2}(X) \cdot \frac{\alpha^4}{Z_H(X)}+ t_{b3}(X) \cdot \frac{\alpha^5}{Z_H(X)} - t_{h1}(X)\cdot \frac{\alpha^6}{Z_H(X)}\notag\\ &- t_{h2}(X)\cdot \frac{\alpha^7}{Z_H(X)} - t_{h3}(X)\cdot \frac{\alpha^8}{Z_H(X)}- t_{h4}(X)\cdot \frac{\alpha^9}{Z_H(X)}\notag \end{align}
$$

where

$$
\begin{align} t_{sat}(X) &= q_1(X)\cdot \widetilde{w_1}(X) + q_2(X)\cdot \widetilde{w_2}(X) + q_3(X)\cdot \widetilde{w_3}(X) + q_4(X)\cdot \widetilde{w_4}(X)\notag\\ &+ q_{m1}(X)\cdot \widetilde{w_1}(X)\cdot \widetilde{w_2}(X) + q_{m2}(X)\cdot \widetilde{w_3}(X)\cdot \widetilde{w_4}(X) + q_{c}(X) + \mathsf{PI}(X)\notag\\ &+ q_{ecc}(X)\cdot \widetilde{w_1}(X)\cdot \widetilde{w_2}(X)\cdot \widetilde{w_3}(X)\cdot \widetilde{w_4}(X)\cdot \widetilde{w_o}(X)\notag\\ &- q_o(X)\cdot \widetilde{w_o}(X)\notag \end{align}
$$

and

$$
\begin{align} t_{\sigma 1}(X) = &(\widetilde{w_1}(X) + \beta\cdot X + \gamma)\cdot (\widetilde{w_2}(X) + \beta\cdot k_1\cdot X + \gamma)\cdot (\widetilde{w_3}(X) + \beta\cdot k_2\cdot X + \gamma)\notag\\ &\cdot (\widetilde{w_4}(X) + \beta\cdot k_3\cdot X + \gamma)\cdot (\widetilde{w_o}(X) + \beta\cdot k_4\cdot X + \gamma)\notag\\ &\cdot \widetilde{z}(X)\notag \end{align}
$$

and

$$
\begin{align} t_{\sigma 2}(X) = &(\widetilde{w_1}(X) + \beta\cdot S_{\sigma 1}(X) + \gamma)\cdot (\widetilde{w_2}(X) + \beta\cdot S_{\sigma 2}(X) + \gamma)\cdot (\widetilde{w_3}(X) + \beta\cdot S_{\sigma 3}(X) + \gamma)\notag\\ &\cdot (\widetilde{w_4}(X) + \beta\cdot S_{\sigma 4}(X) + \gamma)\cdot (\widetilde{w_o}(X) + \beta\cdot S_{\sigma o}(X) + \gamma)\notag\\ &\cdot \widetilde{z}(X\omega)~~~\text{// the shifting trick}\notag \end{align}
$$

and

$$
\begin{align} t_{\sigma 3}(X) = (\widetilde{z}(X) - 1)\cdot L_1(X)\notag \end{align}
$$

and

$$
\begin{align} t_{b1}(X) &= q_b(X)\cdot \widetilde{w_2}(X) \cdot (1 - \widetilde{w_2}(X))\notag\\ t_{b2}(X) &= q_b(X)\cdot \widetilde{w_3}(X) \cdot (1 - \widetilde{w_3}(X))\notag\\ t_{b3}(X) &= q_b(X)\cdot \widetilde{w_4}(X) \cdot (1 - \widetilde{w_4}(X))\notag \end{align}
$$

and

$$
\begin{align} t_{h1}(X) &= q_{prk3}(X)\cdot \left(\begin{array}{l} (\widetilde{w_4}(X) + g\cdot \widetilde{w_3}(X) + q_{prk3}(X) - \widetilde{w_3}(X\omega))^5\\ + g\cdot (\widetilde{w_4}(X) + g\cdot \widetilde{w_3}(X) + q_{prk3}(X))^2\\ - (\widetilde{w_1}(X) + g\cdot \widetilde{w_2}(X) + q_{prk1}(X))\end{array}\right)\notag\\[0.5em] t_{h2}(X) &= q_{prk3}(X)\cdot \left(\begin{array}{l} (g\cdot \widetilde{w_4}(X) + (g^2+1)\cdot \widetilde{w_3}(X) + q_{prk4}(X) - \widetilde{w_o}(X))^5\\ + g\cdot (g\cdot \widetilde{w_4}(X) + (g^2+1)\cdot \widetilde{w_3}(X) + q_{prk4}(X))^2\\ - (g\cdot \widetilde{w_1}(X) + (g^2+1)\cdot \widetilde{w_2}(X) + q_{prk2}(X))\end{array}\right)\notag\\[0.5em] t_{h3}(X) &= q_{prk3}(X)\cdot \left(\begin{array}{l} (\widetilde{w_4}(X) + g\cdot \widetilde{w_3}(X) + q_{prk3}(X) - \widetilde{w_3}(X\omega))^5\\ + g\cdot (\widetilde{w_3}(X\omega))^2 + g^{-1} - \widetilde{w_1}(X\omega)\end{array}\right)\notag\\[0.5em] t_{h2}(X) &= q_{prk3}(X)\cdot \left(\begin{array}{l} (g\cdot \widetilde{w_4}(X) + (g^2+1)\cdot \widetilde{w_3}(X) + q_{prk4}(X) - \widetilde{w_o}(X))^5\\ + g\cdot (\widetilde{w_o}(X))^2 + g^{-1} - \widetilde{w_2}(X\omega)\end{array}\right)\notag \end{align}
$$

Then, in the coefficient representations, we split the polynomial into five parts: $$t_1(X)$$, $$t_2(X)$$, $$t_3(X)$$, $$t_4(X)$$, and $$t_5(X)$$, where each polynomial has degree $$n-2$$. This is because $$t(X)$$ is expected to have degree $$3\cdot (n+2) + 2\cdot(n+1) + (n+2) - n = 5n+10$$, and $$5n+10 = 5 \cdot (n+2)$$.

**Step 7: commit the split quotient polynomials, without hiding**

We commit all these polynomials and put the commitments $$\mathsf{cm}_{t1}$$, $$\mathsf{cm}_{t2}$$, $$\mathsf{cm}_{t3}$$, $$\mathsf{cm}_{t4}$$, and $$\mathsf{cm}_{t5}$$ into the sponge.

**Step 8: open the polynomials at a random point**

The prover squeezes a random challenge $$\zeta\in\mathbb{F}$$ and compute the following opening evaluations:

$$
\begin{array}{c} \widetilde{w_1}(\zeta), \widetilde{w_2}(\zeta), \widetilde{w_3}(\zeta), \widetilde{w_4}(\zeta), \widetilde{w_o}(\zeta), S_{\sigma 1}(\zeta), S_{\sigma 2}(\zeta), S_{\sigma 3}(\zeta), S_{\sigma 4}(\zeta),\\[0.5em] q_{prk3}(\zeta), q_{prk4}(\zeta), \widetilde{w_1}(\zeta\omega), \widetilde{w_2}(\zeta\omega), \widetilde{w_3}(\zeta\omega), \widetilde{z}(\zeta \omega) \end{array}
$$

And we remind the readers that some evaluations are over $$\zeta\omega$$ instead of $$\zeta$$. This is common in entry product arguments. The prover puts these, which are elements in $$\mathbb{F}$$, into the sponge.

**Step 9: compute the linearization polynomial**

The linearization polynomial is, at a high level, to replace $$\widetilde{w_1}(X)$$, $$\widetilde{w_2}(X)$$, $$\widetilde{w_3}(X)$$, $$\widetilde{w_1}(X\omega)$$, $$\widetilde{w_2}(X\omega)$$, $$\widetilde{w_3}(X\omega)$$, $$\widetilde{w_4}(X)$$, $$\widetilde{w_o}(X)$$, $${S_{\sigma1}}(X)$$, $${S_{\sigma2}}(X)$$, $${S_{\sigma3}}(X)$$, $${S_{\sigma4}}(X)$$, $$q_{prk3}(X)$$, $$q_{prk4}(X)$$, and $$\widetilde{z}(X\omega)$$ with the evaluations over that random point. More specifically, $$r(X)$$ reads as follows. Note that the locations of $$Z_H(X)$$ are different now. The constant terms of $$r(X)$$ are removed here.

$$
\begin{align} r(X) &= r_\mathsf{sat}(X) + r_{1}(X)\cdot \alpha - r_{2}(X) \cdot \alpha + r_{3}(X)\cdot \alpha^2 + r_{4}(X)\cdot \alpha^3 \notag\\ &+ r_{5}(X)\cdot \alpha^4 + r_{6}(X)\cdot \alpha^5 + r_{7}(X)\cdot \alpha^6 + r_{8}(X)\cdot \alpha^7\notag\\ &- Z_H(\zeta) (t_1(X) + \zeta^{n+2}\cdot t_2(X) + \zeta^{2(n+2)}\cdot t_3(X)+ \zeta^{3(n+2)}\cdot t_4(X)+ \zeta^{4(n+2)}\cdot t_5(X))\notag \end{align}
$$

where

$$
\begin{align} r_\mathsf{sat}(X) &= \widetilde{w_1}(\zeta)\cdot q_1(X) + \widetilde{w_2}(\zeta)\cdot q_2(X) + \widetilde{w_3}(\zeta)\cdot q_3(X) + \widetilde{w_4}(\zeta)\cdot q_4(X)\notag\\ &+\widetilde{w_1}(\zeta)\cdot \widetilde{w_2}(\zeta)\cdot q_{m1}(X) + \widetilde{w_3}(\zeta)\cdot \widetilde{w_4}(\zeta)\cdot q_{m2}(X)+q_c(X)\notag\\ &+ q_{ecc}(X)\cdot \widetilde{w_1}(\zeta)\cdot \widetilde{w_2}(\zeta)\cdot \widetilde{w_3}(\zeta)\cdot \widetilde{w_4}(\zeta)\cdot \widetilde{w_o}(\zeta)\notag\\ &-\widetilde{w_o}(\zeta)\cdot q_o(X)\notag \end{align}
$$

and

$$
\begin{align} r_\mathsf{1}(X) = &(\widetilde{w_1}(\zeta) + \beta\cdot \zeta +\gamma)\cdot (\widetilde{w_2}(\zeta) + \beta\cdot k_1\cdot \zeta +\gamma)\cdot (\widetilde{w_3}(\zeta) + \beta\cdot k_2\cdot \zeta +\gamma)\notag\\ &\cdot (\widetilde{w_4}(\zeta) + \beta\cdot k_3\cdot \zeta +\gamma)\cdot (\widetilde{w_o}(\zeta) + \beta\cdot k_4\cdot \zeta +\gamma)\cdot \widetilde{z}(X)\notag \end{align}
$$

and

$$
\begin{align} r_\mathsf{2}(X) = &(\widetilde{w_1}(\zeta) + \beta S_{\sigma 1}(\zeta) +\gamma)\cdot (\widetilde{w_2}(\zeta) + \beta S_{\sigma 2}(\zeta) +\gamma)\cdot (\widetilde{w_3}(\zeta) + \beta S_{\sigma 3}(\zeta) +\gamma)\notag\\ &\cdot (\widetilde{w_4}(\zeta) + \beta S_{\sigma 4}(\zeta) +\gamma)\cdot \beta\cdot S_{\sigma o}(X)\cdot \widetilde{z}(\zeta \omega)\notag \end{align}
$$

Note that $$S_{\sigma o}(X)$$ is not being replaced by its evaluation, and

$$
r_{3}(X) = \widetilde{z}(X) \cdot L_1(\zeta)
$$

and

$$
\begin{align} r_{4}(X) &= q_b(X)\cdot \widetilde{w_2}(\zeta)\cdot (\widetilde{w_2}(\zeta) - 1)\notag\\ r_{5}(X) &= q_b(X)\cdot \widetilde{w_3}(\zeta)\cdot (\widetilde{w_3}(\zeta) - 1)\notag\\ r_{6}(X) &= q_b(X)\cdot \widetilde{w_4}(\zeta)\cdot (\widetilde{w_4}(\zeta) - 1)\notag \end{align}
$$

and

$$
\begin{align} r_{7}(X) &= q_{prk3}(\zeta)\cdot q_{prk1}(X)\notag\\ r_{8}(X) &= q_{prk3}(\zeta)\cdot q_{prk2}(X)\notag \end{align}
$$

Now we have the linearization polynomial. Although this polynomial is not linear, its degree is down from $$\approx 5n$$ to $$\approx n$$, and one can see that the polynomial collapses to a small one.

We note that the evaluation of $$r(X)$$ at point $$\zeta$$ is as follows. The prover does not need to include this number in the proof because it can be computed by the verifier.

$$
\begin{align} r(\zeta) &= -\mathsf{PI}(\zeta)+\alpha\cdot(\widetilde{w_1}(\zeta) + \beta S_{\sigma1}(\zeta) + \gamma) \cdot(\widetilde{w_2}(\zeta) + \beta S_{\sigma2}(\zeta) + \gamma)\cdot(\widetilde{w_3}(\zeta) + \beta S_{\sigma3}(\zeta) + \gamma)\notag\\ &\cdot(\widetilde{w_4}(\zeta) + \beta S_{\sigma4}(\zeta) + \gamma)\cdot(\widetilde{w_o}(\zeta)+\gamma)\cdot \widetilde{z}(\zeta \omega)+\alpha^2 L_1(\zeta)\notag\notag\\ &+ \alpha^6 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (\widetilde{w_4}(\zeta) + g\cdot \widetilde{w_3}(\zeta) + q_{prk3}(\zeta) - \widetilde{w_3}(\zeta\omega))^5\\ + g\cdot (\widetilde{w_4}(\zeta) + g\cdot \widetilde{w_3}(\zeta) + q_{prk3}(\zeta))^2\\ - (\widetilde{w_1}(\zeta) + g\cdot \widetilde{w_2}(\zeta) )\end{array}\right)\notag\\ &+ \alpha^7 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (g\cdot \widetilde{w_4}(\zeta) + (g^2+1)\cdot \widetilde{w_3}(\zeta) + q_{prk4}(\zeta) - \widetilde{w_o}(\zeta))^5\\ + g\cdot (g\cdot \widetilde{w_4}(\zeta) + (g^2+1)\cdot \widetilde{w_3}(\zeta) + q_{prk4}(\zeta))^2\\ - (g\cdot \widetilde{w_1}(\zeta) + (g^2+1)\cdot \widetilde{w_2}(\zeta))\end{array}\right)\notag\\ &+ \alpha^8 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (\widetilde{w_4}(\zeta) + g\cdot \widetilde{w_3}(\zeta) + q_{prk3}(\zeta) - \widetilde{w_3}(\zeta\omega))^5\\ + g\cdot (\widetilde{w_3}(\zeta))^2 + g^{-1} - \widetilde{w_1}(\zeta\omega) \end{array}\right)\notag\\ &+ \alpha^9 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (g\cdot \widetilde{w_4}(\zeta) + (g^2+1)\cdot \widetilde{w_3}(\zeta) + q_{prk4}(\zeta) - \widetilde{w_o}(\zeta))^5\\ + g\cdot (\widetilde{w_o}(\zeta))^2 + g^{-1} - \widetilde{w_2}(\zeta\omega) \end{array}\right)\notag \end{align}
$$

**Step 10: compute the opening proof polynomials**

Now we want to prove that the previous openings are correct, as well as $$r(X)$$ is actually vanishing in $$H$$. We first squeeze out a challenge $$v\in\mathbb{F}$$ from the sponge. This is done by showing that one can find a polynomial $$W_\zeta(X)$$ such that:

$$
W_\zeta(X) = \frac{1}{X-\zeta}\left(\begin{array}{l} \widetilde{w_1}(X) - \widetilde{w_1}(\zeta)\notag\\ +v(\widetilde{w_2}(X) - \widetilde{w_2}(\zeta))\notag\\ +v^2(\widetilde{w_3}(X) - \widetilde{w_3}(\zeta))\notag\\ +v^3(\widetilde{w_4}(X) - \widetilde{w_4}(\zeta))\notag\\ +v^4(\widetilde{w_o}(X) - \widetilde{w_o}(\zeta))\notag\\ +v^5(S_{\sigma 1}(X) - S_{\sigma 1}(\zeta))\notag\\ +v^6(S_{\sigma 2}(X) - S_{\sigma 2}(\zeta))\notag\\ +v^7(S_{\sigma 3}(X) - S_{\sigma 3}(\zeta))\notag\\ +v^8(S_{\sigma 4}(X) - S_{\sigma 4}(\zeta))\notag\\ +v^9(q_{prk3}(X) - q_{prk3}(\zeta))\notag\\ +v^{10}(q_{prk4}(X) - q_{prk4}(\zeta))\notag\\ +v^{11}(r(X) - r(\zeta))\notag \end{array}\right)
$$

and similarly, another polynomial $$W_{\zeta\omega}(X)$$ as follows.

$$
W_{\zeta\omega}(X) = \frac{1}{X - \zeta\omega}\left(\begin{array}{l} \widetilde{z}(X) - \widetilde{z}(\zeta\omega)\notag\\ +v(\widetilde{w_1}(X) - \widetilde{w_1}(\zeta\omega))\notag\\ +v^2(\widetilde{w_2}(X) - \widetilde{w_2}(\zeta\omega))\notag\\ +v^3(\widetilde{w_3}(X) - \widetilde{w_3}(\zeta\omega))\notag \end{array}\right)
$$

We commit these two polynomials as $$\mathsf{cm}_{\zeta}$$ and $$\mathsf{cm}_{\zeta\omega}$$.

**Step 11: output the full proof**

After the Fiat-Shamir transform, the final proof reads as follows.

$$
\left(\begin{array}{c} \mathsf{cm}_{w1}, \mathsf{cm}_{w2}, \mathsf{cm}_{w3}, \mathsf{cm}_{w4}, \mathsf{cm}_{wo},\\ \mathsf{cm}_{z}, \\ \mathsf{cm}_{t1}, \mathsf{cm}_{t2}, \mathsf{cm}_{t3}, \mathsf{cm}_{t4}, \mathsf{cm}_{t5},\\ \widetilde{w_1}(\zeta), \widetilde{w_2}(\zeta), \widetilde{w_3}(\zeta), \widetilde{w_4}(\zeta), \widetilde{w_o}(\zeta),\\S_{\sigma 1}(\zeta), S_{\sigma 2}(\zeta), S_{\sigma 3}(\zeta), S_{\sigma 4}(\zeta),\\ q_{prk3}(\zeta),q_{prk4}(\zeta), \widetilde{w_1}(\zeta\omega), \widetilde{w_2}(\zeta\omega), \widetilde{w_3}(\zeta\omega),\\ \widetilde{z}(\zeta\omega),\\ \mathsf{cm}_{\zeta}, \mathsf{cm}_{\zeta\omega} \end{array}\right)
$$

### Verifier

The verifier reads the full proof above and proceeds as follows.

**Step 1: compute all the challenges**

For convenience, the verifier first computes all the random challenges in this protocol execution: $$\beta$$, $$\gamma$$, $$\alpha$$, $$\zeta$$, $$v$$, and $$u$$.

* Initialize the same cryptographic sponge.
* Put $$\mathsf{cm}_{w1}, \mathsf{cm}_{w2}, \mathsf{cm}_{w3}, \mathsf{cm}_{w4}, \mathsf{cm}_{wo}$$ into the sponge and squeeze out $$\beta,\gamma\in\mathbb{F}$$ from the sponge.
* Put $$\mathsf{cm}_{z}$$ into the sponge and squeeze out $$\alpha\in\mathbb{F}$$ from the sponge.
* Put $$\mathsf{cm}_{t1}, \mathsf{cm}_{t2}, \mathsf{cm}_{t3}, \mathsf{cm}_{t4}, \mathsf{cm}_{t5}$$ into the sponge and squeeze out $$\zeta\in\mathbb{F}$$ from the sponge.
* Put $$\widetilde{w_1}(\zeta), \widetilde{w_2}(\zeta), \widetilde{w_3}(\zeta), \widetilde{w_4}(\zeta), \widetilde{w_o}(\zeta), S_{\sigma 1}(\zeta), S_{\sigma 2}(\zeta), S_{\sigma 3}(\zeta), S_{\sigma 4}(\zeta), q_{prk3}(\zeta), q_{prk4}(\zeta),\allowbreak \widetilde{w_1}(\zeta\omega),\allowbreak \widetilde{w_2}(\zeta\omega),\allowbreak \widetilde{w_3}(\zeta\omega), \widetilde{z}(\zeta \omega)$$ into the sponge and squeeze out $$v\in\mathbb{F}$$ from the sponge.
* Put $$\mathsf{cm}_{\zeta}$$ and $$\mathsf{cm}_{\zeta\omega}$$ into the sponge and squeeze out $$u\in\mathbb{F}$$ from the sponge.

**Step 2: compute** $$r(\zeta)$$

Recall from the Step 9 of the prover, $$r(\zeta)$$ can indeed be computed by the verifier.

$$
\begin{align} r(\zeta) &= -\mathsf{PI}(\zeta)+\alpha\cdot(\widetilde{w_1}(\zeta) + \beta S_{\sigma1}(\zeta) + \gamma) \cdot(\widetilde{w_2}(\zeta) + \beta S_{\sigma2}(\zeta) + \gamma)\cdot(\widetilde{w_3}(\zeta) + \beta S_{\sigma3}(\zeta) + \gamma)\notag\\ &\cdot(\widetilde{w_4}(\zeta) + \beta S_{\sigma4}(\zeta) + \gamma)\cdot(\widetilde{w_o}(\zeta)+\gamma)\cdot \widetilde{z}(\zeta \omega)+\alpha^2 L_1(\zeta)\notag\\ &- \alpha^6 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (\widetilde{w_4}(\zeta) + g\cdot \widetilde{w_3}(\zeta) + q_{prk3}(\zeta) - \widetilde{w_3}(\zeta\omega))^5\\ + g\cdot (\widetilde{w_4}(\zeta) + g\cdot \widetilde{w_3}(\zeta) + q_{prk3}(\zeta))^2\\ - (\widetilde{w_1}(\zeta) + g\cdot \widetilde{w_2}(\zeta) )\end{array}\right)\notag\\ &- \alpha^7 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (g\cdot \widetilde{w_4}(\zeta) + (g^2+1)\cdot \widetilde{w_3}(\zeta) + q_{prk4}(\zeta) - \widetilde{w_o}(\zeta))^5\\ + g\cdot (g\cdot \widetilde{w_4}(\zeta) + (g^2+1)\cdot \widetilde{w_3}(\zeta) + q_{prk4}(\zeta))^2\\ - (g\cdot \widetilde{w_1}(\zeta) + (g^2+1)\cdot \widetilde{w_2}(\zeta))\end{array}\right)\notag\\ &- \alpha^8 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (\widetilde{w_4}(\zeta) + g\cdot \widetilde{w_3}(\zeta) + q_{prk3}(\zeta) - \widetilde{w_3}(\zeta\omega))^5\\ + g\cdot (\widetilde{w_3}(\zeta))^2 + g^{-1} - \widetilde{w_1}(\zeta\omega) \end{array}\right)\notag\\ &- \alpha^9 \cdot q_{prk3}(\zeta)\left(\begin{array}{l} (g\cdot \widetilde{w_4}(\zeta) + (g^2+1)\cdot \widetilde{w_3}(\zeta) + q_{prk4}(\zeta) - \widetilde{w_o}(\zeta))^5\\ + g\cdot (\widetilde{w_o}(\zeta))^2 + g^{-1} - \widetilde{w_2}(\zeta\omega) \end{array}\right)\notag \end{align}
$$

**Step 3: assemble** $$\mathsf{cm}_r$$

The verifier can also assemble the commitment of $$r(X)$$ from available commitments, as follows.

$$
\begin{align} \mathsf{cm}_{r} &= \mathsf{cm}_{sat} + \mathsf{cm}_{r 1}\cdot \alpha - \mathsf{cm}_{r 2}\cdot \alpha + \mathsf{cm}_{r 3}\cdot \alpha^2\notag\\ &- Z_H(\zeta)\cdot(\mathsf{cm}_{t1} + \zeta^{n+2}\cdot \mathsf{cm}_{t2}+ \zeta^{2(n+2)}\cdot \mathsf{cm}_{t3}+ \zeta^{3(n+2)}\cdot \mathsf{cm}_{t4}+ \zeta^{4(n+2)}\cdot \mathsf{cm}_{t5})\notag\\ &+ \mathsf{cm}_{b} \cdot (\widetilde{w_2}(\zeta)\cdot (\widetilde{w_2}(\zeta) - 1)\cdot \alpha^3 + \widetilde{w_3}(\zeta)\cdot (\widetilde{w_3}(\zeta) - 1)\cdot \alpha^4 + \widetilde{w_4}(\zeta)\cdot (\widetilde{w_4}(\zeta) - 1)\cdot \alpha^5)\notag\\ &+ \mathsf{cm}_{prk1}\cdot q_{prk3}(\zeta)\cdot \alpha^6+ \mathsf{cm}_{prk2}\cdot q_{prk3}(\zeta)\cdot \alpha^7 \notag \end{align}
$$

where

$$
\begin{align} \mathsf{cm}_{sat} &= \widetilde{w_1}(\zeta)\cdot \mathsf{cm}_{q1}+\widetilde{w_2}(\zeta)\cdot \mathsf{cm}_{q2} + \widetilde{w_3}(\zeta)\cdot \mathsf{cm}_{q3}+ \widetilde{w_4}(\zeta)\cdot \mathsf{cm}_{q4}\notag\\ &+\widetilde{w_1}(\zeta)\cdot\widetilde{w_2}(\zeta)\cdot \mathsf{cm}_{m1}+\widetilde{w_3}(\zeta)\cdot\widetilde{w_4}(\zeta)\cdot \mathsf{cm}_{m2}+\mathsf{cm}_{qc} \notag\\ &+\widetilde{w_1}(\zeta)\cdot\widetilde{w_2}(\zeta)\cdot\widetilde{w_3}(\zeta)\cdot\widetilde{w_4}(\zeta)\cdot\widetilde{w_o}(\zeta)\cdot \mathsf{cm}_{ecc}\notag\\ &-\widetilde{w_o}(\zeta)\cdot \mathsf{cm}_o\notag \end{align}
$$

and

$$
\begin{align} \mathsf{cm}_{r 1} = &(\widetilde{w_1}(\zeta) + \beta\cdot \zeta +\gamma)\cdot (\widetilde{w_2}(\zeta) + \beta\cdot k_1\cdot \zeta +\gamma)\cdot (\widetilde{w_3}(\zeta) + \beta\cdot k_2\cdot \zeta +\gamma)\notag\\ &\cdot (\widetilde{w_4}(\zeta) + \beta\cdot k_3\cdot \zeta +\gamma)\cdot (\widetilde{w_o}(\zeta) + \beta\cdot k_4\cdot \zeta +\gamma)\cdot \mathsf{cm}_{z}\notag \end{align}
$$

and

$$
\begin{align} \mathsf{cm}_{r 2} =&(\widetilde{w_1}(\zeta) + \beta S_{\sigma 1}(\zeta) +\gamma)\cdot (\widetilde{w_2}(\zeta) + \beta S_{\sigma 2}(\zeta) +\gamma)\cdot (\widetilde{w_3}(\zeta) + \beta S_{\sigma 3}(\zeta) +\gamma)\notag\\ &\cdot (\widetilde{w_4}(\zeta) + \beta S_{\sigma 4}(\zeta) +\gamma)\cdot \beta\cdot \widetilde{z}(\zeta \omega)\cdot \mathsf{cm}_{\sigma o}\notag \end{align}
$$

and

$$
\begin{align} \mathsf{cm}_{r 3} = L_1(\zeta)\cdot \mathsf{cm}_{z} \notag \end{align}
$$

**Step 4: compute linear combination of commitments**

Let the cumulative commitment $$\mathsf{cm}$$ be as follows. Note that the last one has a coefficient $$u$$.

$$
\begin{align} \mathsf{cm} &= \mathsf{cm}_{w1} + v\cdot \mathsf{cm}_{w2} + v^2\cdot \mathsf{cm}_{w3} + v^3\cdot\mathsf{cm}_{w4} + v^4\cdot\mathsf{cm}_{wo}+v^5\cdot\mathsf{cm}_{\sigma 1}+v^6\cdot\mathsf{cm}_{\sigma 2} \notag\\ &+v^7\cdot\mathsf{cm}_{\sigma 3}+v^8\cdot\mathsf{cm}_{\sigma 4} + v^9\cdot \mathsf{cm}_{prk3} + v^{10}\cdot\mathsf{cm}_{prk4} + v^{11}\cdot \mathsf{cm}_r\notag\\ &+ u\cdot (\mathsf{cm}_{z} + v\cdot \mathsf{cm}_{w1} + v^2\cdot \mathsf{cm}_{w2} + v^3\cdot \mathsf{cm}_{w3})\notag \end{align}
$$

**Step 5: compute linear combination of evaluations**

Let the cumulative evaluation $$s$$ be as follows. Also, note the last one.

$$
\begin{align} s &= \widetilde{w_1}(\zeta) + v\cdot \widetilde{w_2}(\zeta) + v^2\cdot \widetilde{w_3}(\zeta) + v^3\cdot\widetilde{w_4}(\zeta)+ v^4\cdot\widetilde{w_o}(\zeta)+ v^5\cdot S_{\sigma 1}(\zeta)+v^6\cdot S_{\sigma 2}(\zeta)\notag\\ &+ v^7\cdot S_{\sigma 3}(\zeta) + v^8\cdot S_{\sigma 4}(\zeta) + v^9\cdot q_{prk3}(\zeta) + v^{10}\cdot q_{prk4}(\zeta) + v^{11}\cdot r(\zeta)\notag\\ &+ u\cdot (\widetilde{z}(\zeta\omega) + v\cdot \widetilde{w_1}(\zeta\omega) + v^2\cdot \widetilde{w_2}(\zeta\omega) + v^3\cdot \widetilde{w_3}(\zeta\omega))\notag \end{align}
$$

**Step 6: pairing**

Compute $$L, R$$ as follows.

$$
L = e((\mathsf{cm}_{\zeta} + u\cdot \mathsf{cm}_{\zeta\omega}), x\cdot H)
$$

where $$H$$ is the generator of $$\mathbb{G}_2$$ in the SRS and $$x$$ is the secret in the SRS. The element $$x\cdot H$$ here is part of the SRS.

$$
R = e((\zeta\cdot\mathsf{cm}_{\zeta}+u\cdot\zeta\cdot\omega\cdot\mathsf{cm}_{\zeta\omega}+\mathsf{cm} - s\cdot G), H)
$$

where $$G$$ is the generator of $$\mathbb{G}_1$$ in the SRS.

**Step 7: decision**

The verifier accepts the proof if $$L = R$$ and rejects otherwise.

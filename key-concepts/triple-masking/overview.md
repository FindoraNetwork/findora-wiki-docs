# Overview

The `Findora SDK` contains a `Triple Masking` API that enables developers to have access to the latest `Findora` privacy features include a fully secured transfer with zero visibility and full privacy.

Users can transfer funds from their _normal_ wallet to an _anonymous_ wallet. This process is called `bar to abar`.

When the `bar to abar` process is completed, the person who has access to the keys of that _anonymous_ wallet and the **special hash with the transfer information** (a.k.a _a commitment_) would be able to decode the information related to that transfer. That person could see their balance, use funds from it, transfer it back to the _normal_ wallet_,_ etc.

After funds are _converted_ (using `bar to abar`), they are fully secured and hidden under full privacy protection, which means no one can trace either the sender's _normal_ wallet information or the amount or type of the asset. It is fully secured, and the only way to retrieve that information and use those funds is to have both **the commitment** and **the anonymous wallet** information.

It is **critically** important to secure and protect this information; otherwise, funds would be completely lost without any option to recover it.

To receive funds from the _anonymous wallet_, the user needs to perform the _opposite (reversed)_ operation, which is called `abar to bar`. The user needs to provide the commitment, some pieces of the anonymous wallet information, and information about the normal wallet (where the funds should be transferred).

Both operations (and a few others, such as `abar to abar transfer`) are available in the `Findora SDK` via its `Triple Masking` API, please see the examples in the next chapters.

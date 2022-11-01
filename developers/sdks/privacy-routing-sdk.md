---
description: How to use privacy-routing-sdk
---

# Privacy Routing SDK

## How to use `privacy-routing-sdk`

You can use `privacy-routing-sdk` to transfer any FRC-20 asset (including FRA) on Findora Smart Chain from Address A to Address B, and remove the link between the two addresses. Both addresses can be classical user address or contract address.

{% embed url="https://github.com/FindoraNetwork/privacy-routing-sdk" %}

### Privacy Routing Overview

Below is a visual representation of the major flows when routing transactions which begins on the Findora EVM wallet through the Findora UTXO layer (to break the link between the sender and final Findora EVM wallet receiver).

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Privacy Routing SDK Process Flow</p></figcaption></figure>

Here is the process flow using the SDK's APIs:

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Privacy Routing API Call Flow</p></figcaption></figure>

### Asset Type on Findora Native Chain

* **BAR**
  * Transparent Asset
* **ABAR**
  * Shielded Asset (`{amount, asset type, address}` masked)

### Simple Steps to Use

First [clone](https://github.com/FindoraNetwork/privacy-routing-sdk) and add the SDK to your project.

> **Import SDK**

```typescript
// Use appropriate ways to importing the privacy-routing-sdk
import { Sdk } from "privacy-routing-sdk";
const { Sdk } = require("privacy-routing-sdk");
```

> **Initiate SDK**

```typescript
import { Sdk } from "privacy-routing-sdk";

const ENV_CONFIG = {
  hostUrl: "findora RPC",
};

// Initiating the SDK configuration
await Sdk.init(ENV_CONFIG);
```

### Supported Tokens

* **FRC20 (FRA token)**
* **FRC20 (Customized token)**
  * any FRC20 token on Findora EVM

### Findora EVM -> Findora EVM Transaction

Using **privacy-routing-sdk** for a complete confidential cross chain transaction by the following steps,

*   **(1) From `EVM compatible chain` to `Findora Native Chain`**

    * **Bridging FRC20(FRA token) to Findora Native Chain**

    ```typescript
    await evm.transfer.fraToBar({
      bridgeAddress: simBridgeAddress, // bridge contract address
      recipientAddress: "0x.....", // wallet account address
      amount: "100", // send amount
    });
    ```

    * **Bridging FRC20(Customized token) to Findora Native Chain**

    ```typescript
    /*
    Parameters
      bridgeAddress: simBridge contract address
      tokenAddress: FRC20 token address
      totalAmount: send amount
      recipientAddress: wallet account address
    */
    await evm.services.approveToken(tokenAddress, simBridgeAddress, tokenAmount);
    return await evm.transfer.frc20ToBar({
      bridgeAddress: simBridgeAddress,
      recipientAddress,
      tokenAddress,
      tokenAmount,
    });
    ```
* **(2) Converting Assets from `BAR` to `ABAR` in Findora Native Chain （entering confidential cycle）**

```typescript
import { findora } from "privacy-routing-sdk";

/**
Parameters
  sids: consumable utxo sids
*/
const walletWrap = await findora.keypair.getWallet();
findora.transfer.barToAbar(walletWrap, sids);
```

* **(3) Converting Assets from `ABAR` to `BAR` in Fidnora Native Chain （leaving confidential cycle）**

```typescript
import { findora } from "privacy-routing-sdk";

/**
Parameters
  commitments: consumable Abar utxo sids
*/
const walletWrap = await findora.keypair.getWallet();
findora.transferabarToBar(
  walletWrap.anonWallet,
  walletWrap.walletEnd,
  commitments
);
```

*   **(4) Bridging from `Findora Native Chain` to `EVM Compatible chain`**

    * Bridging **FRC20 (FRA token)** to Findora EVM

    ```typescript
    import { findora } from "privacy-routing-sdk";

    const walletWrap = await findora.keypair.getWallet();
    await findora.transfer.barToEVM(
      walletWrap.walletEnd,
      "100", // token amount
      recipientAddress, // recipient's address
      "",
      "",
      false
    );
    ```

    * Bridging **FRC20 (Customized token)** to Findora EVM

    ```typescript
    import { findora, evm } from "privacy-routing-sdk";

    const walletWrap = await findora.keypair.getWallet();
    const assetCode = await evm.services.getAssetCode(
      prismBridgeAddress,
      tokenAddress, // FRC20 token address
      findoraNetworkRpcUrl
    );

    await findora.transfer.barToEVM(
      walletWrap.walletEnd,
      "100", // token amount
      recipientAddress, // recipient's address
      assetCode,
      "",
      false
    );
    ```

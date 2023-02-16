---
description: Anonymous routing for every FRC20 transfer
---

# Privacy Routing SDK

### Introduction

`Privacy-Routing-SDK` provides simple and integration-friendly APIs for converting FRC20 transfers into anonymous transfers that break the link between senders and receivers. With just a small modification to your DApp's frontend, you can enhance your DeFi, Lending, or other project with privacy features.

### How It Works

`Privacy-Routing-SDK` is powered by zero-knowledge proof technology, allowing for the link between senders and receivers to be broken. The transfer can be completed in just four API calls&#x20;

1. **`depositFRC20()`** to deposit FRC20 tokens as a native asset in the ZK layer.
2. **`barToAbar()`** to wrap the native asset in an anonymous asset.
3. **`abarTobar()`** to unwrap the anonymous asset back to its native form.
4. **`barToEVM()`** to withdraw the native asset back to the EVM.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note: In Findora's native chain, transparent assets are represented as **BAR**, while shielded assets are represented as **ABAR**.
{% endhint %}

The privacy routing process starts with funds being transferred from the sender's EVM address to the privacy layer for privacy shielding, and then back to the receiver's EVM address. During the privacy routing process, one-time receiver addresses are dynamically created and the asset passes through the privacy layer. The key steps are **`barToAbar()`** and **`abarTobar()`**, where the asset is wrapped and unwrapped using one-time stealth addresses, thereby breaking the link between the sender and receiver. The next version of the Privacy-Routing-SDK will simplify the process even further by consolidating multiple API calls into one or two calls to reduce complexity.

### Quickstart Tutorial

Developers can take a look at the `Privacy-Routing-SDK` example on Github.

{% embed url="https://github.com/FindoraNetwork/privacy-routing-sdk-example" %}

{% hint style="info" %}
Note: Privacy-Routing-SDK is now available only on the Findora **Forge** Testnet. See [network settings](../../network-settings/network-settings.md) for RPC details and request **Forge** EVM testnet `FRA` tokens [here](../../general-user-materials/acquire-fra/request-fra-testnet.md).
{% endhint %}

### DeFi Integration

The Findora `Privacy-Routing-SDK` is designed as a general tool for FRC20 tokens and can be integrated into various projects in different ways. In the context of DeFi, the simplest way to integrate the SDK is by adding it to the frontend without modifying the smart contracts.

As an example, let's consider **PancakeSwap** and a scenario where a user wants to swap 10 USDT to 9.98 USDC on the frontend page. The following are the adjusted steps for this scenario

**Step 1: Routing:**

* User address is: `0x661746C36C4379B5994d9883f3bFf662b711Be76`
* Call **`depositFRC20()`** to deposit 10 USDT as a native asset in the privacy layer.
* Call **`barToAbar()`** to wrap the native asset (10 USDT) in an anonymous asset.
* Call **`abarTobar()`** to unwrap the anonymous asset (10 USDT) back to its native form.
* Call **`barToEVM()`** to withdraw the native asset (10 USDT) back to an EVM one-time address.
* One-time receiver is: `0x7366F30D830048dFD947662d92421807bcB7Fdd3`

Upon completion of the privacy routing process, the link between the user address and the one-time receiver address holding 10 USDT is cut off.

**Step 2: Swap:**

* Switches to one-time receiver account: `0x7366F30D830048dFD947662d92421807bcB7Fdd3`.
* Performs a normal swap of 10 USDT to 9.98 USDC.
* Final receiver address doesn’t really matter. It could be the original user address `0x661746C36C4379B5994d9883f3bFf662b711Be76` , or it could be a different address.

The private swap is now complete.

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

### The APIs

Using `Privacy-Routing-SDK` for a complete anonymous routing in 4 steps

*   **(1) Send assets From `Findora EVM` to `Findora Native Chain`**

    * Send **FRA** token to Findora Native Chain

    ```typescript
    await evm.transfer.fraToBar({
      bridgeAddress: simBridgeAddress, // bridge contract address
      recipientAddress: "0x.....",     // wallet account address
      amount: "100", // amount
    });
    ```

    * Send **FRC20** token to Findora Native Chain

    ```typescript
    /**
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
* **(2) Convert assets from `BAR` to `ABAR` in Findora Native Chain (entering anonymous cycle)**

```typescript
import { findora } from "privacy-routing-sdk";

/**
Parameters
  sids: consumable utxo sids
 */
const walletWrap = await findora.keypair.getWallet();
findora.transfer.barToAbar(walletWrap, sids);
```

* **(3) Convert assets from `ABAR` to `BAR` in Findora Native Chain (leaving anonymous cycle)**

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

*   **(4) Withdraw assets from `Findora Native Chain` to `Findora EVM`**

    * Withdraw **FRA** token to Findora EVM

    ```typescript
    import { findora } from "privacy-routing-sdk";

    const walletWrap = await findora.keypair.getWallet();
    await findora.transfer.barToEVM(
      walletWrap.walletEnd,
      "100", // amount
      recipientAddress, // recipient's address
      "",
      "",
      false
    );
    ```

    * Withdraw **FRC20** token to Findora EVM

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
      "100", // amount
      recipientAddress, // recipient's address
      assetCode,
      "",
      false
    );
    ```

### Boilerplate settings

```typescript
import { Sdk } from 'privacy-routing-sdk';
import Web3 from 'web3';

export const ENV_CONFIG = {
  hostUrl: 'https://prod-forge.prod.findora.org',
  feeServerUrl: 'https://forge.invisiblex.org/api/fee',
  configServerUrl: 'https://columbus-config.s3.us-west-2.amazonaws.com/columbus_config_forge.json',
  navticeExplorerUrl: 'https://forge.findorascan.io/',
};

export const FINDORA_EVM_CHAIN_ID = '2154';

Sdk.init({ ...ENV_CONFIG, web3: new Web3(Web3.givenProvider) });
```

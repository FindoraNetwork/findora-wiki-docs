---
description: Setting up and funding your Findora Desktop Wallet
---

# 💰 Testnet Wallet Setup/Funding

{% hint style="danger" %}
If you already have a Findora wallet, **export your private keys** before downloading the testnet wallet. This is best practice and allows you to recover your wallet if anything happens.
{% endhint %}

{% hint style="info" %}
If your Findora wallet is using v0.3.4, and already have the Anvil testnet network added, you will encounter issues during the campaign. **Please make sure to delete the Anvil network from your v0.3.4 wallet** before installing the testnet wallet.
{% endhint %}

### Testnet Wallet Install & Setup

**1.** Visit[ findora.org/testnet](https://www.findora.org/testnet). Download and install the testnet wallet. If using MacOS, you may need to adjust your security settings to install the wallet.

<figure><img src="../../../../.gitbook/assets/downloadWallet.jpg" alt=""><figcaption><p>Download the Testnet Wallet</p></figcaption></figure>

**2.** Click "Settings", then click "Manage" under the Network category, then add the Anvil network.

<figure><img src="https://lh4.googleusercontent.com/ahwYadv3dXQLNBWFnwTQArGKZOIdWuGzI0AC2-MF3Fz6EFUIsVqh6CVsgui1TwEXc9Zm5FZA_4PPUic0oIVglFwSkeaGzJBI5E54F8L5jRZ6TGOUknoLsteb69SiwZZfCrZRfBtDsbIl5dUrAH0Hmzo" alt=""><figcaption><p>Adding Anvil testnet to the wallet.</p></figcaption></figure>

**Anvil network details below:**

| Network Node Nickname   | Anvil                                 |
| ----------------------- | ------------------------------------- |
| Network Node URL        | https://prod-testnet.prod.findora.org |
| Blockchain Explorer Url | https://prod-testnet.findorascan.io   |



**3.** Create two new UTXO wallets in the Findora Testnet Wallet application. You will need to use these two addresses throughout the campaign and for registration.

{% hint style="warning" %}
**Do not import mnemonic or private keys that own mainnet assets.**
{% endhint %}

<figure><img src="https://lh5.googleusercontent.com/CfrI5c-6qp5KkvJX6cJzPEvIJeYfXGoQwbTx1wXYjjlfLe5ns2EJRDO_bT0gTqQHs71VQf5UJKxdGe_0bUVaI1AFWOctpX8nmhNAdk6TBZsRYMHyjoW_nVmmQbtJTWr9c-8aMgZPgLMFmEm5MNq0X7c" alt=""><figcaption><p>Adding Two UTXO Wallets to the Findora Testnet Wallet App</p></figcaption></figure>

**4.** Open your Metamask wallet and add the Anvil testnet network.

**Anvil network details below:**

| Network Name       | Anvil                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------- |
| RPC URL            | [https://prod-testnet.prod.findora.org:8545](https://prod-testnet.prod.findora.org:8545) |
| Chain ID           | 2153                                                                                     |
| Block explorer URL | https://testnet-anvil.evm.findorascan.io                                                 |

<figure><img src="../../../../.gitbook/assets/testnet on MM.jpg" alt=""><figcaption><p>Adding Findora's Anvil Network to Metamask</p></figcaption></figure>

### Wallet Funding

{% hint style="info" %}
You will need FRA tokens in Metamask and the Findora Testnet Wallet for gas fees.
{% endhint %}

**1.** Visit[ Findora Faucet](https://faucet.findora.org/) to receive testnet FRA-EVM tokens. **Enter your 0x... address** to claim them in your Metamask wallet.

<figure><img src="https://lh4.googleusercontent.com/HU9P3Qbjd3CvF5eiu55EF0I31xCUIe3Ikds9zIE0_fwrlQPWmZyGgA46CD77g1qsZPh-96Ratq1GQ6DU1Km0Utjcex9pBc5xhnoHCvZSjCL8cHCrlaaiemZFJ3-tSw2W86e0IcxRiRyvttABKZml9cI" alt=""><figcaption><p>Claiming Testnet FRA Tokens</p></figcaption></figure>

**2.** Open your Metamask wallet, select the Anvil network, and ensure your testnet FRA is received.

**3.** Open the Findora Testnet Wallet, click on Prism++, and then click "Select Wallet".

**4.** Import the private key to your EVM wallet and click Confirm.

<figure><img src="https://lh5.googleusercontent.com/aFYGy37jdixnHrb_TD_0BKtXWu6Ns0ExBLVcn3lzbvt9tjGay0amCA9xoeRh8E2JCQ6OjFxoaWk5sAahXoohydcxdI6HtRQsu0_u_jLEo51YW3w2NA1L2zXZyZ1ddjtJQv0CRsxRLHH6qUI-iLquZTQ" alt=""><figcaption><p>Adding an EVM Wallet to Findora Testnet Wallet</p></figcaption></figure>

{% hint style="info" %}
By importing your private key from Metamask, Prism++ will have the ability to bridge testnet assets from EVM to UTXO in later steps.
{% endhint %}

**5.** Set the direction to EVM-Compatible Wallet **>>** Native Wallet.

Then choose FRA as the Asset Type.&#x20;

<figure><img src="../../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Setting Direction and Choosing the Asset Type</p></figcaption></figure>

{% hint style="info" %}
Make sure to find **both** of your two UTXO wallets with FRA tokens.
{% endhint %}

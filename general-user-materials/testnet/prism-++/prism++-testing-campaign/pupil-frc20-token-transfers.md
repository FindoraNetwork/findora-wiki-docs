---
description: Second stage of the Prism++ testnet campaign. Transferring FRC20.
---

# 🧒 Pupil: FRC20 Token Transfers

For the Pupil, Pilgrim, and Prodigy badge, you will need to complete a Prism++ Transfer loop FRC20, FRC721, and FRC1155 tokens, respectively.

<figure><img src="../../../../.gitbook/assets/prism++ loop (1).png" alt=""><figcaption></figcaption></figure>

**In this stage you will:**

a. Obtain FRC20 testnet tokens to your Metamask.

b. Transfer these tokens to your Findora Testnet Wallet app using Prism++.

c. Initiate a confidential transfer from UTXO wallet 1 to UTXO wallet 2 and back.

d. Transfer these tokens back to your Metamask using Prism++.

### Fund your EVM Wallet with FRC20 Tokens

**1.** Visit the [Findora Testnet Faucet](https://faucet.findora.org/) to receive FRC20 testnet tokens to Metamask.&#x20;

<figure><img src="https://lh6.googleusercontent.com/WgeVQy1puAaiufuSwVJJmY4R02YaZMhQTvJjqfItpTB4c0ugNo3-8vPsw7hxeYnUpjp7jpA9xkWbMbPAezYPvXdmOLf-mBlTmZ-tfEjZMN5JA_D9TWJ5emWRqVpDdHvqOVbrFxJiCCFQ828BukTq7jg" alt=""><figcaption><p>Claim FRC20 tokens on the Findora Testnet Faucet</p></figcaption></figure>

**2.** To view the tokens, add FRC20 via Import Tokens on Metamask.

{% hint style="info" %}
**FRC20 contract address**: 0x0066dDAE5A510Bc751947057D2155783c9DdE1A6
{% endhint %}

{% hint style="info" %}
Token Decimal: 6
{% endhint %}



<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Import FRC20 to Metamask</p></figcaption></figure>

### Transfer Your FRC20 Tokens Using Prism++ (EVM->Native)

**1.** In the Findora Wallet, click the Prism++ tab and set EVM wallet to Native wallet as the direction.&#x20;

**2.** Select your the EVM wallet and then select your 1st UTXO Wallet.

{% hint style="info" %}
If you haven't imported your Metamask private key, see the [Testnet Wallet Setup ](testnet-wallet-setup-funding.md)page for help.
{% endhint %}

<figure><img src="https://lh6.googleusercontent.com/UUz_ThmzLXC16UsFygIGeYXZm50Z-R_EJa49heMnB2SRoQurmNSGrtkOdxzqj_oYCr44Kz0Dg9u7agFfMf-T6uf1Nzmuk2ZoEM0rPAZRCqWwIJS7_62DJ8j3aVGsJB_Ml5K3UzbX_ooafYbTUK1vWPs" alt=""><figcaption><p>Prism++ | Setting Direction and Selecting the EVM and UTXO Wallets</p></figcaption></figure>

**3.** On the same screen, click Asset Type and then paste the FRC20 contract address below: 0x0066dDAE5A510Bc751947057D2155783c9DdE1A6. **Click "Findora Faucet" in the search results.**

<figure><img src="https://lh3.googleusercontent.com/7Al7RrJC3quvmHplpTszCg-YipyHXdqYIHWhHDQfpD1iJ07b8DXAQ09p0cfplD-_HJr-6fITtqaQE7gTKupYIG7vOlDfWLrARnKkWLL8_b-k9GJjfYyTvxZFFjCgaN3bYB8L6PDobtt_bVy3oFwLSVo" alt=""><figcaption><p>The address in the screenshot is an old contract address. Use the one in the documentation</p></figcaption></figure>

**4.** Set the amount to any value below maximum available (10 for example).

**5.** Finish the Prism++ transfer by **clicking Next then Submit**.

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption><p>UTXO Wallet, Asset Type, EVM Wallet, and Amount.</p></figcaption></figure>

### Confidential Transfer Your FRC20 Tokens (UTXO1->UTXO2)

**1.** Input your native wallet address (UTXO Wallet 1) and the amount.&#x20;

<figure><img src="https://lh4.googleusercontent.com/beIBJYnU5l5TdgxDx-T_F8jWPKooek14Q6jgVdKZhUBZSqLqOov3KTYWNgfYOIQslUiHTZJKaTb_wHeZ0-GmBGMK3C321pnRlMrmxSszszoVjrxBV6xbLBIcohn6MLSDGRSsOhDsKbVNelS_hy-wc18" alt=""><figcaption></figcaption></figure>

**2.** On Send tab, perform the confidential transfer for the FRC20 token from UTXO Wallet 1 to UTXO Wallet 2. Findora Desktop Wallet supports confidential transfer to help you customize the level of privacy you prefer for your transfers. To complete the Campaign Tasks, please perform a fully Confidential Transfer in which you hide both the "Asset Type' and the "Asset Amount" of the transaction. You won't be able to see the transaction details (of this transfer) on the Findora Block Explorer.&#x20;

<figure><img src="https://lh4.googleusercontent.com/ucO-07BLaIHNElmVpUTHZUBHqF7f0PbsBiuc8JjvsGfO4mER-TpD6tfnxhXNv7u5VlXpvQUTOaGSS7MS9UNBsdnIhLjSNROQP5O1Jmc5ErLzC--O4L-1xJgKU7229sqaG8FwMty9KsgQ9Sn2uovUrOE" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/bnR6PXICduhPlguWDU-_pyjH1-tdNe0qZ-aFa7JyiLKFc8KBHbjyH4rFxLMzUwBcqUcHhp5uMzqh1P5IM071an-tpgNgNPzw9bojf4r8OskNl468jGxb7YRfkIeDQ-PcubVKgNtnVXGC_V4mrN-f8nw" alt=""><figcaption></figcaption></figure>

**3.** Open the Manage Assets tab, and copy the FRC20’s asset code. Then click the Add button.

<figure><img src="https://lh4.googleusercontent.com/b66WRl56SO__0o0Fm13rLGpNuZY3BcA3hemiveJHAmhHExsE2Y0jOBTHCHGR0sfXBGAgwpi9uor_0nzoWn18IiEzk73as07zr2h0KQdY8rsWqqQRbFyu5Y7pI_-lZs1x41PoVC8jBNT1ec-nNwCDb4k" alt=""><figcaption></figcaption></figure>

**4.** Add the asset to your UTXO wallet 2.

<figure><img src="https://lh4.googleusercontent.com/jrNQxX4bgyc1CLWF0L9bG_8RhlNCZC1u_krKIz7CNrLJVZZB4Qqxu3vcJV4Ewl29PSlyo5Rs3Nwv6E5-PzpQHFR9wUxdfxkHtojNrj_dGax-B1xl1XWm3SOSavfvuczCxk0olLmP27GucnS4ULXEGTk" alt=""><figcaption></figcaption></figure>

### Prism++ Your FRC20 Tokens (Native->EVM)

**Use Prism++ to transfer the FRC20 token back to your EVM wallet.**

<figure><img src="https://lh4.googleusercontent.com/blXW0ZFkJc-oITgnC4mVkudnolcWj7C6bD-NAoY0nRb9aXIep5YBtr0w9Pf0O7bsyHzlmtBcl74h049XSgPvIUSj8vzGzTRqw9v-3kTBgE-AfNP6UB0Ir3wO15pCuhxaKD5E4xVmLsH8GQNj3xIixxk" alt=""><figcaption></figcaption></figure>

\
\
\

# Triple Masking

Triple Masking supports users to hide their addresses in transactions, and you can download the demo to quickly complete an anonymous transfer.

{% hint style="info" %}
Triple Masking Demo is only used on the testnet
{% endhint %}

#### 1. According to your computer system, download the testnet demo installation file from [findora.org/testnet](https://findora.org/testnet).

<figure><img src="https://lh6.googleusercontent.com/ArQBL4Btw4n20upAaB1FYeYfapNduYWjtgsHA3D1MlPfOSS6CpDF9t3bIwf8CzbGfNCI_aBj2mRvJppy1FQC43D-m_Sws--sPLL-mku61vLS0Yw6QGnyFZlW1d8Av1JttOE1eLl8Or8hIhdAIRQ9KgY" alt=""><figcaption></figcaption></figure>

#### 2.Select the qa02 network in Wallet's Settings.

| Name            |                                                               |
| --------------- | ------------------------------------------------------------- |
| **node**        | https://dev-qa02.dev.findora.org                              |
| **explorer**    | http://qa02-findorascan-io.s3-website-us-west-2.amazonaws.com |
| **evm**         | https://dev-qa02.dev.findora.org:8545                         |
| **evm-chainId** | 2222                                                          |

#### 3.Click the create button to create a transparent wallet and an anonymous wallet.

<figure><img src="https://lh6.googleusercontent.com/ous-bOBQhsCtWTGhkfZNe-PTZB1sPfYeSHqmcJHwzaLf4YYg5MO1IBoYMKTCIfkt344lYH0LSB7-aXaqdy9Frm0385TN1yCl3V-SBLK5G4CCiUiGZZb1cb3S55CNyfu2hNKoW_pD4ZyEu1hhGlj8rSE" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh5.googleusercontent.com/40BjKlB-fG9t5VUhQNaJA2M_Pf1ZeNabFo3yclBKgbebvxGExchfsFGHBhl-ifBZDOH6Ps1Q5TJ0UGjIzHIbykobHRSZ0Bvq-QS3N60KKp-z6E66KoKEpirGaCedaE_vMCNT9AxtGEyhWzvWipsr8jY" alt=""><figcaption></figcaption></figure>

#### 4. Visit [faucet](https://faucet.findora.org) website and get qa02 FRA native token

#### 5. Enter the "send" page on the wallet. Select a Transparent Wallet in the "from" box, and select an Anonymous Wallet in the "to" box. Then, enter the amount for transfer. When you choose to send tokens from Transparent Wallet to Anonymous Wallet, the Privacy Options are all selected by default.

\


![](https://lh5.googleusercontent.com/wC69GLJSenLuzNYfC9M3JuGTFf3BSyqYQ8Lek8jd--2aR1YMlUHZdWkABa7le6-DVf9CJkiXaYhCa7W4Q0vL7Pvjl-FhoLecrxKxNED6e45bSuOk80FgXwywX1p6GlasGY4KNvMaOzFDQwoaCYQPdY4)

Here is a table explaining the privacy options for different wallet transfers.

{% hint style="info" %}
**T**:Transparent Wallet

**A**:Anonymous Wallet
{% endhint %}

| Operation | Hide Amounts | Hide Asset Type | Hide Address |
| --------- | ------------ | --------------- | ------------ |
| T to T    | Y/N          | Y/N             | N            |
| T to A    | Y            | Y               | Y            |
| A to T    | Y            | Y               | Y            |
| A to A    | Y            | Y               | Y            |

#### 5.Click Submit button, and your transaction will be submitted to the network

<figure><img src="https://lh5.googleusercontent.com/Oyz1ltWaMpTb-Yo_PkdoiEwF-KY4kUDZE4L6_fSFjbMMcVWPmNk7RZdoOmUggs3HhIyUFT_Gpr3n6KGeu9UAT1-KgsQS8aJQyzA4lD9n8UuEBOSAUGvRx5xD1Q5-R9zXq8ti8RrK1niB9bVbIcvzBeY" alt=""><figcaption></figcaption></figure>

#### 6. Check the Anonymous Wallet and the FRA will be transferred from the transparent wallet

<figure><img src="https://lh6.googleusercontent.com/emXCSyEXMQ7LvewBO_w9zWz8EZjgEQ8MNNcy3--s8x3OchtO0eTTxS6fUx7hsHgpR8ZeFTRvThZswiaCOHUZ7UuynidDEKEB434gkMUyL9FNcMvYIHyQpvCxfXV2Pc8g1h4l7MO9DmuSwEpPdihVLiI" alt=""><figcaption></figcaption></figure>

#### 7.We create a new Anonymous Wallet2 again

<figure><img src="https://lh5.googleusercontent.com/4h4mfRRNIRsaOYBfVIGtVSjAlmDWdYJzH0giBJM0jdpt-NAZ5gfU3b-ngy3R2poQ58awVnoRB89bHHiXPxOdOzprjVx7xo5WeI1QJF2B1hzcVwG_LvWbdMXy1VtCHIqRtDn5_nIvzQ8dgCgEXJ79eHI" alt=""><figcaption></figcaption></figure>

#### 8.Enter the send page again. This time, we select Anonymous Wallet1 in from, and Anonymous Wallet2 in to. After clicking next, we find that the gas has changed.&#x20;

{% hint style="info" %}
#### The detailed calculation for the gas fee method is as follows:



_<mark style="color:blue;">**50\_0000 + 10\_0000 \* x + 20\_0000 \* y + (10\_000 \* extra\_outputs)**</mark>_

\- x is no.of inputs and y is no.of outputs.

\- extra\_outputs = y-x (if y>x).

\- Fee deducted implicitly. No separate fee op required.

\- An extra output is created for remainder of each asset type and that is incl in the fee formula as well\

{% endhint %}

<figure><img src="https://lh4.googleusercontent.com/qG4AE2nsL7HeYKbvYYZ0w-StuiS52G6bO53HWx1YmyjlWJhJm3oej4N0xscJAWBgU615ffBLJm46ICuQnK_tAzxeahk2rTf5pciSsEr_CCjSZm1G4NIgqX-D_Ksdgdz6EjjadKKnMolThXlirwqn334" alt=""><figcaption></figcaption></figure>

#### 9.After click the submit button, we need to wait for a while.Then check this transaction in the block explorer. Both the receiver and the sender of this transaction are hidden. Congratulations, you have completed a Triple Masking transaction.

<figure><img src="https://lh4.googleusercontent.com/8r8YUKcKy_0Jwb69xeVK7WihdctUKZ5d_ZMJcciPMxE__SwitB1D8G416VD8Im7dC9k3Gc3_3WS6IWq7PA5b-hpi4HfWU71Rjq-Ey4p73dLW_SIbeP2uK5RlG1Hvfy4-Dqq2_fVUCivPS1DuL2h0vjk" alt=""><figcaption></figcaption></figure>

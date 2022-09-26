# Rialto Bridge User Guide

### Overview[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#overview) <a href="#overview" id="overview"></a>

Rialto is a bidirectional bridge that connects Findora to other EVM-compatible blockchains. This guide will walk you through how to configure the bridge to move assets from Binance Smart Chain (BSC) to Findora while using your Metamask Wallet.

Below are the key steps to move assets over from a source network (such as BSC) to a destination network (such as Findora).

### Step-by-Step Instructions[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#step-by-step-instructions) <a href="#step-by-step-instructions" id="step-by-step-instructions"></a>

#### Step 1: Configure Metamask for both BSC and Findora[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#step-1-configure-metamask-for-both-bsc-and-findora) <a href="#step-1-configure-metamask-for-both-bsc-and-findora" id="step-1-configure-metamask-for-both-bsc-and-findora"></a>

Goto Metamask’s “Add Network” screen and configure Metamask to connect with BSC using the settings below:

![BSC Network Settings on Metamask](https://wiki.findora.org/assets/images/metamask-1-acd5ccecc4421e515f4c8b8424392f7a.png)

Next, goto Metamask’s “Add Network” screen again and configure Metamask to connect with Findora using the settings below:

![Findora Network Settings on Metamask](https://wiki.findora.org/assets/images/metamask-2-05f5b8a942d4b9be8c7c7409e44544aa.png)

[Check this link](../../network-settings/network-settings.md) for more details on Findora Mainnet network configuration

#### Step 2: Fund Metamask with BNB Tokens[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#step-2-fund-metamask-with-bnb-tokens) <a href="#step-2-fund-metamask-with-bnb-tokens" id="step-2-fund-metamask-with-bnb-tokens"></a>

Rialto bridge transactions whose assets originate from BSC must pay BNB gas fees on the BSC side of the bridge. Thus, you must first buy or transfer BNB tokens into your BSC Mainnet Metamask wallet. If you don’t have BNB tokens, you can buy them from an exchange like Binance.com or any of the exchanges listed on [this page](https://coinmarketcap.com/currencies/bnb/markets/).

Special Note: If you are a developer using the testnet version of Rialto bridge, you can get testnet FRA from the [Findora Discord #faucet channel](https://discord.gg/4u26QR3N6h). To learn more about how to claim the tokens, [checkout this guide](../get-fra/request-testnet-fra.md).

#### Step 3: Transfer Tokens Across Bridge[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#step-3-transfer-tokens-across-bridge) <a href="#step-3-transfer-tokens-across-bridge" id="step-3-transfer-tokens-across-bridge"></a>

* Goto [rialtobridge.io](https://rialtobridge.io/) and connect your BSC Metamask wallet.
* Next set the “Source Network” to BSC.
* Enter the token type and token amount you wish to send from BSC to Findora.
* Enter your destination (Findora) wallet address and click “Start Transfer”.

To send the funds to the same destination wallet address (i.e. set both sending BSC address and receiving Findora address to the same value), click the “I want to send funds to my address” checkbox.

![Rialto Bridge - Setup Tokens to Bridge Over](https://wiki.findora.org/assets/images/rialto-1-281560648af203a1633a1853046154a0.png)

#### Step 4: Confirm Metamask Transaction[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#step-4-confirm-metamask-transaction) <a href="#step-4-confirm-metamask-transaction" id="step-4-confirm-metamask-transaction"></a>

Metamask will ask you to confirm your transaction. Click “Confirm” on the screens below.

![Metamask - Confirm Access Permissions](https://wiki.findora.org/assets/images/metamask-3-f218375d987f0b61ab5582cfef2acd6d.png)

Confirm on the screen below as well:

![Metamask - Confirm Transaction](https://wiki.findora.org/assets/images/metamask-4-ef54ae27aa09b5f9ae53e946fe1f07bb.png)

#### Step 5: View Transaction Details on EVM Block Explorer[​](https://wiki.findora.org/docs/evm\_guides/rialto/rialto-guide#step-5-view-transaction-details-on-evm-block-explorer) <a href="#step-5-view-transaction-details-on-evm-block-explorer" id="step-5-view-transaction-details-on-evm-block-explorer"></a>

To view the completed bridge transaction log, goto evm.findorascan.io. Enter your wallet address into the search bar at upper right of the block explorer and hit enter. Next, click on the “Token Transfers” tab and look for the “Token Minting” success message. A successful bridge transaction will lock your token on the BSC side of the bridge and mint a new, corresponding token on the Findora side of the bridge.

![Findora EVM Block Explorer - Confirm Transaction Success](https://wiki.findora.org/assets/images/block-explorer-1-be890c0800efe1197e743a98cb69b2dc.png)

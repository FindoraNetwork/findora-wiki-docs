---
description: Installing Findora Validator via the Toolbox
---

# Toolbox Setup

This guide is for installing the Validator Toolbox software which you can then use to install and manage a Findora Validator.

## Existing Validators

Toolbox will install on existing validators as well. Since you already have a user account and docker, you're good to skip ahead to [pull script & run installer](toolbox-setup.md#pull-script-and-run-installer) to setup the management menu. After that use the [normal launch command](toolbox-setup.md#launching-toolbox) to check for updates and run the menu each time.

## Pre-Installation Tasks

### Server Selection

You will need a computer/server running 24/7 to run Findora Validator code.

{% embed url="https://docs.findora.org/validator-materials/node-setup-guides/system-requirements" %}
System Requirements
{% endembed %}

## Server Prep

{% hint style="info" %}
If your provider supports `cloud-init` scripts, you can script the setup of the next few steps instead of running them manually.
{% endhint %}

### Setup A User Account

It is suggested to run your application as a user account and not as `root` directly. You can find our guide on setting up a user account in our Manual Setup guide below.

{% embed url="https://docs.findora.org/validator-materials/node-setup-guides/manual-setup#adding-a-user-account" %}
User Account section of the Manual Setup Guide
{% endembed %}

### Docker Installation

Install Docker on your server following the instructions in our Manual Setup guide below.

{% embed url="https://docs.findora.org/validator-materials/node-setup-guides/manual-setup#step-2-install-docker" %}
Docker Installation section of the Manual Setup Guide
{% endembed %}

### Firewall Setup

Firewall types vary depending on OS and provider. Here are the ports required to be open for Findora. Port 22 is for SSH, the rest are for the Findora docker container.

```
22
8545
8667-8669
26657
```

## Pull script & Run Installer

Once you've logged back in and your user is in the docker group, run the following code to install the toolbox and begin installation on either mainnet or testnet.&#x20;

Our menu will launch and ask you a few simple questions to get you fully loaded and online:

{% tabs %}
{% tab title="Start Installer" %}
```bash
cd ~/ && wget https://raw.githubusercontent.com/FindoraNetwork/findora-toolbox/main/src/bin/findora.sh && chmod +x findora.sh && ./findora.sh --installer
```
{% endtab %}
{% endtabs %}

The installer will pull the installation script and get everything setup. At the end of the installer you'll have a fully working validator syncing up to the blockchain on a brand new tmp.gen.keypair and priv\_validator\_key.json file.&#x20;

These are usable as wallets but are also disposable still at this point. You can test out all the functions of a Findora server now as long as you don't run the staking and creation commands.

## After Installation

{% hint style="info" %}
At this point you'll have a system that begins syncing automatically on the blockchain after the database download and unpacking completes. Wait for your `sync_status` to equal false before creating your validator or migrating to a new system.
{% endhint %}

Run the following commands and ensure they return status messages without errors. Your node has been successfully configured and started if no errors are displayed.\
\
Line 1 is used to see your current sync status, you will want to save it for re-use. Lines 2-4 simply show version numbers but should also reply at this time without error.

{% code lineNumbers="true" %}
```
curl 'http://localhost:26657/status'
curl 'http://localhost:8669/version'
curl 'http://localhost:8668/version' # Only if you set the 'ENABLE_LEDGER_SERVICE'
curl 'http://localhost:8667/version' # Only if you set the 'ENABLE_QUERY_SERVICE'
```
{% endcode %}

### Launching Toolbox

Anytime you would like to run the full toolbox menu we suggest pulling updates and then launching the application.&#x20;

The code below works for either `testnet` or `mainnet` toolbox. Here's a string of code you can run to update and start the toolbox again:

```bash
cd ~/ && ./findora.sh
```

### Backup Files

Toolbox copies all files you need to backup into the folder `~/findora_backup` every time you launch it.

Save this folder somewhere safe and always keep it private. You will need it for recovery or migrating servers.

Here's a list of files you'll need to migrate to a new server that we include:

{% tabs %}
{% tab title="mainnet" %}
{% code lineNumbers="true" %}
```bash
~/tmp.gen.keypair
/data/findora/mainnet/node.mnemonic
/data/findora/mainnet/mainnet_node.key
/data/findora/mainnet/tendermint/config/
```
{% endcode %}
{% endtab %}

{% tab title="testnet" %}
```
~/tmp.gen.keypair
/data/findora/testnet/node.mnemonic
/data/findora/testnet/mainnet_node.key
/data/findora/testnet/tendermint/config/
```
{% endtab %}
{% endtabs %}

## New Validators

### Complete Validator Creation

If you're just installing your validator for the first time you still need to fund your wallet, stake your FRA, start your validator and backup your private key files. \
\
At this point you can follow the rest of the manual guide starting from the step below to find your address, deposit your 10k+ starting stake, and sign the transaction to stake and start validating.

{% embed url="https://docs.findora.org/validator-materials/node-setup-guides/manual-setup#step-8-check-signing" %}

## Existing Validators

If you'd like to migrate your keys to the new server you can do that easily now at this time!&#x20;

You'll need to import a few files onto the new server and then **be sure to shut off the old server** before starting the new server with your old keys to avoid **double signing slashing (5% from your pool)**.&#x20;

{% hint style="danger" %}
_**The slashing fee for Missing Blocks is far less and easier to explain than getting slashed for 5%.**_
{% endhint %}

### Backup Recovery Files

If you use the Toolbox on your old server currently, it copies all files you need to backup into the folder `~/findora_backup` every time you launch it.

If you're not using the validator toolbox here's a list of files you'll need to migrate to a new server:

{% tabs %}
{% tab title="mainnet" %}
{% code lineNumbers="true" %}
```bash
~/tmp.gen.keypair
~/staker_memo
/data/findora/mainnet/node.mnemonic
/data/findora/mainnet/mainnet_node.key
/data/findora/mainnet/tendermint/config/
```
{% endcode %}
{% endtab %}

{% tab title="testnet" %}
{% code lineNumbers="true" %}
```
~/tmp.gen.keypair
~/staker_memo
/data/findora/testnet/node.mnemonic
/data/findora/testnet/testnet_node.key
/data/findora/testnet/tendermint/config/
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Migrate your server via Validator Toolbox

To migrate via validator toolbox, use the toolbox to install a brand new node on your new server. Let it fully sync up with the blockchain and now you're ready to use the toolbox to convert this new server over to using your old validator keys and files.

We've built a migration tool into the validator toolbox. To activate this feature create a folder named \~/migrate and using your **old server files** place the **tmp.gen.keypair** file inside along with a copy of your **tendermint/config** folder. Your \~/migrate folder should look like this:

{% code lineNumbers="true" %}
```
~/migrate/tmp.gen.keypair
~/migrate/config
```
{% endcode %}

{% hint style="warning" %}
Once those files are in place shut down your old server to **avoid double signing** as you're ready to change your new server to your old files and start signing instantly.
{% endhint %}

### Change to previous keys

After shutting down your old server, restart the validator toolbox and you will see option 888 on the menu available to migrate your server files to the new validator node.\
\
After running it you'll be up and online almost instantly if your server was fully synced on the temporary keys.\
\
The next time you load toolbox it will ask if you'd like to update the files in your backup folder, say yes to put your old keys into the backup file on the new server and removing the last of the temporary keys.

### Toolbox Options

You can get a print out of our quick options with:

```
cd ~/ && ./findora.sh -h
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

---
description: Installing Findora Node software via the Toolbox on a new server
---

# New Build

This guide is for installing the Validator Toolbox software on a brand-new server setup. We will have notes for first-time validators as there are some additional one-time steps required to become live on testnet or mainnet.

## Pre-Installation Tasks

### Server Selection

You will need a computer/server running 24/7 to run a Findora Validator. Typically this will be a virtual server running on a hosted provider such as Contabo.

{% embed url="https://docs.findora.org/validator-materials/node-setup-guides/system-requirements" %}
System Requirements
{% endembed %}

Once you have a server created you are ready to log in and begin the installation.

## Step 1: Setup A User Account

{% hint style="warning" %}
In this guide, we will be using the name `servicefindora` but feel free to customize each command block for a different username of your choosing.&#x20;
{% endhint %}

### Adding a User Account

Add a new user account to the server using the `adduser` command, shown below.&#x20;

You will need to pick a password and, optionally, enter some basic info and then answer `Y` to confirm, as shown below. Store this password in a secure location.

{% code title="Enter the following command:" %}
```
adduser servicefindora
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

### Provide Root Access to the New Account: <a href="#step-1-pull-findora-docker-image" id="step-1-pull-findora-docker-image"></a>

Once you've created your user account, provide it root access by running the following command:

{% code title="Enter the following command:" %}
```
usermod -aG sudo servicefindora
```
{% endcode %}

There will be no output response to the command.

### Logout and Reconnect as Your New User

At this point, you can log out by typing `exit` and hitting enter.&#x20;

Log back into your node as "servicefindora" using your SSH client (e.g., Putty).

### Verify Group & Root Access for User Account

Verify your new user is in the sudo group by reconnecting now as the new user account. Once logged in, send the command `groups` to verify you are in the sudo group.

{% code title="Enter the following command:" %}
```
groups
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/image (46).png" alt=""><figcaption><p>Ensure that "sudo" appears in the output.</p></figcaption></figure>

## Step 2: Install Docker and Requirements

Install docker by running the following block of code, customize the username `servicefindora` if you're using a different user name:

{% code title="Enter the following command:" overflow="wrap" %}
```
sudo apt update -y && sudo apt install apt-transport-https ca-certificates curl software-properties-common python3-pip python3-dotenv git zip unzip -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt install docker-ce -y && sudo usermod -aG docker servicefindora
```
{% endcode %}

You will see lengthy output from running this command, but it should return to the prompt after a few moments of setting up docker. This is the expected output:

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption><p>Example output during the docker installation step.</p></figcaption></figure>

### **Disconnect and Reconnect as "servicefindora"**

After reconnecting, you can verify you are in the docker group by typing `groups` and verifying the docker group is listed as shown.

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

### Run the "docker ps" Command

Run `docker ps` command. Below is the expected output:

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption><p>Output expected from the "docker ps" command.</p></figcaption></figure>

## Step 3: Firewall Setup

Firewall types vary depending on OS and provider.&#x20;

Here are the ports required to be open for Findora. Port 22 is for SSH, the rest are for the Findora docker container. Use your provider tools or the CLI to configure your firewall.

```
22
8545
8667-8669
26657
```

## Step 4: Download & Run Toolbox Installer

Once you've logged back in and your user is in the docker group, run the following command to install the toolbox and begin installation on either mainnet or testnet.&#x20;

Our menu will launch and ask you a few simple questions to get you fully loaded and online:

{% tabs %}
{% tab title="Download & Start Installer" %}
```bash
cd ~/ && wget https://raw.githubusercontent.com/FindoraNetwork/findora-toolbox/main/src/bin/findora.sh && chmod +x findora.sh && ./findora.sh --installer
```
{% endtab %}
{% endtabs %}

The installer will pull the installation script and get everything setup. At the end of the installer you'll have a fully working validator syncing up to the blockchain on a brand new tmp.gen.keypair and priv\_validator\_key.json file.&#x20;

These are usable as wallets but are also disposable still at this point. You can test out all the functions of a Findora server now as long as you don't run the staking and creation commands.

## After Toolbox Installation

{% hint style="info" %}
At this point you'll have a system that begins syncing automatically on the blockchain after the database download and unpacking completes. Wait for your `sync_status` to equal false before sending your command to create a validator or before migrating an existing validator to the new server.
{% endhint %}

Run the following commands and ensure they return status messages without errors. Your node has been successfully configured and started if no errors are displayed.

{% code lineNumbers="true" %}
```
curl 'http://localhost:26657/status'
curl 'http://localhost:8669/version'
```
{% endcode %}

## Step 5: Complete Validator Creation

#### Fund Validator Wallet & Creating Validator On-Chain <a href="#step-8-check-signing" id="step-8-check-signing"></a>

Now you can run `fn show` or `findora.sh` to see your validator address on this server.&#x20;

You should now fund your validator wallet with at least 10,000 FRA plus extra to cover any gas fees or slashing due to unexpected downtime.

#### Staker Memo File

Create the file staker\_memo in your home directory. This file defines your validator name, description, your website, and logo to display.

{% code title="Enter the following command:" %}
```
nano ~/staker_memo
```
{% endcode %}

This will open the nano text editor. You can copy and paste the template below.

```
{
  "name": "ExampleNode",
  "desc": "I am just an example description. Please change me.",
  "website": "https://www.example.com",
  "logo": "https://www.example.com/logo.png"
}
```

{% hint style="warning" %}
Remember to customize the fields above before saving the file. For the logo, a free and easy platform to use is imgur.com. Paste your logo to imgur.com and use the link they provide, ensuring it ends in .png or .jpg.
{% endhint %}

In the next step, when you create your validator, the information in this file is passed onto the command to be used on the Findora Validator Explorer.&#x20;

{% hint style="info" %}
In the future, you can still utilize this file to update your validator information by re-editing the file and resending your info via the `fn staker-update` command show later.&#x20;
{% endhint %}

#### Create Validator and Start Signing

With the wallet funded and staker\_memo created, you are now ready to create your validator on-chain and begin signing blocks.

The example below shows how to start your validator with a stake of 15,000 FRA with a commission rate of 2%.

**Modify it to your personal preferences.**

{% code title="Customize and enter:" %}
```
fn stake -n $((15000 * 1000000)) -R 0.02 -M "$(cat ~/staker_memo)"
```
{% endcode %}

{% hint style="info" %}
In this example, 15000 \* 1000000 FRA is 15,000 FRA tokens staked.
{% endhint %}

In a few minutes, your validator information page on [findorascan.io ](https://findorascan.io/)will show the commission rate and self-stake you selected in the command above.

**Your validator is now online. Launch your toolbox with the following command!**

```
cd ~/ && ./findora.sh
```

## Step 6: Launching Toolbox

Anytime you would like to run the full toolbox menu we suggest pulling updates and then launching the application.&#x20;

The code below works for either `testnet` or `mainnet` toolbox. Here's a string of code you can run to update and start the toolbox again:

```bash
cd ~/ && ./findora.sh
```

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Main Menu</p></figcaption></figure>

## Wrapping Up

Congratulations!&#x20;

If all steps were completed successfully, your validator should now be online - viewable from the Findora Explorer, in sync with the chain, and self-staked with at least 10,000 FRA.&#x20;

Reviewing the Best Practices and Troubleshooting sections of the validator guide is strongly recommended for your next steps. We also suggest joining the Findora Discord, requesting a validator role, and joining the conversation with other validators.

**Ensure you stay up-to-date on the latest Findora news and changes, as some upgrades to the network will require you to update your validator node in a timely manner.**

## **Stay Involved**

* [Join the Discord.](https://findora.org/discord)
* [Join the Reddit community.](https://findora.org/reddit)

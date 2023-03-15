---
description: >-
  This guide walks you through the installation and configuration of a Findora
  validator node. It is written to ensure easy onboarding for beginners and
  intermediate users.
---

# Manual Setup

### System Requirements[​](https://docs.findora.org/validators/validators-get-started#system-requirements) <a href="#system-requirements" id="system-requirements"></a>

* Hardware Requirements:
  * Minimum: 8GB RAM, 2 Core CPU (2.90GHz per core), 100GB Hard Disk
  * Recommended: 16GB RAM, 4 Core CPU (2.90Ghz per core), 300GB Hard Disk
    * ex: AWS T3 t3.2xlarge
    * ex: AliCloud g6 g6.2xlarge
    * ex: GCP n2 n2-standard-8
* Software Requirements:
  * Ubuntu 20.04LTS or 22.04LTS Operating System or MacOS
  * Firewall ports opened: 8545, 8667-8669, 26657
  * User account with root access

### Step 1: First Server Login <a href="#step-1-pull-findora-docker-image" id="step-1-pull-findora-docker-image"></a>

This guide assumes you have an Ubuntu Server running and can log in as root. We recommend setting up a user account to run the findora service under a new account instead of running the software directly as root.

In this guide, we will be using the name `servicefindora` but feel free to customize each command block for a different username.&#x20;

#### Adding a User Account

Add the new user account to the server using the `adduser` command, shown below.&#x20;

You will need to pick a password and, optionally, enter some basic info and then answer `Y` to confirm, as shown below. Store this password in a secure location.

{% code title="Enter the following command:" %}
```
adduser servicefindora
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

> **✅ Completed**: Add the "servicefindora" user account.

#### Provide Root Access to the "servicefindora" Account: <a href="#step-1-pull-findora-docker-image" id="step-1-pull-findora-docker-image"></a>

Once you've created your user account, provide it root access by running the following command:

{% code title="Enter the following command:" %}
```
usermod -aG sudo servicefindora
```
{% endcode %}

There will be no output response to the command.

> **✅ Completed**: Provide root access to the "servicefindora" account.

#### Logout and Reconnect as Your New User

At this point, you can log out by typing `exit` and hitting enter.&#x20;

Log back into your node as "servicefindora" using your SSH client (e.g., Putty).

> **✅ Completed**: Logout and reconnect as "servicefindora".

#### Verify Root Access for User Account

Verify your new user is in the sudo group by reconnecting now as the new user account. Once logged in, send the command `groups` to verify you are in the sudo group.

{% code title="Enter the following command:" %}
```
groups
```
{% endcode %}

> **✅ Completed**: Verify root access for "servicefindora".

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption><p>Ensure that "sudo" appears in the output.</p></figcaption></figure>

### Step 2: Install Docker

Install docker by running the following block of code, customize the username `servicefindora` if you're using a different user name:

{% code title="Enter the following command:" overflow="wrap" %}
```
sudo apt update -y && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt install docker-ce -y && sudo usermod -aG docker servicefindora
```
{% endcode %}

You'll see lengthy output from running this command, but it should return to the prompt after a few moments of setting up docker. This is the expected output:

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption><p>Example output during the docker installation step.</p></figcaption></figure>

> **✅ Completed**: Install docker and add "servicefindora" to the docker group.

**Disconnect and Reconnect as "servicefindora"**

After reconnecting, you can verify you are in the docker group by typing `groups` and verifying the docker group is listed as shown.

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

> &#x20;**✅ Completed**: Logout and reconnect as "servicefindora".

#### Run the "docker ps" Command

Run `docker ps` command. Below is the expected output:

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption><p>Output expected from the "docker ps" command.</p></figcaption></figure>

> **✅ Completed**: Confirm the output above from the `docker ps` command.

### Step 3: Pull Findora Docker Container Image <a href="#step-1-pull-findora-docker-image" id="step-1-pull-findora-docker-image"></a>

Navigate to your project folder and pull the docker image.&#x20;

Here, we are downloading the `findorad` which is the node of the Findora Network. For security and stability reasons, make sure to download the live version. First, we need to query the live version number.

{% code title="Enter the following command:" overflow="wrap" %}
```
export LIVE_VERSION=$(curl -s https://prod-mainnet.prod.findora.org:8668/version | awk -F\  '{print $2}') && export FINDORAD_IMG=findoranetwork/findorad:${LIVE_VERSION}
```
{% endcode %}

> **✅ Completed**: Run the "export" command.

{% hint style="info" %}
Note: At this point, if your session disconnects, you will need to re-run any exports so your server has these variables configured. They only last for your currently connected session.
{% endhint %}

**Download the correct version:**

{% code title="Enter the following command:" overflow="wrap" %}
```
docker pull ${FINDORAD_IMG}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

> **✅ Completed**: Run the "docker pull" command.

Optional: Verify your version of findorad:&#x20;

{% code title="Enter the following command:" %}
```
docker image ls
```
{% endcode %}

### Step 4: Download & install fn CLI[​](https://wiki.findora.org/docs/validators/manual-setup#step-2-setup-fn-cli) <a href="#user-content-step-2-setup-fn-cli" id="user-content-step-2-setup-fn-cli"></a>

You will need the Findora Node Setup (fn) CLI tool that contains the necessary sub-commands to set up a validator node and stake/unstake FRA.

Download the proper application file for your OS - Linux/MacOS.

{% tabs %}
{% tab title="Linux/WSL" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/fn && chmod +x fn && sudo mv fn /usr/local/bin/
```
{% endcode %}
{% endtab %}

{% tab title="MacOS" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/fn-mac -O fn && chmod +x fn && sudo mv fn /usr/local/bin/
```
{% endcode %}
{% endtab %}
{% endtabs %}

> **✅ Completed**: Download the fn CLI using the command above.

### Step 5: Configure Local Node[​](https://docs.findora.org/docs/validators/manual-setup#step-3-configure-local-node) <a href="#step-3-configure-local-node" id="step-3-configure-local-node"></a>

#### Set Environment Path Variable

{% code title="Enter the following command:" %}
```
export ROOT_DIR=/data/findora/mainnet
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

> **✅ Completed**: Use the export command to configure the environment path variable.

#### Create a Ledger Data Directory

First, we will clean up any old data you might have by removing the ROOT\_DIR folder. Be sure to back up all your keys (validator, node, and wallet key) before removing this directory.

{% hint style="danger" %}
**Proceed With Caution**&#x20;

Since the ROOT\_DIR is the source of the connection to Mainnet, you might lose your funds if the keys are not backed up properly. This warning applies only if you're running this command on an existing, pre-built validator node.&#x20;

Ignore this warning if you're starting from scratch.
{% endhint %}

```bash
sudo rm -rf ${ROOT_DIR}
```

> **✅ Completed**: Remove the ROOT\_DIR folder.

Now create a new ledger data directory & set permissions for your `servicefindora` user; customize the username if needed before running:

{% code title="Enter the following command:" overflow="wrap" %}
```bash
sudo mkdir -p ${ROOT_DIR} && sudo chown -R servicefindora:servicefindora ${ROOT_DIR}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

> **✅ Completed**: Create a new ledger data directory and set user permissions.

#### Initialize Tendermint

Initializing Tendermint will create a node key (stored in a newly created file at the path `${ROOT_DIR}/tendermint/config/priv_validator_key.json`). The node key will be used to identify your node, sign blocks, and perform other Tendermint consensus-related tasks.

{% code title="Enter the following command:" overflow="wrap" %}
```
docker run --rm -v ${ROOT_DIR}/tendermint:/root/.tendermint ${FINDORAD_IMG} init --mainnet || exit 1
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

> &#x20;**✅ Completed**: Initialize Tendermint using the command above.

#### Setting Permissions

Set the correct permissions by running the following code. No output is expected.

{% code title="Enter the following command:" overflow="wrap" %}
```
sudo chown -R servicefindora:servicefindora ${ROOT_DIR}/tendermint/
```
{% endcode %}

> **✅ Completed**: Set permissions using the command above.

#### Get the Link for the Latest Chain Data

Set your namespace to the current working environment. No output is expected.

{% code title="Enter the following command:" overflow="wrap" %}
```
export NAMESPACE=mainnet
```
{% endcode %}

Findora node may contain light history (regular full node) or full history (archive node) based on the node operators' needs. An archive node requires larger disk space (200GB as of Jan. 2023) than regular full nodes.

To get data link for regular **full node**

{% code title="Enter the following command:" overflow="wrap" %}
```
wget -O "${ROOT_DIR}/latest" "https://prod-${NAMESPACE}-us-west-2-chain-data-backup.s3.us-west-2.amazonaws.com/latest" && export CHAINDATA_URL=$(cut -d , -f 1 "${ROOT_DIR}/latest")
```
{% endcode %}

To get data link for **archive node**

{% code title="Enter the following command:" overflow="wrap" %}
```
wget -O "${ROOT_DIR}/latest" "https://prod-${NAMESPACE}-us-west-2-archive-data-backup.s3.us-west-2.amazonaws.com/latest" && export CHAINDATA_URL=$(cut -d , -f 1 "${ROOT_DIR}/latest")
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

Run the following to verify the download link. It should display a link ending in .tar.gz.

{% code title="Enter the following command:" %}
```
echo $CHAINDATA_URL
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

> **✅ Completed**: Obtain the link for the latest chain data and export URL to a variable.

### Step 6: Download Findora Database

Next, you need to download the data from the link you got in the step above.&#x20;

{% hint style="info" %}
**Note**

This might take a while depending on file size, server location, and internet download speed on your VPS. You will see a progress bar while the download runs with an estimated time remaining.
{% endhint %}

{% code title="Enter the following command:" %}
```bash
wget -O "${ROOT_DIR}/snapshot" "${CHAINDATA_URL}"
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

> **✅ Completed**: Download the Findora database.

Run the following commands to unpack the zipped file and finish the process.&#x20;

This will take a few minutes and a lot of text will be output.

{% code title="Enter the following command:" overflow="wrap" lineNumbers="true" %}
```bash
mkdir "${ROOT_DIR}/snapshot_data" && tar zxvf "${ROOT_DIR}/snapshot" -C "${ROOT_DIR}/snapshot_data" && mv "${ROOT_DIR}/snapshot_data/data/ledger" "${ROOT_DIR}/findorad" && rm -rf ${ROOT_DIR}/tendermint/data && mv "${ROOT_DIR}/snapshot_data/data/tendermint/${NAMESPACE}/node0/data" "${ROOT_DIR}/tendermint/data" && rm -rf ${ROOT_DIR}/snapshot_data && rm -rf ${ROOT_DIR}/snapshot
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If you encounter a security issue error when trying to initialize findora node, you may need to mto approve its security privileges in your OS first manually then re-run the command again
{% endhint %}

> **✅ Completed**: Unpack the zipped database file.

Wait until the unzipping process is completed before proceeding..

### Step 7: Generate Wallet Staking Key[​](https://docs.findora.org/docs/validators/manual-setup#step-4-generate-staking-key) <a href="#step-4-generate-staking-key" id="step-4-generate-staking-key"></a>

#### Generate New Encryption Keys

Generate a new, random pair of public and private keys that will be used for FRA staking:

{% code title="Enter the following command:" %}
```bash
fn genkey > ${ROOT_DIR}/tmp.gen.keypair
```
{% endcode %}

> **✅ Completed**: Generate new encryption keys.

#### View the Newly Created Keys

{% code title="Enter the following command:" %}
```
cat ${ROOT_DIR}/tmp.gen.keypair
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Important:

Make sure to save this information in a secure location. Using this output as a note inside a password vault is recommended. Wherever you decide to save your mnemonic and private key (the "sec\_key" line), please ensure it's password protected.&#x20;

**Never share this information.**
{% endhint %}

> **✅ Completed**: Generate new encryption keys and save the output to a secure location.

#### Import Private Key into the Findora Wallet

For convenience, you can conveniently import your new validator private key into the Findora wallet. Doing so will allow you to check and manage your FRA balances or to view historical transaction data for this wallet address.&#x20;

It's suggested to edit the wallet name once imported for easy identification.

Reference the Findora Wallet section under the Wallet category for information on importing an existing wallet.

The private key is displayed next to `sec_key` (above).

{% hint style="warning" %}
The **private key** or the **mnemonic phrase** should never be shared with anyone, even with people from the Findora community or development team. Our mods will never ask for this information. It would be advisable to keep a backup of your mnemonic on a separate storage, should you ever need to restore it.
{% endhint %}

> **✅ Completed**: Import your new mnemonic phrase into the Findora wallet.

#### Copy Your New Wallet Key to the Data Location

Copy your new wallet key to the data location for future use. This command will run with no output.

{% code title="Enter the following command:" overflow="wrap" %}
```
cp ${ROOT_DIR}/tmp.gen.keypair ${ROOT_DIR}/mainnet_node.key
```
{% endcode %}

> **✅ Completed**: Copy the new wallet key to the data location.

#### Store the Mnemonic Words

For convenience in setting up your node via the `fn` tool, store your 24 mnemonic keywords (located inside tmp.gen.keypair) into `${ROOT_DIR}/node.mnemonic.`&#x20;

This command will run without output.

{% code title="Enter the following command:" overflow="wrap" %}
```bash
echo "24_mnemonic_keywords_here" > ${ROOT_DIR}/node.mnemonic
```
{% endcode %}

Below is an example of that command. Customize the command for your mnemonic.&#x20;

<mark style="color:red;">**Do not use the mnemonic displayed below on your validator!**</mark>

{% code overflow="wrap" %}
```bash
# Note: This is an example of a mnemonic phrase being configured. 

echo "repair drink action brass term blur fat doll spoon thumb raise squirrel tornado engine tumble picnic approve elegant tube urge ghost secret seminar blame" > ${ROOT_DIR}/node.mnemonic
```
{% endcode %}

You can verify the file is setup properly by running the following command, which should return your 24 mnemonic works on a single line:

```bash
cat ${ROOT_DIR}/node.mnemonic
```

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption><p>Example output.</p></figcaption></figure>

> **✅ Completed**: Store the mnemonic words into ${ROOT\_DIR}/node.mnemonic

### Step 8: Connect to the Network[​](https://docs.findora.org/docs/validators/manual-setup#step-5-connect-to-the-network) <a href="#step-5-connect-to-the-network" id="step-5-connect-to-the-network"></a>

To connect `fn` with the Findora Network and to your node.mnemonic & priv\_validator_\__key.json files, run the following command, which will return no output:

{% code title="Enter the following command:" overflow="wrap" %}
```
fn setup -S https://prod-mainnet.prod.findora.org && fn setup -O ${ROOT_DIR}/node.mnemonic && fn setup -K ${ROOT_DIR}/tendermint/config/priv_validator_key.json
```
{% endcode %}

After entering this command, you can now run `fn show` to see your validator information.&#x20;

{% hint style="info" %}
Note:&#x20;

We have yet to send the command to perform the initial staking and configuration, both of which are required to get your validator online. This will come later.
{% endhint %}

Note your Findora address, as this will need to be funded with at least 10,000 FRA to start your validator.

> &#x20;**✅ Completed**: Connect to the network.

### Step 9: Start Local Node[​](https://docs.findora.org/docs/validators/manual-setup#step-6-start-or-upgrade-local-node) <a href="#step-6-start-or-upgrade-local-node" id="step-6-start-or-upgrade-local-node"></a>

Optional: Stop your local container if necessary using the command below. Stopping the local container is only necessary if you're working on an existing, live node.

```bash
docker rm -f findorad || exit 1
```

Mandatory: Start your node container with the command below (add `--arc-history=65530,10` for archive node) to pull and setup the latest image.

{% code title="Enter the following command:" overflow="wrap" %}
```
docker run -d \
    -v ${ROOT_DIR}/tendermint:/root/.tendermint \
    -v ${ROOT_DIR}/findorad:/tmp/findora \
    -p 8669:8669 \
    -p 8668:8668 \
    -p 8667:8667 \
    -p 8545:8545 \
    -p 26657:26657 \
    -e EVM_CHAIN_ID=2152 \
    --name findorad \
    ${FINDORAD_IMG} node \
    --ledger-dir /tmp/findora \
    --tendermint-host 0.0.0.0 \
    --tendermint-node-key-config-path="/root/.tendermint/config/priv_validator_key.json" \
    --enable-query-service \
    --enable-eth-api-serviceStep 10: Check Local Node Status
```
{% endcode %}

To run the node in archive mode, you have to add below option

```bash
--arc-history=65530,10
```

To run the node with Rosetta API enabled, you have to pass additional environment variables

```bash
-e ROSETTA=true           # required
-e ROSETTA_PORT=8080      # overriding options: any http port
-e ROSETTA_NETWORK=PRINET # overriding options: MAINNET, TESTNET, PRIVET
-e ROSETTA_MODE=ONLINE    # overriding options: ONLINE, OFFLINE
```

> **✅ Completed**: Start your node container.

### Step 10: Check Local Node Status[​](https://docs.findora.org/docs/validators/manual-setup#step-7-check-local-node-status) <a href="#step-7-check-local-node-status" id="step-7-check-local-node-status"></a>

Run the following commands and ensure they return status messages without errors. Your node has been successfully configured and started if no errors are displayed.

{% code title="Enter the following commands:" overflow="wrap" lineNumbers="true" %}
```bash
curl 'http://localhost:26657/status'
curl 'http://localhost:8669/version'
curl 'http://localhost:8668/version' # Only if you set the 'ENABLE_LEDGER_SERVICE'
curl 'http://localhost:8667/version' # Only if you set the 'ENABLE_QUERY_SERVICE'
```
{% endcode %}

{% hint style="info" %}
Moving forward, you can use **the top curl command** to view the status of your node and check if it's in sync or not at this time. You will want to wait until your server is fully synced up before moving on to the next step.&#x20;

You can verify this is completed by running the status curl command and by verifying that "catching\_up" is false, as shown in the screenshot below.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption><p>"catching_up": false = in sync | true = still syncing</p></figcaption></figure>

{% hint style="info" %}
You may continue through the guide as the validator catches up, but it will not sign blocks until "catching\_up" shows false and the steps below are complete.
{% endhint %}

### Step 11: Fund Validator Wallet & Creating Validator On-Chain <a href="#step-8-check-signing" id="step-8-check-signing"></a>

Using `fn show` allows you to see your future validator address. Because the self-stake of 10,000 FRA is mandatory for creating your on-chain validator, you should now fund your validator wallet with at least 10,000 FRA plus extra to cover any gas fees or slashing due to unexpected downtime.

{% hint style="info" %}
Use the Findora wallet to monitor the balance of your validator address.
{% endhint %}

> **✅ Completed**: Transfer 10,000+ FRA to your validator address.

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

> **✅ Completed**: Create and customize the staker\_memo file.

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

> **✅ Completed**: Customize self-stake and commission rate and create your on-chain validator.

### Wrapping Up

Congratulations!&#x20;

If all steps were completed successfully, your validator should now be online - viewable from the Findora Explorer, in sync with the chain, and self-staked with at least 10,000 FRA.&#x20;

Reviewing the Best Practices and Troubleshooting sections of the validator guide is strongly recommended for your next steps. We also suggest joining the Findora Discord, requesting a validator role, and joining the conversation with other validators.

**Ensure you stay up-to-date on the latest Findora news and changes, as some upgrades to the network will require you to update your validator node in a timely manner.**

### **Stay involved:**

* [Join the Discord.](https://findora.org/discord)
* [Join the Reddit community.](https://findora.org/reddit)
* [Join the Telegram channel.](https://findora.org/telegram)

{% hint style="info" %}
It's recommended to stay active and support the Findora project and its community by answering questions and creating content such as articles, educational videos, etc.
{% endhint %}




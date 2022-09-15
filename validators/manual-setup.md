# Manual Setup

### Step 1: Pull Findora docker image[​](https://wiki.findora.org/docs/validators/manual-setup#step-1-pull-findora-docker-image) <a href="#step-1-pull-findora-docker-image" id="step-1-pull-findora-docker-image"></a>

Navigate to your project folder and pull docker image. Here, we are downloading the `findorad` which is the node of the Findora Network. For security and stability reasons, make sure to download the live version. First we need to query the live version number

{% tabs %}
{% tab title="Mainnet" %}
```bash
export LIVE_VERSION=$(curl -s https://prod-mainnet.prod.findora.org:8668/version | awk -F\  '{print $2}')
export FINDORAD_IMG=findoranetwork/findorad:${LIVE_VERSION}
```
{% endtab %}

{% tab title="Testnet" %}
```bash
export LIVE_VERSION=$(curl -s https://prod-testnet.prod.findora.org:8668/version | awk -F\  '{print $2}')
export FINDORAD_IMG=findoranetwork/findorad:${LIVE_VERSION}
export CHECKPOINT_URL=https://prod-testnet-us-west-2-ec2-instance.s3.us-west-2.amazonaws.com/testnet/checkpoint
```
{% endtab %}
{% endtabs %}

In this example, we get the live version is \`v0.3.27-release\`. Then we download the correct version by

```bash
docker pull ${FINDORAD_IMG}
```

<figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-0.png" alt=""><figcaption></figcaption></figure>

Verify you have the latest version by checking for the tag as seen in the picture below

```bash
docker image ls
```

<figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-2.png" alt=""><figcaption></figcaption></figure>

### Step 2: Setup fn CLI[​](https://wiki.findora.org/docs/validators/manual-setup#step-2-setup-fn-cli) <a href="#step-2-setup-fn-cli" id="step-2-setup-fn-cli"></a>

1.  You will need the Findora Node Setup (fn) CLI tool that contains the neccessary sub-commands to setup a validator node and stake/unstake FRA.

    Download according to your operating system:

    * [Linux](https://wiki.findora.org/bin/linux/fn)
    * [MacOS](https://wiki.findora.org/bin/macos/fn)

    You can also run a node on windows via _Windows Subsystem for Linux_
2.  Move your downloaded `fn` to your path directory by either running

    ```bash
    mv fn /usr/local/bin/
    ```

    or by running the command below if you moved the fn file to HOME

    ```bash
    cp $HOME/fn /user/local/bin/
    ```



    <figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-3.png" alt=""><figcaption></figcaption></figure>
3.  Ensure that binaries have executable permissions set correctly



    <figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-4.png" alt=""><figcaption></figcaption></figure>

### Step 3: Configure Local Node[​](https://wiki.findora.org/docs/validators/manual-setup#step-3-configure-local-node) <a href="#step-3-configure-local-node" id="step-3-configure-local-node"></a>

1.  Set Environment Path Variables

    ```bash
    export ROOT_DIR=< The data path of your node >
    ```



    <figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-5.png" alt=""><figcaption></figcaption></figure>
2.  Create ledger data directory

    First we are going to clean up any old data you might have by removing the ROOT\_DIR folder. Be sure to backup all your keys (validator, node and wallet key) before removing this directory.

> **NOTE**
>
> **Proceed with caution** - Since the ROOT\_DIR is the source of the connection to Mainnet, you might lose your funds if the keys are not backed up properly

```bash
sudo rm -rf ${ROOT_DIR}
```

Now create a new ledger data directory

```bash
sudo mkdir -p ${ROOT_DIR}
```

3\. Initialize Tendermint

Initializing Tendermint will create a node key (stored in a newly created file at the path `${ROOT_DIR}/tendermint/config/priv_validator_key.json`). The node key will be used to identify your node, sign blocks and perform other tendermint consensus-related tasks.

{% tabs %}
{% tab title="Mainet" %}
```bash
 docker run --rm -v ${ROOT_DIR}/tendermint:/root/.tendermint ${FINDORAD_IMG} init --mainnet || exit 1
```
{% endtab %}

{% tab title="Testnet" %}
```
 docker run --rm -v ${ROOT_DIR}/tendermint:/root/.tendermint ${FINDORAD_IMG} init --testnet || exit 
```
{% endtab %}
{% endtabs %}

Set correct permission

```bash
sudo chown -R `id -u`:`id -g` ${ROOT_DIR}/tendermint/
```

4\. Get the link for latest Chain Data

Set your namespace to the current working environment

{% tabs %}
{% tab title="Mainnet" %}
```bash
export NAMESPACE=mainnet
```
{% endtab %}

{% tab title="Testnet" %}
```bash
export NAMESPACE=testnet
```
{% endtab %}
{% endtabs %}

Get latest chain link and export URL to variable

```bash
wget -O "${ROOT_DIR}/latest" "https://prod-${NAMESPACE}-us-west-2-chain-data-backup.s3.us-west-2.amazonaws.com/latest"
export CHAINDATA_URL=$(cut -d , -f 1 "${ROOT_DIR}/latest")
```

Run `echo $CHAINDATA_URL` to verify the link

<figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-6.png" alt=""><figcaption></figcaption></figure>

1.  Download the Data

    Next, you need to download the data from the link you got in the step above. This might take a while.

    ```bash
    wget -O "${ROOT_DIR}/snapshot" "${CHAINDATA_URL}"
    ```



    Run the following commands to finish the process.

    ```bash
    mkdir "${ROOT_DIR}/snapshot_data"
    tar zxvf "${ROOT_DIR}/snapshot" -C "${ROOT_DIR}/snapshot_data"
    mv "${ROOT_DIR}/snapshot_data/data/ledger" "${ROOT_DIR}/findorad"
    rm -rf ${ROOT_DIR}/tendermint/data
    mv "${ROOT_DIR}/snapshot_data/data/tendermint/${NAMESPACE}/node0/data" "${ROOT_DIR}/tendermint/data"
    rm -rf ${ROOT_DIR}/snapshot_data
    ```

    <figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-7.png" alt=""><figcaption></figcaption></figure>

> **NOTE**
>
> If you encounter a security issue error when trying to initialize findora node, you may need to manually approve its security privileges in your OS first and then re-run the command again.

### Step 4: Generate Staking Key[​](https://wiki.findora.org/docs/validators/manual-setup#step-4-generate-staking-key) <a href="#step-4-generate-staking-key" id="step-4-generate-staking-key"></a>

1.  Generate Keys

    Generate a new, random pair of public and private keys that will be used for FRA staking:

    ```bash
    fn genkey > ${ROOT_DIR}/tmp.gen.keypair
    ```

    To view the keys: `cat ${ROOT_DIR}/tmp.gen.keypair`

    Example:

    ```bash
    # Note: This is an example. Do not use them in your own node.
    Wallet Address: fra1955hpj2xzkp4esd5928yhtp0l78ku8fkztvwcypvr8mk6x8tkn6sjsajun
    Mnemonic: repair drink action brass term blur fat doll spoon thumb raise squirrel tornado engine tumble picnic approve elegant tube urge ghost secret seminar blame
    Key: {
        "pub_key": "LSlwyUYVg1zBtCqOS6wv_49uHTYS2OwQLBn3bRjrtPU=",
        "sec_key": "b0MGhK7xaRQHuhzFkaBhQ1o4GwTumJEWt1NQ7FChNwA="
    }
    ```
2.  Importing private key to wallet

    For convenience, you can import the `sec_key` (aka private key) into any Findora wallet (Win/Mac wallet, mobile wallet, CLI wallet tool, etc.), to check and manage your FRA balances or to view historical transaction data for this wallet address.

> **NOTE**
>
> The private key or the mnemonic should never be shared with anyone, even with people from the Findora community or development team. Our mods will never ask for this information. It would be advisable to keep a backup of your mnemonic on a separate storage, should you ever need to restore it.

3\. Store your keypair for future use

{% tabs %}
{% tab title="Mainnet" %}
<pre class="language-bash"><code class="lang-bash"><strong>cp ${ROOT_DIR}/tmp.gen.keypair ${ROOT_DIR}/mainnet_node.key</strong></code></pre>
{% endtab %}

{% tab title="Testnet" %}
```bash
cp ${ROOT_DIR}/tmp.gen.keypair ${ROOT_DIR}/testnet_node.key
```
{% endtab %}
{% endtabs %}

4\. Store Mnemonic words

For convenience in setting up your node via the `fn` tool, store your 24 mnemonic keywords (located inside tmp.gen.keypair) into `${ROOT_DIR}/node.mnemonic`

```bash
echo <24 mnemonic keywords> > ${ROOT_DIR}/node.mnemonic
```

Example:

```bash
# Note: This is an example. Do not use them in your own node.
echo "repair drink action brass term blur fat doll spoon thumb raise squirrel tornado engine tumble picnic approve elegant tube urge ghost secret seminar blame" > ${ROOT_DIR}/node.mnemonic
```

### Step 5: Connect to the Network[​](https://wiki.findora.org/docs/validators/manual-setup#step-5-connect-to-the-network) <a href="#step-5-connect-to-the-network" id="step-5-connect-to-the-network"></a>

To connect `fn` with the Findora Network, use this command:

{% tabs %}
{% tab title="Mainnet" %}
```bash
fn setup -S https://prod-mainnet.prod.findora.org
```
{% endtab %}

{% tab title="Testnet" %}
```bash
fn setup -S https://prod-testnet.prod.findora.org
```
{% endtab %}
{% endtabs %}

To connect your staking key (inside `node.mnemonic`) to `fn`, use the below command. This allows fn to sign transactions on your behalf.

```bash
# Ex: fn setup -O ${ROOT_DIR}/node.mnemonic
fn setup -O <Path to the mnemonic of your node> || exit 1
```

To connect your Node Key to `fn`, use the command below.

```bash
# Ex: fn setup -K ${ROOT_DIR}/tendermint/config/priv_validator_key.json
fn setup -K <path to validator key> || exit 1
```

### Step 6: Start or Upgrade Local Node[​](https://wiki.findora.org/docs/validators/manual-setup#step-6-start-or-upgrade-local-node) <a href="#step-6-start-or-upgrade-local-node" id="step-6-start-or-upgrade-local-node"></a>

Stop your local container if necessary using this command:

```bash
docker rm -f findorad || exit 1
```

To start your validator container, run this command

{% tabs %}
{% tab title="Mainnet" %}
```bash
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
    --enable-eth-api-service
```
{% endtab %}

{% tab title="Testnet" %}
```bash
docker run -d \
    -v ${ROOT_DIR}/tendermint:/root/.tendermint \
    -v ${ROOT_DIR}/findorad:/tmp/findora \
    -v ${ROOT_DIR}/checkpoint.toml:/root/checkpoint.toml \
    -p 8669:8669 \
    -p 8668:8668 \
    -p 8667:8667 \
    -p 8545:8545 \
    -p 26657:26657 \
    -e EVM_CHAIN_ID=2153 \
    --name findorad \
    ${FINDORAD_IMG} node \
    --ledger-dir /tmp/findora \
    --checkpoint-file=/root/checkpoint.toml \
    --tendermint-host 0.0.0.0 \
    --tendermint-node-key-config-path="/root/.tendermint/config/priv_validator_key.json" \
    --enable-query-service \
    --enable-eth-api-service
```
{% endtab %}
{% endtabs %}

Logging for Node:

```bash
docker logs -f findorad
```

### Step 7: Check Local Node Status[​](https://wiki.findora.org/docs/validators/manual-setup#step-7-check-local-node-status) <a href="#step-7-check-local-node-status" id="step-7-check-local-node-status"></a>

If the following commands return status messages without any errors, then your node has been successfully configured and started

```bash
curl 'http://localhost:26657/status'
curl 'http://localhost:8669/version'
curl 'http://localhost:8668/version' # Only if you set the 'ENABLE_LEDGER_SERVICE'
curl 'http://localhost:8667/version' # Only if you set the 'ENABLE_QUERY_SERVICE'
```

### Step 8: Check Signing[​](https://wiki.findora.org/docs/validators/manual-setup#step-8-check-signing) <a href="#step-8-check-signing" id="step-8-check-signing"></a>

Run the following on console on your server to show the latest stats.

```bash
fn show
```

<figure><img src="https://wiki.findora.org/img/validator_setup_guide/manual-setup-8.png" alt=""><figcaption></figcaption></figure>

> **NOTE**
>
> For the next steps, proceed to [this Staking Guide](staking-guide.md) to learn how to fund your validator and stake FRA.

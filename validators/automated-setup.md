# Automated Setup

This guides shows how to use the automated setup scripts to configure your validator node and download the binaries automatically.

#### Setup the fn CLI Tool[​](https://wiki.findora.org/docs/validators/automated-setup#setup-the-fn-cli-tool) <a href="#setup-the-fn-cli-tool" id="setup-the-fn-cli-tool"></a>

`fn`: Findora Node Setup (fn) is a command-line (CLI) utility that allows you to set up a validator node and stake/unstake FRA.

{% tabs %}
{% tab title="Linux version" %}
{% file src="../.gitbook/assets/fn (1)" %}
{% endtab %}

{% tab title="MacOS version" %}
{% file src="../.gitbook/assets/fn-mac" %}
{% endtab %}
{% endtabs %}

Download the appropriate file and move to your path:

```bash
wget https://wiki.findora.org/bin/linux/fn
chmod +x fn
mv fn /usr/local/bin/
```

#### Generate Keys[​](https://wiki.findora.org/docs/validators/automated-setup#generate-keys) <a href="#generate-keys" id="generate-keys"></a>

Generate a new, random pair of public and private keys that will be used for FRA staking:

```bash
fn genkey > tmp.gen.keypair
```

To view the keys: `cat tmp.gen.keypair`

Before continuing, the staking private key (`sec_key` in your `tmp.gen.keypair` file) should be saved in a file at the following path:

```bash
/data/findora/{network_name}/{network_name}_node.key
```

Note: If this directory does not exist, you will need to create it.

#### Download and run the automated setup script[​](https://wiki.findora.org/docs/validators/automated-setup#download-and-run-the-automated-setup-script) <a href="#download-and-run-the-automated-setup-script" id="download-and-run-the-automated-setup-script"></a>

{% tabs %}
{% tab title="Mainnet" %}
{% file src="../.gitbook/assets/node_init_mainnet.sh" %}
{% endtab %}

{% tab title="Second Tab" %}
{% file src="../.gitbook/assets/node_init_testnet.sh" %}
{% endtab %}
{% endtabs %}

Example:

```bash
bash -x node_init_testnet.sh
```

**NOTE**

All existing validator and wallet information will be removed by running these scripts. If all you want is to keep your data, [Safety Clean](version-update.md#auto-safety-clean) should be used

#### Connect to the Network[​](https://wiki.findora.org/docs/validators/automated-setup#connect-to-the-network) <a href="#connect-to-the-network" id="connect-to-the-network"></a>

To connect `fn` with the Findora Network, use this command:

* For Testnet: `fn setup -S https://prod-testnet.prod.findora.org`
* For Mainnet: `fn setup -S https://prod-mainnet.prod.findora.org`

To connect your staking key (inside `node.mnemonic`) to fn, use the below command. This allows fn to sign transactions on your behalf.

```bash
# Ex: fn setup -O ${ROOT_DIR}/node.mnemonic
fn setup -O <Path to the mnemonic of your node> || exit 1
```

To connect your Node Key to fn, use the command below.

```bash
# Ex: fn setup -K ${ROOT_DIR}/tendermint/config/priv_validator_key.json
fn setup -K <path to validator key> || exit 1
```

> **NOTE**
>
> For the next steps, proceed to this [Staking Guide](staking-guide.md) to learn how to fund your validator and stake FRA.\
>

# Version Updating Guide

`Note:` A major platform version upgrade (v0.3.3x) upgrade window has been scheduled for 12/12/22 through 12/19/22.

Validators can begin updating their validator binary version on Monday 12/12/22 at 6p PT. They must finish updating by Monday 12/19/22 at 6p PT. Simply run the script in the `Update Binary Version via Docker` instructions below to automatically update your validator to version to v0.3.3x. Validators will also need to update their `fn` CLI tool as well to work with the v0.3.3x platform version.

\---

### Update Binary Version via Docker[​](https://wiki.findora.org/docs/validators/update-version#update-image-version) <a href="#update-image-version" id="update-image-version"></a>

The script below can be used in any environment to update your validator to the latest binary version via Docker.

{% tabs %}
{% tab title="Mainnet" %}
{% file src="../../.gitbook/assets/update_version_mainnet.sh" %}
{% endtab %}

{% tab title="Testnet" %}
{% file src="../../.gitbook/assets/update_version_testnet.sh" %}
{% endtab %}
{% endtabs %}

Example:

```bash
bash -x update_version_mainnet.sh
```

The `Update Image Version` script above will:

```
1. Retrieve the latest version number that all validators should run
2. Stop the existing `findorad` docker container
3. Start a new Docker container with the latest version
4. Output the Docker container status and image version
```

To confirm if the upgrade worked correctly, check the output of the script which will display both the i) node status and the ii) image version that is running.



#### Upgrade the fn CLI Tool[​](https://wiki.findora.org/docs/validators/automated-setup#setup-the-fn-cli-tool) <a href="#setup-the-fn-cli-tool" id="setup-the-fn-cli-tool"></a>

`fn`: Findora Node Setup (fn) is a command-line (CLI) utility that allows you to set up a validator node and stake/unstake FRA. You can download the `fn` tool via the two options below.

`Note:` For both Mac and Linux users, you must move the `fn` tool to the `/usr/local/bin/` path.

Download Option 1)

{% tabs %}
{% tab title="Linux version" %}
{% file src="../../.gitbook/assets/fn (1)" %}
Note: You must move the `fn` tool to the `/usr/local/bin` path after download
{% endfile %}
{% endtab %}

{% tab title="MacOS version" %}
{% file src="../../.gitbook/assets/fn-mac" %}
Note: You must move the `fn` tool to the `/usr/local/bin` path after download
{% endfile %}
{% endtab %}
{% endtabs %}

Download Option 2)

```bash
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/fn
chmod +x fn
mv fn /usr/local/bin/
```

### Auto Safety Clean[​](https://wiki.findora.org/docs/validators/update-version#auto-safety-clean) <a href="#auto-safety-clean" id="auto-safety-clean"></a>

Use the following scripts to clean the data and restart the validator. Please note that this script WILL NOT clean your validator ID and wallet data.



{% tabs %}
{% tab title="Mainnet" %}
{% file src="../../.gitbook/assets/safety_clean_mainnet.sh" %}
{% endtab %}

{% tab title="Testnet" %}
{% file src="../../.gitbook/assets/safety_clean_testnet.sh" %}
{% endtab %}
{% endtabs %}

Example:

```bash
bash -x safety_clean_testnet.sh
```



The `Auto Safety Clean` script above will:

```
1. Get the latest image version number 
2. Stop the exist findorad docker container
3. Remove the existing data (data only, not the keys)
    rm -rf "${ROOT_DIR}/findorad"
    rm -rf "${ROOT_DIR}/tendermint/data"
    rm -rf "${ROOT_DIR}/tendermint/config/addrbook.json"
4. Download the latest data from Findora mv to the data folders.
5. Start a new container with the latest version
6. Output the container status and image version
```


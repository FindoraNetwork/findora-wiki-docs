---
description: >-
  The safety clean script can be used as a last resort to obtain the latest
  version, wipe the node of stale data, and download the latest database.
---

# Emergency Recovery

## Auto Safety Clean[​](https://wiki.findora.org/docs/validators/update-version#auto-safety-clean) <a href="#auto-safety-clean" id="auto-safety-clean"></a>

Use the following scripts to clean the data and restart the validator. Please note that this script WILL NOT clean your validator ID and wallet data.

{% hint style="warning" %}
<mark style="color:red;">**Expect a long period of downtime while the database is downloaded.**</mark>
{% endhint %}

### **Option #1 - Automatic**

Download the `safety_clean` script to your node using `wget`.

{% tabs %}
{% tab title="Mainnet" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/safety_clean_mainnet.sh
```
{% endcode %}
{% endtab %}

{% tab title="Testnet" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/safety_clean_mainnet.sh
```
{% endcode %}
{% endtab %}
{% endtabs %}

Run the script.

{% tabs %}
{% tab title="Mainnet" %}
```
bash -x safety_clean_mainnet.sh
```
{% endtab %}

{% tab title="Testnet" %}
```
safety_clean_testnet.sh
```
{% endtab %}
{% endtabs %}

### **Option #2 - Manual**

Download and manually transfer the script to your node.

{% tabs %}
{% tab title="Mainnet" %}
{% file src="../../.gitbook/assets/safety_clean_mainnet.sh" %}
{% endtab %}

{% tab title="Testnet" %}
{% file src="../../.gitbook/assets/safety_clean_testnet.sh" %}
{% endtab %}
{% endtabs %}

Run the script at the directory where the file has been transferred.

{% tabs %}
{% tab title="Mainnet" %}
```
bash -x safety_clean_mainnet.shbash -x safety_clean_mainnet.shbash -x safety_clean_mainnet.shbash -x safety_clean_mainnet.sh
```
{% endtab %}

{% tab title="Testnet" %}
```
bash -x safety_clean_testnet.sh
```
{% endtab %}
{% endtabs %}

#### Expectations

The `Auto Safety Clean` script will:

```
1. Get the latest image version number 
2. Stop the exist findorad docker container
3. Remove the existing data (data only, not the keys)
    rm -rf "${ROOT_DIR}/findorad"
    rm -rf "${ROOT_DIR}/tendermint/data"
    rm -rf "${ROOT_DIR}/tendermint/config/addrbook.json"
4. Download the latest data from Findora and mv to the data folders.
5. Start a new container with the latest version
6. Output the container status and image version
```

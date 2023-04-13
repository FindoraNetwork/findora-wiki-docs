# Node Upgrades

{% hint style="warning" %}
An upgrade window for major version upgrade v0.3.42 has been scheduled for **April** **10th, 2023** through **April 14th, 2023**. <mark style="color:red;">This upgrade is mandatory for all node operators.</mark>
{% endhint %}

**IMPORTANT UPGRADE NOTES ⤵️**

> Node operators can begin updating their validator binary version on Thursday, April 13th, 2023 at 12 PM Pacific. Upgrading must be completed by Monday, April 24th, by block height 4,033,522.&#x20;
>
> To upgrade, run the script using the **`Update Binary Version via Docker`** instructions below. These steps will automatically update your validator to version v0.3.42.&#x20;
>
> <mark style="color:red;">**Expect a few minutes of downtime while the upgrade is performed.**</mark>

## Update Binary Version via Docker[​](https://wiki.findora.org/docs/validators/update-version#update-image-version) <a href="#update-image-version" id="update-image-version"></a>

### **Option #1 - Automatic**

Run the command below to download the upgrade script to your node.

{% tabs %}
{% tab title="Mainnet" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget -O update_version_mainnet.sh https://raw.githubusercontent.com/FindoraNetwork/findora-wiki-docs/main/.gitbook/assets/update_version_mainnet.sh
```
{% endcode %}
{% endtab %}

{% tab title="Testnet" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget -O update_version_testnet.sh https://raw.githubusercontent.com/FindoraNetwork/findora-wiki-docs/main/.gitbook/assets/update_version_testnet.sh
```
{% endcode %}
{% endtab %}
{% endtabs %}

**✅ Completed**: Use WGET to download the latest binary.

Run the command below to run the update script and upgrade your node.

{% code title="Enter the following command:" overflow="wrap" %}
```
bash -x update_version_mainnet.sh
```
{% endcode %}

The latest version will be displayed as output on your node once completed.

**✅ Completed**: Use BASH to run the update script and upgrade your node. Confirm the version.

### **Option #2 - Manual**

Download the script and transfer it to your node manually.

{% tabs %}
{% tab title="Mainnet" %}
{% file src="../../.gitbook/assets/update_version_mainnet.sh" %}
{% endtab %}

{% tab title="Testnet" %}
{% file src="../../.gitbook/assets/update_version_testnet.sh" %}
{% endtab %}
{% endtabs %}

**✅ Completed**: Download and manually transfer the update script to your node,.

Run the command below to run the update script and upgrade your node. Enter the command at the directory where the file has been transferred.

```bash
bash -x update_version_mainnet.sh
```

**✅ Completed**: Run the update script and update your node.

### Expectations

The `Update Image Version` script will:

```
1. Retrieve the latest version number all validators should run.
2. Stop the existing `findorad` docker container.
3. Start a new Docker container with the latest version.
4. Output the Docker container status and image version.
```

To confirm if the upgrade worked correctly, the output of the script will display:

1. Node status.&#x20;
2. Running image version.

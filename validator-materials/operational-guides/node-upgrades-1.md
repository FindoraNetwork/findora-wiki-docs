---
description: >-
  Run the steps below to perform an upgrade on your Findora node using the
  Validator Toolbox.
---

# Node Upgrade (Toolbox)



{% hint style="warning" %}
An upgrade window for version upgrade **v0.3.42** has been scheduled for **April** **10th, 2023** through **April 14th, 2023**. <mark style="color:red;">This upgrade is mandatory for all node operators.</mark>
{% endhint %}

**IMPORTANT UPGRADE NOTES ⤵️**

> Node operators can begin updating their validator binary version on Thursday, April 13th, 2023 at 12 PM Pacific. Upgrading must be completed by Monday, April 24th, by block height 4,033,522.&#x20;
>
> To upgrade, run the script using the **`Update Binary Version via Docker`** instructions below. These steps will automatically update your validator to version v0.3.42.&#x20;
>
> <mark style="color:red;">**Expect a few minutes of downtime while the upgrade is performed.**</mark>

## Update Binary Version via Docker[​](https://wiki.findora.org/docs/validators/update-version#update-image-version) <a href="#update-image-version" id="update-image-version"></a>

Step1: Run the command below to download the upgrade script to your node.

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

Step 2: Run the command below to run the update script and upgrade your node.

{% code title="Enter the following command:" overflow="wrap" %}
```
bash -x update_version_mainnet.sh
```
{% endcode %}

The latest version will be displayed as output on your node once completed.

**✅ Completed**: Use BASH to run the update script and upgrade your node. Confirm the version.

Step 3: Once the upgrade script completes, run the following command to ensure your node is running the updated release.

{% code title="Enter the following command:" %}
```
docker ps
```
{% endcode %}

Ensure part of the output displays `findoranetwork/findorad:v0.3.xx-release` where "xx" is the minor release number.&#x20;

{% hint style="info" %}
See above for the most up-to-date version.
{% endhint %}

**✅ Completed**: Ensure your node is upgraded.

### Expectations

The `Update Image Version` script will:

```
1. Retrieve the latest version number all validators should run.
2. Stop the existing `findorad` docker container.
3. Start a new Docker container with the latest version.
4. Output the Docker container status and image version.
```

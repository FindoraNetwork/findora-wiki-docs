---
description: >-
  Findora Node Setup (fn) is a command-line (CLI) utility that allows you to
  perform wallet operations such as staking and unstaking FRA.
---

# fn CLI Upgrade (Wallet)

## Upgrade the fn CLI Tool[​](https://wiki.findora.org/docs/validators/automated-setup#setup-the-fn-cli-tool) <a href="#setup-the-fn-cli-tool" id="setup-the-fn-cli-tool"></a>

You can download the `fn` tool using one of the two options below.

{% hint style="info" %}
For Mac and Linux users, you must move the `fn` tool to the `/usr/local/bin/` path.
{% endhint %}

### Option #1 - Automatic

Run `wget` command below download the latest fn CLI to your node.

{% tabs %}
{% tab title="Linux" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/fn
```
{% endcode %}
{% endtab %}

{% tab title="MacOS" %}
{% code title="Enter the following command:" overflow="wrap" %}
```
wget https://github.com/FindoraNetwork/findora-wiki-docs/raw/main/.gitbook/assets/fn-mac
```
{% endcode %}
{% endtab %}
{% endtabs %}

Run `chmod` command below to apply the appropriate permissions to the file.

{% tabs %}
{% tab title="Linux" %}
{% code title="Enter the following command:" %}
```
chmod +x fn
```
{% endcode %}
{% endtab %}

{% tab title="MacOS" %}
{% code title="Enter the following command:" %}
```
chmod +x fn-mac
```
{% endcode %}
{% endtab %}
{% endtabs %}

Move the file to the appropriate location with `mv`.

{% tabs %}
{% tab title="Linux" %}
```
mv fn /usr/local/bin/
```
{% endtab %}

{% tab title="MacOS" %}
```
mv fn-mac /usr/local/bin/
```
{% endtab %}
{% endtabs %}

### Option #2 - Manual

Download the file below and manually transfer it to your node.

{% tabs %}
{% tab title="Linux" %}
{% file src="../../.gitbook/assets/fn" %}
{% endtab %}

{% tab title="MacOS" %}
{% file src="../../.gitbook/assets/fn-mac" %}
{% endtab %}
{% endtabs %}

Move the binary file to the appropriate directory once it file is downloaded and manually transferred to your node. Run this at the directory where the file was trasferred.

{% tabs %}
{% tab title="Linux" %}
```
mv fn /usr/local/bin/mv fn /usr/local/bin/
```
{% endtab %}

{% tab title="MacOS" %}
```
mv fn-mac /usr/local/bin/
```
{% endtab %}
{% endtabs %}

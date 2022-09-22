# Version Update

### Update Image Version[​](https://wiki.findora.org/docs/validators/update-version#update-image-version) <a href="#update-image-version" id="update-image-version"></a>

The following scripts can be used in any environment to update the image version.

{% tabs %}
{% tab title="Mainnet" %}
{% file src="../.gitbook/assets/update_version_mainnet.sh" %}
{% endtab %}

{% tab title="Testnet" %}
{% file src="../.gitbook/assets/update_version_testnet.sh" %}
{% endtab %}
{% endtabs %}

Example:

```bash
bash -x version_update_testnet.sh
```

### Auto Safety Clean[​](https://wiki.findora.org/docs/validators/update-version#auto-safety-clean) <a href="#auto-safety-clean" id="auto-safety-clean"></a>

Use the following scripts to clean the data and restart the validator. Please note that this script WILL NOT clean your validator ID and wallet data.

Before running the script, make sure to set Environment Path Variables. Set `$ROOT_DIR` to the same path as used in the setup.

{% tabs %}
{% tab title="Mainnet" %}
{% file src="../.gitbook/assets/safety_clean_mainnet.sh" %}
{% endtab %}

{% tab title="Second Tab" %}
{% file src="../.gitbook/assets/safety_clean_testnet.sh" %}
{% endtab %}
{% endtabs %}

Example:

```bash
bash -x safety_clean_testnet.sh
```

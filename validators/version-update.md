# Version Update

### Update Image Version[​](https://wiki.findora.org/docs/validators/update-version#update-image-version) <a href="#update-image-version" id="update-image-version"></a>

The following scripts can be used in any environment to update the image version.

* For Testnet: [**version\_update\_testnet.sh**](https://wiki.findora.org/assets/files/update\_version\_testnet-dd5f8a00487245157643c8144516d29f.sh)
* For Mainnet: [**version\_update\_mainnet.sh**](https://wiki.findora.org/assets/files/update\_version\_mainnet-4f20384f16d1f0e2d90e1f7ebc7ea935.sh)

Example:

```bash
bash -x version_update_testnet.sh
```

### Auto Safety Clean[​](https://wiki.findora.org/docs/validators/update-version#auto-safety-clean) <a href="#auto-safety-clean" id="auto-safety-clean"></a>

Use the following scripts to clean the data and restart the validator. Please note that this script WILL NOT clean your validator ID and wallet data.

Before running the script, make sure to set Environment Path Variables. Set `$ROOT_DIR` to the same path as used in the setup.

* For Testnet: [**safety\_clean\_testnet.sh**](https://wiki.findora.org/assets/files/safety\_clean\_testnet-6ff123c1a085fd2cd9cbdc2152f6b6f5.sh)
* For Mainnet:[**safety\_clean\_mainnet.sh**](https://wiki.findora.org/assets/files/safety\_clean\_mainnet-029f3d60993cc8317a3d767bfc504236.sh)

Example:

```bash
bash -x safety_clean_testnet.sh
```

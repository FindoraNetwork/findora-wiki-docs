---
description: Backup Files & Migration with Toolbox
---

# Additional Info

## Backup Files

Toolbox copies all files you need to backup into the folder `~/findora_backup` every time you launch it.

Save this folder somewhere safe and always keep it private. You will need it for recovery or migrating servers.

Here's a list of files you'll need to migrate to a new server that we include:

{% tabs %}
{% tab title="mainnet" %}
{% code lineNumbers="true" %}
```bash
~/tmp.gen.keypair
/data/findora/mainnet/node.mnemonic
/data/findora/mainnet/mainnet_node.key
/data/findora/mainnet/tendermint/config/
```
{% endcode %}
{% endtab %}

{% tab title="testnet" %}
```
~/tmp.gen.keypair
/data/findora/testnet/node.mnemonic
/data/findora/testnet/mainnet_node.key
/data/findora/testnet/tendermint/config/
```
{% endtab %}
{% endtabs %}

## Migrate your server via Validator Toolbox

To migrate via validator toolbox, use the toolbox to install a brand new node on your new server. Let it fully sync up with the blockchain and now you're ready to use the toolbox to convert this new server over to using your old validator keys and files.

We've built a migration tool into the validator toolbox. To activate this feature create a folder named \~/migrate and using your **old server files** place the **tmp.gen.keypair** file inside along with a copy of your **tendermint/config** folder. Your \~/migrate folder should look like this:

```
~/migrate/tmp.gen.keypair~/migrate/config
```

Once those files are in place you can shut down your old server to **avoid double signing** as you're ready to flip the new server to your old file and start signing instantly.

After shutting down your old server, restart the validator toolbox and you will see option 888 available to migrate your server files to the new validator node.

After running it you'll be up and online almost instantly as you let it sync up and keep running without stopping it except for a moment when we change your keys over.

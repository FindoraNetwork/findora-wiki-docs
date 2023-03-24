---
description: Toolbox will install on existing validators.
---

# Existing Build

### Install Requirements

You will need to install a few packages to be able to run the toolbox on an existing validator server. Run the following command to install packages used:

```bash
sudo apt install python3-pip python3-dotenv git -y
```

### Pull script & Run Installer

Our menu will launch and ask you a few simple questions to get you fully loaded and online. Run the following code to pull and setup `findora.sh` our main script:

{% tabs %}
{% tab title="Start Toolbox Setup" %}
```bash
cd ~/ && wget https://raw.githubusercontent.com/FindoraNetwork/findora-toolbox/main/src/bin/findora.sh && chmod +x findora.sh
```
{% endtab %}
{% endtabs %}

### Launching Toolbox

Once `findora.sh` is downloaded and configured to run, the command below is used to launch the full toolbox menu. This will pull the latest updates for toolbox each time it is launched.

```bash
cd ~/ && ./findora.sh
```

Running the toolbox will present a screen similar to the image below.

<figure><img src="../../../.gitbook/assets/image (5) (3).png" alt=""><figcaption><p>Main Menu</p></figcaption></figure>

{% hint style="info" %}
See below for notes on each option presented in the full menu.&#x20;
{% endhint %}

{% hint style="warning" %}
Keep in mind that options 8, 9, 10, and 999 may result in missed blocks!
{% endhint %}

| Option |          Function         | Notes                                                                                             |
| ------ | :-----------------------: | ------------------------------------------------------------------------------------------------- |
| 1      |   Show 'curl' stats info  | Shows output of `curl 'http://localhost:26657/status'`, most info will be moved to the front page |
| 2      |    Show 'fn' stats info   | Shows output of `fn show`, most info will be moved to the front page                              |
| 3      |     Claim Pending FRA     | Claim your pending rewards                                                                        |
| 4      |        Transfer FRA       | Send your FRA to another address                                                                  |
| 5      | Set Transfer Options Menu | A menu to configure your transfer options                                                         |
| 6      |  Change Rate or Info Menu | A menu to configure your rate or update your validator's info via staker\_memo                    |
| 7      |  Update `fn` Application  | Pull and update to the latest version of the `fn` application                                     |
| 8      |  Update Findora Container | Pull latest version, re-create and restart local server container, you may miss blocks            |
| 9      |      Run Safety Clean     | Runs the safety\_clean script, wipes database, preserves wallet info, full reset of system        |
| 10     |  Update Operating System  | Safely stops your container before running updates, you may miss blocks                           |
| 11     |   Show system disk info   | Info about hard drive space!                                                                      |
| 12     |   TMI about your Server   | All of the hardware information on your VPS                                                       |
| 999    |       Reboot Server       | Safely stop your container & reboot your server. You will miss blocks with this option!           |

### Help Menu

See the help menu options anytime with the following command:

```
./findora.sh -h
```

<figure><img src="../../../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

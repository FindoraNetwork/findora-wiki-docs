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

<table><thead><tr><th width="112">Option</th><th align="center">Function</th><th>Notes</th></tr></thead><tbody><tr><td>1</td><td align="center">Show 'curl' stats info</td><td>Shows output of <code>curl 'http://localhost:26657/status'</code>, most info will be moved to the front page</td></tr><tr><td>2</td><td align="center">Show 'fn' stats info</td><td>Shows output of <code>fn show</code>, most info will be moved to the front page</td></tr><tr><td>3</td><td align="center">Claim Pending FRA</td><td>Claim your pending rewards</td></tr><tr><td>4</td><td align="center">Transfer FRA</td><td>Send your FRA to another address</td></tr><tr><td>5</td><td align="center">Set Transfer Options Menu</td><td>A menu to configure your transfer options</td></tr><tr><td>6</td><td align="center">Change Rate or Info Menu</td><td>A menu to configure your rate or update your validator's info via staker_memo</td></tr><tr><td>7</td><td align="center">Update <code>fn</code> Application</td><td>Pull and update to the latest version of the <code>fn</code> application</td></tr><tr><td>8</td><td align="center">Update Findora Container</td><td>Pull latest version, re-create and restart local server container, you may miss blocks</td></tr><tr><td>9</td><td align="center">Run Safety Clean</td><td>Runs the safety_clean script, wipes database, preserves wallet info, full reset of system</td></tr><tr><td>10</td><td align="center">Update Operating System</td><td>Safely stops your container before running updates, you may miss blocks</td></tr><tr><td>11</td><td align="center">Show system disk info</td><td>Info about hard drive space!</td></tr><tr><td>12</td><td align="center">TMI about your Server</td><td>All of the hardware information on your VPS</td></tr><tr><td>999</td><td align="center">Reboot Server</td><td>Safely stop your container &#x26; reboot your server. You will miss blocks with this option!</td></tr></tbody></table>

### Help Menu

See the help menu options anytime with the following command:

```
./findora.sh -h
```

<figure><img src="../../../.gitbook/assets/image (1) (1) (2) (2).png" alt=""><figcaption></figcaption></figure>

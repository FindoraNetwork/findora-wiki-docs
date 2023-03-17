---
description: >-
  The example below shows how to acquire a virtual server running on Contabo, a
  cloud provider with affordable rates.
---

# Acquire a Server

Running a validator on Findora requires you have a server running 24x7x365. We suggest using a cloud provider and virtual server to run your node, but a personal server would suffice as well.&#x20;

## Step 1: Get a server

To run a validator you need a server can run 24x7. You can run on your personal server or get one from cloud provider such as AWS, GCP and Azure.

{% hint style="info" %}
We do not recommend using your home computer. Issues with your home computer software, hardware, connection, or power will create downtime for your node and your stake will be slashed as a result.
{% endhint %}

If you do not have a server now, we suggest rent a VPS on Contabo.&#x20;

Click this [link](https://contabo.com/en/vps/vps-l-ssd?addons=1415\&image=ubuntu.267\&qty=1\&contract=3\&storage-type=vps-l-800-gb-ssd) to rent a server.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

As an example, the Contabo VPS L server meets the recommended specs to run a Findora validator node. The minimum storage required for Findora Mainnet Validator is 200GB, but we suggest opting for 400GB NVMe for peace of mind.&#x20;

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Entry a password and keep all other options default.&#x20;

Once you have acquired a server, you may proceed to setting up your new validator on Findora.&#x20;

## Step 2: Node Setup

Two options are available for you when it comes to the setup:

* ****[**Manual Setup**](manual-setup.md)****
  * This method walks you through the process, step-by-step, one command at a time. This is recommended for first timers as you get to learn the process before taking shorter, easier paths.
* ****[**Toolbox Setup**](toolbox-setup/)****
  * This method uses a toolbox to do much of the heavy lifting for you. The toolbox provides you with a set of tools for managing and troubleshooting your validator.&#x20;

{% hint style="info" %}
You can install the toolbox separately after following the steps in Manual Setup.
{% endhint %}

Proceed with one of the options above to setup a validator on your new server.

---
description: >-
  This guide walks through how to deploy a local blockchain instance for
  software development and testing purposes. Alternatively, developers can also
  develop and test on Anvil Testnet.
---

# Development Network

### 1. Prerequisites[​](https://wiki.findora.org/docs/developers/development\_network#1-prerequisites) <a href="#1-prerequisites" id="1-prerequisites"></a>

#### i) Install Golang[​](https://wiki.findora.org/docs/developers/development\_network#i-install-golang) <a href="#i-install-golang" id="i-install-golang"></a>

[https://go.dev/doc/install](https://go.dev/doc/install)

**Tips for Linux (Ubuntu)**[**​**](https://wiki.findora.org/docs/developers/development\_network#tips-for-linux-ubuntu)

<pre class="language-bash"><code class="lang-bash"><strong>#first command needs to be run as root, rest as your normal user
</strong>wget https://go.dev/dl/go1.18.3.linux-amd64.tar.gz 
sudo su 
rm -rf /usr/local/go &#x26;&#x26; tar -C /usr/local -xzf go1.18.3.linux-amd64.tar.gz

#exit root now
exit

#add to path. For more permanent you should add this line to bottom of your ~/.profile
export PATH=$PATH:/usr/local/go/bin

#check go version
go version</code></pre>

#### ii) Install Rust <a href="#ii-install-rust" id="ii-install-rust"></a>

[https://rustup.rs/](https://rustup.rs/)

If already installed, please update to 1.59 or newer

```bash
rustup update
```

#### iii) Install System Specific Dependencies <a href="#iii-install-system-specific-dependencies" id="iii-install-system-specific-dependencies"></a>

{% tabs %}
{% tab title="Ubuntu" %}
```bash
sudo apt update && \
sudo apt upgrade -y && \
sudo apt install -y build-essential libleveldb-dev libssl-dev pkg-config clang libclang-dev librocksdb-dev
```
{% endtab %}

{% tab title="Second Tab" %}
```bash
brew install openssl leveldb​
```
{% endtab %}
{% endtabs %}

### 2. Build Required Binaries[​](https://wiki.findora.org/docs/developers/development\_network#2-build-required-binaries) <a href="#2-build-required-binaries" id="2-build-required-binaries"></a>

Findora blockchain can run on both MacOS or Linux. The commands below will build all required binaries to start a local Findora blockchain.

```bash
git clone -b v0.3.19-release https://github.com/FindoraNetwork/platform &&
cd platform &&
make build_release
```

Please make sure to add all below 3 binaries to your `$PATH`. By default, they will be copied to `~/.cargo/bin/` which should already be in your `$PATH`.

* `stt`: The tool to initialize Findora blockchain.
* `abcid`: Findora core protocol.
* `tendermint`: Tendermint consensus engine.

### 3. Install Python3 and toml-cli[​](https://wiki.findora.org/docs/developers/development\_network#3-install-python3-and-toml-cli) <a href="#3-install-python3-and-toml-cli" id="3-install-python3-and-toml-cli"></a>

Findora devnet tools are written in Python3 and use `toml-cli` to manipulate configuration files. [Install Python3](https://www.python.org/downloads/) if not already installed. Also, install `toml-cli` using the command below:

```bash
pip3 install toml-cli
```

and then copy newly installed `toml` cli tool to `/usr/local/bin` to make it visible

```bash
cp /Library/Python/3.x/site-packages/toml /usr/local/bin
```

### 4. Run Devnet[​](https://wiki.findora.org/docs/developers/development\_network#4-run-devnet) <a href="#4-run-devnet" id="4-run-devnet"></a>

Inside your `platform` directory, execute `make devnet` in the terminal.

<figure><img src="https://wiki.findora.org/img/make-devnet.png" alt=""><figcaption></figcaption></figure>

#### i) What's in devnet?[​](https://wiki.findora.org/docs/developers/development\_network#i-whats-in-devnet) <a href="#i-whats-in-devnet" id="i-whats-in-devnet"></a>

| Name   | Description                 |
| ------ | --------------------------- |
| node0  | The validator               |
| node1  | The fullnode                |
| Faucet | The key pair that holds FRA |

#### ii) How to control devnet?[​](https://wiki.findora.org/docs/developers/development\_network#ii-how-to-control-devnet) <a href="#ii-how-to-control-devnet" id="ii-how-to-control-devnet"></a>

The local blockchain can be stopped and restarted anytime during development and tests.

* Stop Blockchain: `./tools/devnet/stopnodes.sh`
* Restart Blockchain: `./tools/devnet/startnodes.sh`
* Start Over: `make devnet` again.

<figure><img src="https://wiki.findora.org/img/stop-start-devnet.png" alt=""><figcaption></figcaption></figure>

### 5. Devnet URLs and Ports[​](https://wiki.findora.org/docs/developers/development\_network#5-devnet-urls-and-ports) <a href="#5-devnet-urls-and-ports" id="5-devnet-urls-and-ports"></a>

| URL                                             | Purpose                                                            |
| ----------------------------------------------- | ------------------------------------------------------------------ |
| [http://127.0.0.1](http://127.0.0.1/)           | connects to [Findora Electron Wallet](https://wallet.findora.org/) |
| [http://127.0.0.1:8545](http://127.0.0.1:8545/) | connects to Web3 HTTP                                              |
| [http://127.0.0.1:8546](http://127.0.0.1:8546/) | connects to Web3 WebSocket                                         |

### 6. Troubleshoot[​](https://wiki.findora.org/docs/developers/development\_network#6-troubleshoot) <a href="#6-troubleshoot" id="6-troubleshoot"></a>

* Problem 1
  * Error Message:
    * `make build_release fails with go:linkname must refer to declared function or variable`
*   Solution

    *   Update your golang.org/x/sys

        ```bash
        # go to platform/tools/tendermint run following to update  
        go get -u golang.org/x/sys
        ```

    ***
* Problem 2
  * `.findora` file is missing
* Solution
  * manually add `.findora` to your home directory (i.e. directory `~`)

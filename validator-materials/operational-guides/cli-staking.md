# CLI Staking

Validators must stake a minimum of 10,000 FRA to register as a validator. Before you can stake FRA to your validator, you must first transfer FRA to the `Findora Address` (i.e. wallet address) of your validator.

### Funding[​](https://wiki.findora.org/docs/validators/staking-guide#funding) <a href="#funding" id="funding"></a>

#### Testnet Funding[​](https://wiki.findora.org/docs/validators/staking-guide#testnet-funding) <a href="#testnet-funding" id="testnet-funding"></a>

You can request Testnet FRA tokens using our Discord Bot. Please [follow this guide](../../general-user-materials/request-fra-testnet.md) to claim your free FRA Native Chain tokens.

While requesting the tokens, you need to specify the `Findora Address` associated with your validator node. To locate this wallet address, run `fn show`, and get your fra address as displayed in the screenshot below.

<figure><img src="../../.gitbook/assets/image (1) (4).png" alt=""><figcaption></figcaption></figure>

#### Mainnet Funding[​](https://wiki.findora.org/docs/validators/staking-guide#mainnet-funding) <a href="#mainnet-funding" id="mainnet-funding"></a>

Transfer FRA from an existing Findora wallet to your `Findora Address`. If you don’t have FRA tokens, you can buy them from any exchange listed on [this page](https://coinmarketcap.com/currencies/findora/markets/).

### Node Operations[​](https://wiki.findora.org/docs/validators/staking-guide#node-operations) <a href="#node-operations" id="node-operations"></a>

#### fn CLI tool[​](https://wiki.findora.org/docs/validators/staking-guide#fn-cli-tool) <a href="#fn-cli-tool" id="fn-cli-tool"></a>

Besides node setup, the `fn` tool is also used for general validator staking operations such as staking FRA into the validator, setting the commission rate the validator charges, transferring FRA balance on the validator to another wallet address and claiming FRA rewards.

To see the list of all sub-commands under `fn` use the `--help` flag as shown below:

```bash
fn --help
```

To get detailed info about a specific sub-command, use the `--help` flag along with the command.

Example: `fn stake --help`

```bash
fn-stake
  Stake tokens (i.e. bond tokens) from a Findora account to a Validator

USAGE:
  fn stake [FLAGS] [OPTIONS] --amount <Amount>

FLAGS:
    -a, --append     stake more FRAs to your node
        --force      ignore warning and stake FRAs to your target node
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -n, --amount <Amount>                      how much `FRA unit`s you want to stake
    -R, --commission-rate <Rate>               the commission rate of your node, a float number from 0.0 to 1.0
    -S, --staker-priv-key <SecretKey>          the file which contains private key (in base64 format) of proposer
    -M, --validator-memo <Memo>                the description of your node, optional
    -A, --validator-td-addr <TendermintAddr>   stake FRAs to a custom validator
```

> Other Examples:\
> \> `fn unstake --help`\
> \> `fn claim --help`\
> \> `fn transfer --help`

#### Stake Initial FRA and Set Commission Rate[​](https://wiki.findora.org/docs/validators/staking-guide#stake-initial-fra-and-set-commission-rate) <a href="#stake-initial-fra-and-set-commission-rate" id="stake-initial-fra-and-set-commission-rate"></a>

After receiving FRA to your validator's `Findora Address`, you must stake a minimum of 10,000 FRA to become a validator. Only the top 100 validators (with the most FRA staked) will earn FRA rewards.

> **Tip**: Before staking, wait for 100% data synchronization of your validator node, otherwise you may be charged a 'validator node offline' penatly fee.

```bash
# - Your Staker Memo file should like this:
cat staker_memo

{
  "name": "ExampleNode",
  "desc": "I am just a example description, please change me.",
  "website": "https://www.example.com",
  "logo": "https://www.example.com/logo"
}
```

```bash
# ex)
# - To stake 999,999 FRAs with a commision rate of 2% (and validator name of Validator_Pool_A)
# - Note: that is 999999 * 1000000 FRA units
fn stake -n $((999999 * 1000000)) -R 0.02 -M "$(cat staker_memo)"
```

#### Stake Additional FRA[​](https://wiki.findora.org/docs/validators/staking-guide#stake-additional-fra) <a href="#stake-additional-fra" id="stake-additional-fra"></a>

```bash
# Stake an additional 2,000 FRA to your validator
fn stake -a -n $((2000 * 1000000))
```

#### View Node Information[​](https://wiki.findora.org/docs/validators/staking-guide#view-node-information) <a href="#view-node-information" id="view-node-information"></a>

To find information about your validator node, use the `fn show` command. Sample output is below:

<figure><img src="../../.gitbook/assets/image (8) (3).png" alt=""><figcaption></figcaption></figure>

#### Claim FRA Rewards[​](https://wiki.findora.org/docs/validators/staking-guide#claim-fra-rewards) <a href="#claim-fra-rewards" id="claim-fra-rewards"></a>

Top 100 validators will earn block rewards. If your validator is a top 100 validator, it will earn rewards which will show up in the `rewards` section on `fn show`.

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

If your reward balance is greater than 0, you can claim your earned rewards via the `fn claim` sub-command

```bash
# fn claim -n <the amount of FRA units you want>
# ex)
#   If you have a reward balance of 20 FRA (i.e. "rewards: 20000000")
#   and wish to claim 10 FRA (out of 20 FRA), issue the command below:
fn claim -n $((10 * 1000000))
```

#### Unstake FRA[​](https://wiki.findora.org/docs/validators/staking-guide#unstake-fra) <a href="#unstake-fra" id="unstake-fra"></a>

**Unstake Some of Your FRA**[**​**](https://wiki.findora.org/docs/validators/staking-guide#unstake-some-of-your-fra)

```bash
# fn unstake -n <the amount of FRA units you want>
# ex)
#   To unstake 900 FRA (ie. 900 * 1000000)
fn unstake -n $((900 * 1000000))
```

**Close Validator and Unstake All of Your FRA**[**​**](https://wiki.findora.org/docs/validators/staking-guide#close-validator-and-unstake-all-of-your-fra)

> **NOTE**: This operation will unstake all of your FRA and remove your node from the Findora Network.

```bash
fn unstake
```

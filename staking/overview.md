---
description: >-
  Findora is an open, permissionless blockchain secured by a decentralized
  network of global validators running the Tendermint consensus mechanism. Like
  other proof of stake (PoS) blockchains, the main
---

# Overview

### Staking[​](https://wiki.findora.org/docs/modules/staking/overview#staking) <a href="#staking" id="staking"></a>

Staking FRA tokens allows validators to participate in consensus voting process. To participate, FRA tokens are staked by validators into a PoS contract where the tokens are bonded and subject an unbonding period of 113,400 blocks (roughly 21-22 days) if the validator decides to stop participating in the consensus process. Validators are subjects to slashing penalties during this unbonding period. Notably, the unbonding period exists in order to disincentivize validators from engaging in malicious activities such as a long-range attack (i.e. forking the blockchain and becoming a validator for both the original blockchain and forked (i.e. "fake") blockchain.

Staked tokens are eligible for Block Rewards and subject to slashing penalties.

### Validators[​](https://wiki.findora.org/docs/modules/staking/overview#validators) <a href="#validators" id="validators"></a>

FRA token holders can earn additional FRA reward tokens by setting up their own validator, which is a special type of full node that participates in the consensus voting process. Consensus voting is a critical part of writing the next block on Findora. Validators must `stake` their FRA tokens (i.e. lock the tokens into a bond deposit which is subject to a 113,400 block unbonding period (roughly 21-22 days) if the validator decides to later unstake the tokens). If bonded tokens end up being used to vote duplicitously (i.e. for two conflicting commit-vote signatures), the validator's bonded tokens will be slashed (i.e. deducted from the validator's wallet balance and burned as a penalty). Thus, bonding tokens during the staking process is critical to incentivizing honest participation in the consensus process.

Validator consensus voting follows the Tendermint consensus ruleset which is based on Byzantine Consensus algorithm for asynchronous systems. To incentivize validators to participate in the voting process, they are eligible to earn block rewards for their efforts and the block rewards (probabilistically) paid to validators is directly proportional to the FRA staked by the validator.

Validators are selected from the pool of validators candidates based on the number of FRA staked. Only the validators in the top 100 in terms of FRA staked will participate in the consensus voting process.

### Delegators[​](https://wiki.findora.org/docs/modules/staking/overview#delegators) <a href="#delegators" id="delegators"></a>

FRA holders that do not want to set up their own validator to directly stake FRA can instead delegate their tokens to a validator to be staked on their behalf. After paying a commission fee, delegators also earn block rewards.

### Block Rewards and Slashing Penalties[​](https://wiki.findora.org/docs/modules/staking/overview#block-rewards-and-slashing-penalties) <a href="#block-rewards-and-slashing-penalties" id="block-rewards-and-slashing-penalties"></a>

Block rewards exist to incentivize the secure, decentralized participation of 3rd party validators to create the next block. Intentionally malicious or incompetent validators who double sign transactions or offer low availability to participate in consensus voting are punished thru slashing penalties.

See the [Rewards](rewards.md) and [Penalties](penalties.md) documents for details.

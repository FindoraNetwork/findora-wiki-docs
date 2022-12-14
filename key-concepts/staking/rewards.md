# Rewards

Staking your FRA to become an active member of the Findora protocol comes with responsibility and rewards. By design, Findora rewards are non-inflationary and the protocol allocates a 2% (420 million FRA) of its total circulating supply to fund incentives. This ensures that the network is grounded well enough until transaction fees gain traction. These rewards are primarily meant to jump-start the network - the network will in the long run sustain itself and reward validators via transaction fees.

The Findora network has two set of incentives - the block rewards and the block proposer rewards.

Block rewards are incentives given to validators that successfully write a block to the network but they come with certain cavaets. A pro-rata share in the amount of FRA staked is equivalent to the chance of being selected to write a new block. This means if a validator has more FRA staked that other validators, they automatically have more chances of writing the next block than other validators ergo more of a chance to earn the block reward. Also, the validator that proposes the block gets all the reward. This means that the node doesn't have to share their rewards with other validators in the network.

Block Proposer Rewards are secondary rewards paid out not only to the validator that proposes a block but every validator that participates in the process of prevoting and pre-commiting a block, and they are smaller in size.

### Rewards Calculations[​](https://wiki.findora.org/docs/modules/staking/rewards#rewards-calculations) <a href="#rewards-calculations" id="rewards-calculations"></a>

The amount of FRA paid out per block for the a) `Block Reward` and b) `Block Proposer Bonus Reward` is described below.

#### Block Reward Calculation[​](https://wiki.findora.org/docs/modules/staking/rewards#block-reward-calculation) <a href="#block-reward-calculation" id="block-reward-calculation"></a>

The (annual) block reward calculation follows the formula below:

Y = 1 / x \* \[Rate Modifier Constant]

With x and y defined as:

y = Annualized Block Reward Rate

x = % Circulating Supply Staked (i.e. FRA staked / unlocked FRA)

The Rate Modifier Constant is set at `0.0536` (as of 5/1/2022) and is responsible for determining the reward rate for each value of % circulating supply staked. In the future, this rate modifier may be changed based on governance voting by FRA holders.

![](https://i.imgur.com/VHiFR0J.png)

The above formula describes the _annual_ block reward payout rate. However, since the reward is paid out per block, the formula above must be de-annualized down to a per block reward rate. This is done via using the continuous compounding formula in reverse. The block reward rate is recalculated every block.

Block Reward Rate (per block) = (1 + y)^(1/1,855,059)-1

Where 1,855,059 is the number of blocks Findora generates based on a 17s average block time (60_60_24\*365/17).

#### Block Proposer Bonus Reward[​](https://wiki.findora.org/docs/modules/staking/rewards#block-proposer-bonus-reward) <a href="#block-proposer-bonus-reward" id="block-proposer-bonus-reward"></a>

The bonus rewards for the block proposer are calculated based on the following table . These calculations are independant of Block Rewards . The Bonus reward is payed out to further incentives the block proposing validator.

![](https://i.imgur.com/ik5xJp3.png)

### Rewards Distribution[​](https://wiki.findora.org/docs/modules/staking/rewards#rewards-distribution) <a href="#rewards-distribution" id="rewards-distribution"></a>

Block rewards calculated based on the above formulae , Both `Block Reward` and `Block Proposer Bonus Reward` are awarded to the block proposer .

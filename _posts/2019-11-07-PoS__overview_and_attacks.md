# Proof-of-Stake - Overview and Attacks

The Introduction into this article gives an overview about the PoS core concept and different ways to implement this concept. The main part will discuss attacks on Proof-of-Stake networks. 

At first, let us get rid of a common misconception. I also thought this until I wrote this article. In the term Proof-of-Stake the stake refers to the economic meaning of stake. Usually a stakeholder is someone who has a stake in something (like a company). Hence, the stake refers to just a participant in the network who holds a share (usually tokens) from the network. The first PoS networks did not have the concept of staking and take away the stake if a Valdiator misbehaves. Holding tokens in your account was the stake.

## Overview and common concept

Proof-of-Stake (PoS) is a consensus algorithm like e.g. Proof-of-Work. In general, a consensus algorithm (in the context of Blockchains) tries to find an agreement about the current state of the data stored in the Blockchain. 

In Proof-of-Work, accounts called Validators generate and validate new blocks (instead of miners in PoW). For each new block, a network specific **Validator picking algorithm** (it could be purely random) chooses a subset from all available Validators to do the **block generation and verification**. Usually, to prevent Validators to act malicious, a **slashing process** punishes Validators if they act malicious. To punish Validators, there is a **staking/election process** which puts some value at risk (stake/bond) for each Validator. A **rewarding process** rewards correct behavior. Hence, to become a validator there is some kind of **staking process**.

This is the underlying basic concept of PoS. But this basic concept can be achieved in different ways. It is hard to differ all the existing implementations. Additionally, many networks give accounts the **voting rights** on protocol amendments and similar topics. Therefore, this also needs to be part of the classification of different PoS networks.

I will introduce different PoS implementations in the next sections. To do so, it makes sense to find features to classify the PoS networks variants. In the introduction, I already wrote the determining features in bold letters.

The differences in PoS implementations usually are:

- **staking/election process**
  - How does the bonding/staking work?
  - What is the stake? (e.g. Token amount and Coin-age)
  - Can Validator accumulate stakes from other accounts or not (just stake for theirselves)?
- **Validator picking algorithm**
  - How is a Validator picked? (e.g. proportional to the stake or completely random)
- **Block generation and verification**
  - Who generates the block?
  - Who verifies the block?
- **Slashing process** 
  - Who determines malicious behavior and when? (e.g. automatically or manual)
  - Who is punished for misbehavior? (e.g. the account who stakes or the validator)
- **Rewarding process**
  - How is the reward distributed? (e.g. Validator gets all or shared with Stakers)
- **Voting rights**
  - What rights do Validators and token holders have? (e.g. Validators vote on network amendments and propose blocks)

Sources:

[Understanding Proof of Stake: The Nothing at Stake Theory](https://medium.com/coinmonks/understanding-proof-of-stake-the-nothing-at-stake-theory-1f0d71bc027)

## Popular Variants

### Pure Proof-of-Stake (PPoS)

**staking/election process**
- Every account with the required token (stake) is a Validator 
- Stakes are usually token/coins amount and also the coin age could matter
  
**Validator picking algorithm**
- One of the Validators is picked randomly (usually depends on the stake)
- A subset of Validators is picked randomly (usually depends on the stake) to verify the block 

**Block generation and verification**
- The chosen Validator generates the new block
- A subset of Validators validate this block

**Slashing process** 
- No punishment possible because the stake was not bonded/locked

**Rewarding process**
- The Validator gets the reward (Blockreward or/and fees)

**Voting rights**
- Staker vote on protocol amendments etc.


<!-- Implementations:

- PoSv1-3
  - are similar to Bitcoin in that they use the UTXO model and longest chain consensus rules -->


### Bonded Proof-of-Stake (BPoS)

This veriant has only one major difference. The accounts need to bond/lock their stake. In case of misbehavior it will be seized/burned. The following list just highlights the differences to PPoS:

**staking/election process**
- Every account with the required token can become a Validator by bonding/locking their stake
- Accounts bond value only for themselves

**Slashing process** 
- The Validator is punished for malicious behavior
- usually only objective punishment
  

Important note: Everybody can become a Validator by bonding a stake. There is no way to bond a stake for someone else. Comparable to direct democracy where everybody need to vote on their own.


### Delegated Proof Of Stake (DPoS)

This variant adds the functionality that accounts can vote for delegates/representative accounts. Therefore, accounts with small stakes can participate by accumulating enough stakes to bond. There is also a fixed number of Validators which are elected for a certain period of time. The following list highlights the differences to BPos:

**staking/election process**
- Accounts bond their stake to vote on an account which they trust and want it to become a Validator (you can also call it Representative/Delegate)
- There is a fixed amount of Validators/Delegates/Representative
- The Accounts with the most accumulated votes become Validators
  
**Validator picking algorithm**
- Out of the set of Validators which where voted by the accounts, one of the Validators is picked randomly (often uniformly)
- A subset of Validators is picked randomly (often uniformly) to verify the block 

**Slashing process** 
- The accounts that bonded the stake lose their stake
- DPOS punishes objective and subjective bad behavior by voting people out

**Rewarding process**
- The Validator gets the reward (Blockreward or/and fees)
- The Validator usually gives back some reward to the accounts which staked for him

**Voting rights**
- Validators vote on protocol amendments etc. - not the accounts that staked


Comparable to representative democracy

<!-- Implementation:

- EOS - 21 Validators (100 Standby Validators), 
- LISK
- TRON
- BitShares -->

### Liquid Proof-of-Stake (LPoS) ?=! Leased Proof of Stake (LPoS)

LPoS is a mix out of BPoS and DPoS. It puts not restriction on the validator set. Any account can be a validator based on the bonded stake or delegated bonded stake.

**staking/election process**
- Every account can become validator
- Bonding stakes for an other account is also possible (liquid/leasing aspect)
- No fixed number of validators
- Tokens are not locked (taken into custody) i.e. they don’t lose the tokens from their wallets
  
**Voting rights**
- LPoS also offer voting rights, except that as a token holder you get to vote directly in the protocol amendments, and not only in who secures the network like in DPoS.

<!-- Implementation

- Tezos 
  - Also has endorsers (witnesses) for the created blocks who checked it
  - Delegates and Bond pools possible -->

### Hybrid/Mixed Proof-of-Stake (HPoS)

Hybrid systems combine different approaches. E.g. Caspar combines PoS and PoW. Another example would be the combination of Masternodes + POS mining or Delegated Byzantine Fault Tolerance like NEO implements it. The variations are just too many to cover all of them. Depending on what PoS parts they use, the system might be vulnerable to one of the attacks discussed in the next section.

<!-- Exampe Projects:

- Ethereum Caspar -->
<!-- Casper only punishes objective bad behavior by slashing bonds. -->
<!-- Casper relies on proof-of-work to determine when and who and when gets to propose and bonded-stake-weight to determine who the validators are.  -->
<!-- Protocols like Casper attempt to minimize the overhead by relying on proof-of-work for short-term consensus and only reaching finality over every 100th block (checkpoint). This means Casper-based chains reach finality every 20 to 30 minutes. -->
<!-- - ?EOSIO -->

<!-- ### Proof-of-Stake Voting (PoSV) -->
<!-- ### Masternode staking (?Proof of Service)
Masternodes are incapable of creating new blocks, but are capable of verifying transactions. Reason for it to still be categorised as a consensus algorithm. Due to its focus on securing the network, it has the power to reject blocks that might cause harm to the network.
PIVX type consensus structures with POS minging + Masternodes. -->
<!-- ### Delegated Byzantine Fault Tolerance with ONG dividends
### Delegated Byzantine Fault Tolerance with GAS dividends -->

## Specific Attacks

### The 51% Attack Equivalent
Similar to 51% attacks in PoW networks a user can control more than 50% of the network's stake. This is assumed to be highly unlikely for multiple reasons. First, to get this many tokens, the price will peak and make it pretty expensive. Secondly, attacking a network while owning more than half of it seems unreasonable. Still, it might be worth the risk for some competitors. But keep in mind, that it would be relatively easy to reset the network and ban/seize the account/tokens.


*Mitigation*

It is hart to prevent this attack but the attack is hard to perform and easy to later undo.

Sources:

> [How Proof of Stake Renders a 51% Attack Unlikely and Unappealing](https://blog.qtum.org/how-proof-of-stake-renders-a-51-attack-unlikely-and-unappealing-ddebdc91a569)


### Nothing at Stake

To understand this attack I need to repeat what was mentioned in the introduction. The ''stake'' in Proof-of-Stake **does not** refer to the tokens that a Validator puts at risk (stakes) which can later be taken away when misbehavior is detected. The first blockchain projects implementing PoS did not require a security deposit. In early versions of PoS, owning tokens was sufficient to become a Validator. **Holding tokens in a wallet was the stake.** Hence, if validators attacked the network, nothing happened to their ''staked'' coins.

Let us assume the network forked for some reason. As blocks can easily created and Validators are rewarded for contributing a block, it makes sense to contribute a block to every fork. Therefore, making sure to receive the block reward on the winning longest chain. But if every validator does this the network could run into a consensus failure. There will simply be no longest chain for a long time as they progress with the same speed. 


> The ''Nothing at Stake'' problem
>
> |  |  |
> | ------- | ------- |
> | The Nothing at Stake problem  | Stake does not add to the convergence of the system, since the same stake can be applied to multiple competing chains, which is a risk free way of stakers increasing their rewards. In contrast, in PoW based systems, energy is a real world finite resource and therefore the ''same'' work cannot be applied to multiple competing chains. |
> | Defense 1 | The issue can be avoided or mitigated against. The protocol can be adjusted such that if a staker uses the same stake on multiple chains, a third party can submit a proof of this to either chain, resulting in a punishment, such as the confiscation of the stake (slashing conditions). Alternatively instead of a punishment, the cheater could lose potential rewards or be excluded from the staker pool. |
> | Response from PoS sceptic | The above defence is inappropriate and punishes what may be legitimate or necessary behavior. For example if a staker receives a block first, while the majority receives an alternative block first, it may be legitimate for that staker to change their mind and switch to follow the majority. Indeed the process of changing your mind and switching to the majority to ensure the network converges is the point of the consensus system. If this behavior is punished, how does the system converge?<br><br>Either the economic value of the punishment is higher than the rewards for switching to follow the majority, or it isn’t. Therefore the nothing at stake problem means PoS systems can never make a contribution to system convergence and the idea is therefore fundamentally flawed. <br><br> [!img](PoSsceptic.png) |
> |Defence 2 | The apparent dilemma above can potentially be  resolved in various ways. For instance:<br><br>Earlier proposals from Casper used multiple rounds of staking. Changing one’s mind in the early rounds can be legitimate and perhaps the punishment is small, while in later rounds the punishment for using the same stake in multiple competing chains increases, such that eventually users have a high degree of assurance over the finality of the system.<br>The most recent iteration of Casper aims to allow validators to change their minds, but only in ''legitimate'' scenarios and not when its ''illegitimate''. |
> | Response from PoS sceptic | By adding multiple rounds or criteria in which validators can change their minds one is increasing the complexity of the system. This is merely adding layers of obfuscation to conceal the inherent weaknesses illustrated by the nothing at stake problem, without solving the fundamental issue.|
> |Defence 3 | No system is perfect, indeed it’s mathematically impossible to construct a perfect system and therefore the nothing at stake problem is not solved, however the measures identified above mitigate the problem, such that these theoretical issues are unlikely to apply in the real world.|
From [Complete guide to Proof of Stake – Ethereum’s latest proposal & Vitalik Buterin interview](https://blog.bitmex.com/complete-guide-to-proof-of-stake-ethereums-latest-proposal-vitalik-buterin-interview/) 


*Mitigation*

The Validators' bond their stake which then is seized or burned if they vote on multiple chains.
Casper implements a design strategy to counteract this problem called Slasher.


Sources 

> [Casper (proof of stake)](https://golden.com/wiki/Casper_(proof_of_stake))
>
> [PoTS—A Secure Proof of TEE-Stake for Permissionless Blockchains](https://eprint.iacr.org/2018/1135.pdf)
>
> [Understanding Proof of Stake: The Nothing at Stake Theory](https://medium.com/coinmonks/understanding-proof-of-stake-the-nothing-at-stake-theory-1f0d71bc027)
>
> [Complete guide to Proof of Stake – Ethereum’s latest proposal & Vitalik Buterin interview](https://blog.bitmex.com/complete-guide-to-proof-of-stake-ethereums-latest-proposal-vitalik-buterin-interview/) 

### Fake Stake Attacks 

I kept the original name from the article. But the name seems misleading. These attacks are Denial of service attacks which fill up the victim's RAM and/or disk space.

Due to ineffective data validation (especially implementations which use Bitcoins implementation as base such as PoSv3 - [Proof-of-Stake version 3](http://earlz.net/view/2017/07/27/1904/the-missing-explanation-of-proof-of-stake-version)) when receiving blocks over the network, this attack enables an attacker to fill a node's RAM and/or disk. The attack can be carried out without much stake (in some cases even none at all). These kind of attack can, according to the underlying article, could be carried out on nearly all currencies based on the UTXO and longest chain Proof-of-Stake model. For affected chains check the list towards the end of the referenced article.

**RAM Attack**

> In detail affected chains do not check coinstake transaction before storing a block to RAM or disk. The vulnerabilities are caused by adopting Bitcoin's ''header first'' principle. Bitcoin propagates blocks in two messages: Block and Header. First, Bitcoin checks the header and if it is a longest (or longer) chain. In PoS chains the coinstake transaction is usually only present in the Block but not the Header. Therefore, the Header is insufficient to perform a PoS check. The node stores the Header directly to an in-memory data structure (mapBlockIndex). As a result, any network attacker, even with no stake whatsoever, can fill up a victim node’s RAM.

**Disk Attack**

> The second variation of this attack can be carried out against the same codebases, although it works in a slightly different manner and targets a different resource, the victim’s disk rather than RAM. Arguably an attack involving disk is more harmful to the victim: If RAM is filled up and the node crashes, it can simply be restarted. However, if the disk is full, manual intervention would be required (for example, to run an external script to clean up stale blocks from disk).

> Different preliminary checks are performed when receiving a block rather than receiving a header. Ideally, since the block does contain the coinstake transaction, the node software should check the coinstake transaction before committing the block to disk. However, as mentioned, if the block is on a fork, there is no easy way for a node to access the UTXO spent by the coinstake transaction. Perhaps for this reason, these codebases do not validate the coinstake transaction.

> Exploiting either of these vulnerabilities can be carried out without having any stake in the affected cryptocurrency at all. The RAM version of the attack is particularly trivial, but for technical reasons, the disk version of the attack requires slightly more care (though still no stake is required). The details are explained in a short paper to be presented at [Financial Cryptography 2019](https://fc19.ifca.ai/preproceedings/180-preproceedings.pdf).


*Mitigation*

Checkpoints,  enforce  that any fork generated prior to a sufficiently deep block (i.e., prior to a checkpoint) is discarded.

Sources:

> [''Fake Stake'' attacks on chain-based Proof-of-Stake cryptocurrencies](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806)
> 
> [Short Paper: I Can’t Believe It’s Not Stake!Resource Exhaustion Attacks on PoS](https://fc19.ifca.ai/preproceedings/180-preproceedings.pdf)


### Stake Amplification or Spent Stake Attack

This attack is also possible if the data validation is ineffective when receiving blocks over the network. But instead of filling up RAM or DISK the attacker fakes a high stake without really having it. This again affects primarily PoSv3 implementations.

> The code checks if the coin exists but not if it is unspent. Even if we’re validating a block on a fork of the main chain, the coinstake transaction is validated against the TxDB for the main chain itself. 

> To carry out a ''spent stake attack'', use an output that is seen by the node but is already spent. We would need to mine a valid block that passes the difficulty target, which in turn would require a large amount of stake. As it turns out, however, we can abuse the incomplete validation to generate an arbitrary amount of apparent stake using a technique which the author of the article and paper call ''stake amplification''.


*Mitigations*

- Monitoring malicious behavior and disconnect/ban the node. Drawback: Could ban honest nodes which undergo a reorg
- Partial validation up to a fixed length. Drawback: Chains can split/fork unintended.

Sources:

[''Fake Stake'' attacks on chain-based Proof-of-Stake cryptocurrencies](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806)

[Short Paper: I Can’t Believe It’s Not Stake!Resource Exhaustion Attacks on PoS](https://fc19.ifca.ai/preproceedings/180-preproceedings.pdf)

### Validator selection attacks

These attacks target the Validator selection process. The attacker tries to influence (increase) the chance of being selected as the Validator.

#### Adaptive key selection attacks

> Since proof-of-stake systems admit open participation, any-one can buy up stake in the system and participate.  This also means anyone can (possibly maliciously) choose their public-keys through which they participate in the consensus.  A possible attack, therefore, is to adaptively choose public-keys, after gathering partial information about the  randomness  seed  used  for  block-proposer  selection,  such  that  corrupt  nodes  are elected more often as block-proposer than their fair chance.

Source: 

[Snow White: Robustly Reconfigurable Consensus and Applicationsto Provably Secure Proof of Stake](https://eprint.iacr.org/2016/919.pdf)

#### Stake Grinding

> Finally, in stake grinding attacks, adversaries use their computational resources to increase their probabilities of being elected as leaders/miners of the upcoming blocks. - [see](https://eprint.iacr.org/2018/1135.pdf) -

> In a pure PoS system, stakers also need to produce blocks. These systems have often worked by selecting a sequence of authorised block producers randomly from a pool, where the probability is proportional to the stake. The issue here is a source of randomness is required inside the consensus system. If the blocks themselves are used for generating the entropy, stakers could try to manipulate the content in blocks in order to allocate themselves future blocks. Stakers may then need more and more computing power to try more and more alternative blocks, until they are allocated a future block. This then essentially results in a PoW system. 
To combat stake grinding attacks, a number of  PoS  proposals  utilize  a  deterministic  algorithm  to  elect block leaders. This, however, gives rise to another important problem:  the  leader  of  each  valid  block  is  predictable  in the  network,  thus  making  it  vulnerable  to  planned  denial-of-service attack strategies. Moreover, an adversary can still perform stake grinding by skipping an opportunity to create a block if they are able to increase their advantage over future blocks. - [see](https://blog.bitmex.com/complete-guide-to-proof-of-stake-ethereums-latest-proposal-vitalik-buterin-interview/) -


*Mitgitation (validator selection attacks)*

Proper source of randomness.

Sources:

[Complete guide to Proof of Stake – Ethereum’s latest proposal & Vitalik Buterin interview](https://blog.bitmex.com/complete-guide-to-proof-of-stake-ethereums-latest-proposal-vitalik-buterin-interview/)

[PoTS—A Secure Proof of TEE-Stake for Permissionless Blockchains](https://eprint.iacr.org/2018/1135.pdf)


### Long-Range Attacks 

These attacks are special non-PoW chains (especially PoS). These kind of attacks are possible because there is no work (hash) which needs to be calculated when ''rewriting history''. Therefore, they are also referred as history attacks. Once the newly crafted branch becomes longer than the main chain, it will overtake it. 

#### Simple Long-Range Attack
This attack assumes that there are no proper timestamp checks implemented. An attack scenario could be that the attacker starts at the genisis block mining blocks correctly. The attack will be slower as the main chain. But by forging the time stamps the attacker just beams the blockchain into the future. The main chain will just see a longer chain and accept it. In implementations where nodes do not take into consideration timestamps, both branches will be valid and nodes won’t be able to spot the trick trick.

[!img](https://miro.medium.com/max/700/1*iQSm8i2CL-S5IJUiyAlSgw.png)

The information was taken an partially quoted from [Rewriting History: A Brief Introduction to Long Range Attacks](https://blog.positive.com/rewriting-history-a-brief-introduction-to-long-range-attacks-54e473acdba9)

#### Classic Long-Range Atack
> This can be achieved when, e.g., the attacker acquires the private keys of old accounts which no longer have any stake at the moment, but that have accrued majority stake at previous block height h; the attacker can  then  construct  a  fork  starting  from  block h leveraging these accounts. 

> Due to the large amount of rewards given to the attacker, one could then generate a higher stake chain than the existing chain and a large multi year chain re-organisation could be performed. 

*Mitigation: (3)*

Sources:

[PoTS—A Secure Proof of TEE-Stake for Permissionless Blockchains](https://eprint.iacr.org/2018/1135.pdf)

[Complete guide to Proof of Stake – Ethereum’s latest proposal & Vitalik Buterin interview](https://blog.bitmex.com/complete-guide-to-proof-of-stake-ethereums-latest-proposal-vitalik-buterin-interview/)


### Posterior Corruption 
Nodes currently syncing (IBD - Initial Block Download) or refreshing are mainly vulnerable to this attack. An attacker who mined an alternative chain in secret can send this to a node and cause e.g. a chain split. If the attacker uses Eclipse attacks which could also be leveraged by one of the RAM/disk attacks, the attacker can trick honest nodes into a controlled malicious chain. It is hard to protect against these kinds of attacks. Newly joining nodes or nodes which where offline for a long time need to trust some other node(s).

*Mitigation: (2)*

Sources:

[PoTS—A Secure Proof of TEE-Stake for Permissionless Blockchains](https://eprint.iacr.org/2018/1135.pdf)

[''Fake Stake'' attacks on chain-based Proof-of-Stake cryptocurrencies](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806)

[Stake-Bleeding Attackson Proof-of-Stake Blockchains](https://eprint.iacr.org/2018/248.pdf)

[Rewriting History: A Brief Introduction to Long Range Attacks](https://blog.positive.com/rewriting-history-a-brief-introduction-to-long-range-attacks-54e473acdba9)
    
#### Stake-Bleeding Attack

To perfrom a Stake-Bleeding attack, an attacker sets up a private chain where the attacker generates blocks when possible and skips all other validators. The attacker on the other hand does not contribute to the main chain. At the beginning the private chain will advance very slow because each time the algorithm does not choose the attacker as validator no block is generated. But the validator is the only one on the private chain getting rewards. Hence, the relative stake increases all the time. At some point the attackers relative stake is big enough to progress faster in the private chain than in the main chain. As soon as more blocks are produced in the private chain than in the main chain, the attacker  redistributes the stake to other validators and then goes on to publish her branch.

*Mitigations: 1,2*

Sources:

[''Fake Stake'' attacks on chain-based Proof-of-Stake cryptocurrencies](https://medium.com/@dsl_uiuc/fake-stake-attacks-on-chain-based-proof-of-stake-cryptocurrencies-b8b05723f806)

[Stake-Bleeding Attackson Proof-of-Stake Blockchains](https://eprint.iacr.org/2018/248.pdf)


**Mitigation (Long-Range attacks)**

1. Longest Chain Rule
2. Moving Checkpoints
3. Key-Evolving Cryptography
4. Context-Aware Transactions
5. Plenitude Rule/strict chain density statistics

_____

## Final remarks
For simplicity parts of the text are quoted. The source should always be linked near the quote. In case some authors want a better highlighting of their text parts, please get in touch with me and file an issue in the github repository or create a merge request.


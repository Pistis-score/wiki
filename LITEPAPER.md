<p align="center">
<a href="https://github.com/PlushFamily/plush-protocol-contracts" target="blank"><img src="https://user-images.githubusercontent.com/9155259/199185204-06e0d120-5cbf-46b9-a817-b05634170003.svg" width="120" alt="Pistis logo" /></a>
</p>

# <p align="center"> Pistis: a comprehensive financial reputation

<p align="center">Kirill Demishev, Dmitrii Mingalev

<p align="center">paper@pistis.network

<p align="center">https://pistis.network

<p align="center">ver. 1.05

## Abstract

DeFi is still in its infancy right now, with little to no overlap with the traditional financial sector. Two worlds - DeFi and TradFi exist separately from each other, which hinders the development of the quantity and quality of financial services available to DeFi users. The abundance of self-contained blockchains and sidechains and the anonymity of their users exacerbate the situation. We believe that the ability to issue and take under-collateralized loans through DeFi protocols will advance the development of the domain and make DeFi useful to the average person.


## 1. Introduction

Loans in DeFi are currently useless to most people since to borrow some tokens you usually need to have other tokens that cost even more than the target funds. It’s necessary to secure the loan. The over-collateralization of loans keeps the number of DeFi users that ever interacted with DeFi equal to 2.4% of all existing wallets (data for the Ethereum network). 28 Billion dollars currently locked in DeFi protocols, which is just 0.17% of total consumer debt in the USA ($16.5 trillion) as of September 2022. Such a huge gap in numbers could be significantly decreased by offering DeFi users under-collateralized loans. There is something that customers can use as collateral instead or together with tokens - their reputation. 


## 2. Reputation

The reputation of any person is always a composable entity. The financial reputation of a DeFi user could be composed of three main parts: DeFi reputation score, TradFi reputation score, and Personal reputation score.


<p align="center">
  <img src="https://github.com/Pistis-score/wiki/blob/main/images/Pistis_reputation_components.jpg">
</p>


DeFi score is a number that reflects all operations of the user with all DeFi protocols, from all user’s addresses in all blockchains. It also should take into account historical data of all addresses linked to the user's reputation score.

TradFi score is the score from some national rating agency or financial institute. Historical data on users' accounts could also be considered.

A personal score is a composition of digital and non-digital data related to the user. Digital data consists of on-chain data (POAPs, certificates, other reputation tokens) and off-chain data (Facebook, Twitter, Instagram accounts, and more), and non-digital data, eg. paper educational certificates, professional and other types of awards, and so on.

To avoid manipulations data sources added to the reputation can not be unlinked in the future for any reason. Also, one source can be connected to one reputation token only.


## 3. Pistis protocol

Pistis protocol is a set of smart contracts with the following functionality: 



1. Issue and reissue Pistis soulbound dNFT
2. Lock and burn Pistis Token
3. Interact with data storages (Ceramic and Arweave)

Integration with Arweave allows for permanently storing the list of off-chain data sources of each token while Ceramic integration helps to store historical data of tokens.

Below is a scheme of the core components that participate in Pistis score composition, including Pistis protocol:

<p align="center">
  <img src="https://github.com/Pistis-score/wiki/blob/main/images/Pistis_score_components.jpg">
</p>


### 3.1. Pistis Token

Pistis Token is the cornerstone of the Pistis Protocol. It is a soulbound dynamic NFT that has several purposes:



1. Store user’s overall reputation along with the date it was calculated
2. Store user’s DeFi reputation along with the date it was calculated
3. Store user’s TradFi reputation along with the date it was calculated
4. Store user’s Personal reputation along with the date it was calculated
5. Manage access to the data linked to the Pistis Token
6. Governance of the protocol

Pistis is a transferable token. The incentive not to share it is the possibility that other people ruin the user's reputation. This feature also widens the number of Pistis Token use cases. Communities, DAOs, companies, and other organizations could create this token for themselves in the future and grow their reputation to get access to under-collateralized loans in DeFi.


## 4. DAO

Pistis DAO is the entity that governs Pistis protocol. Initially, the governance will be linked to Pistis Token and PSTS ERC-20 tokens (see section 9 for details) where 

_Voting Power = 1 Pistis Token * (amount of PSTS)_

Another DAO responsibility is to manage the vault growing and developing the Community and Pistis product.


## 5. Pistis Nodes

Pistis Nodes have a simple and important purpose - calculate, recalculate and place the scores in the Token as metadata. The process of calculation is as follows:



1. The master node assigns the calculation tasks to random N (N to be defined later) nodes.
2. Selected nodes retrieve the token data from Ceramic, Arweave, and Chainlink.
3. Selected nodes calculate the scores and send the final results to the master node.
4. The master node calculates the median result.
5. The master node runs a smart contract that changes the scores on dNFT and writes the updated data to Ceramic.
6. Selected nodes that provided the master node with correct values (error &lt;= 5%) get rewarded.
7. Those selected nodes that provided the master node with incorrect values are penalized
8. In case some selected node is unavailable it gets blocked for a while and then penalized.

A Proof-of-Stake mechanism will be implemented for nodes which means all of them will stake some PSTS tokens (see section 9 for details).

In the first stages of the project, the nodes will be run by the Pistis foundation. Later on, any user could run their nodes by setting up equipment that meets minimal requirements and staking some funds. The reward will be a part of the service fee paid by the user or the organization on behalf of the user.

To decrease the fee for recalculation jobs some DeFi protocols could ask for the recalculation of blockchain-based data only. Recalculation before the loan issuance is necessary to mitigate the risk the client made a loan in many protocols simultaneously.


## 6. Loan issuance general flow
  
The flow above is an example of how the DeFi protocol could interact with the Pistis protocol. In case the protocol works on another blockchain and doesn’t persist on Ethereum, Chainlink services will be added to the process as a bridge between blockchains.
  
  <p align="center">
  <img src="https://github.com/Pistis-score/wiki/blob/main/images/Pistis_loan_flow.jpg" width="600">
</p>


## 7. Loan guarantee

We understand that the most difficult part for users is to start using the protocol since they don’t have much historical data. To address this issue, simplify and speed-up engagement and make the protocol available for more users the loan guarantee mechanism was added to Pistis.

Users can temporarily increase their score by asking another user with a higher score to be their guarantee for a certain loan. The guarantee will stake some funds and their reputation to vouch for a user. In case the user fulfills their obligations the guarantee receives his stake back with a reward. Otherwise, the staked amount will be lost and the reputation will suffer significantly.

Moreover, to start a new DAO and boost its growth, founders will be able to stake their Pistis Tokens together to be able to get undercollateralized loans for their DAO business development. 


## 8. Social mechanics

To create a working protocol we are confident that Pistis Token should belong to the user during their whole life. But life is long and there are two issues that Pistis needs to address:



1. Pistis Token is lost or stolen.
2. The user relocated to the metaverse forever and doesn’t need the token anymore but unable to burn it.

For lost and stolen tokens Pistis will use the social recovery option, where the user's family and friends could recover the token for a selected address and burn the previously minted token. Unfortunately, currently, there is no way to recover a Pistis score on the token in case it was damaged by the violator unless the damage is compensated. The plush family protocol will be used to build a decentralized social graph of the user.

In case of permanent relocation to the Metaverse and inability to use Pistis reputation there (we believe that someday even permanent relocation of the person to Metaverse will not stop them operating in their best interests, and interests of their loved ones) the social burning of the token will be available where all participants who claimed and proofed the relocation will be rewarded.


## 9. Tokenomics

The PSTS token is an ERC-20 token issued to keep the protocol working. It’s used as:



1. Calculation fee
2. Staking reward
3. Node running reward
4. Governance voting power along with Pistis Token
5. Protocol development incentive

Below is the scheme for how the loan request fee will be distributed:

<p align="center">
  <img src="https://github.com/Pistis-score/wiki/blob/main/images/Pistis_loan_request_fee_distribution.jpg" width="600">
</p>

The fee for recalculation that includes adding a new source of data to Pistis Token will be different since Arweave will be added to the scheme.

Assuming to complete the user's operation Pistis protocol needs to pay N PSTS to Ceramic, Chainlink, and Arweave. Pistis nodes will get 0.3*N PSTS and Pistis DAO will get 0.13*N PSTS so the total fee would be equal to 1.43*N PSTS. This formula is flexible and could be edited by the DAO in a later stage when Pistis is decentralized enough.

PSTS token is non-mintable with an initial issue of 1 Billion PSTS. Below is the distribution of PSTS tokens. Lock and vesting terms could be discovered in [the tokenomics paper](https://docs.google.com/spreadsheets/d/1hAkPjArqPrFdOE9XcyTWWPfmJkQwzYRhfyj0wSZjjlo/edit?usp=sharing).


## 10. Conclusion

We have proposed a reputation system that will add real value to DeFi protocols and attract new users to Web 3 and DeFi particularly. We designed Pistis to unite currently available Web 3 tools around the user’s needs in under-collateralized loans. Technologies of Chainlink, Ceramic, Arweave, and Plush along with capabilities provided by Ethereum allow us to build a reputation that is:



1. Decentralized
2. Owned by the user
3. Could be proofed preserving user’s privacy
4. Linked to the soulbound dNFT and thus updatable
5. Based on DeFi, TradFi, and Personal data
6. Considering multiple addresses on different blockchains interacted with different protocols
7. Designed to be cultivated through the whole life of its owner and beyond

The protocol will be governed by the DAO that has several stages of growth before approaching full decentralization in the future.

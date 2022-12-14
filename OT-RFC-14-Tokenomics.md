# **OTC-RFC-14: OriginTrail Club on TRAC Tokenomics** 

Authors: OriginTrail Club

Contributors: BRX, Dmitry, LuKu, Milian, hottogo, K’walla, Calvin, Famous Amos 

Date: Oct 14, 2022

Note: We thank BRX/otnoderunner for creating and gathering information used for this representative response.

## Introduction

OriginTrail Club is actively gathering all community feedback concerning all RFCs by the core developer team of OriginTrail, assembling it together with our own point of view, and providing the team with an in-depth analysis of the subject matter. 

Moving forward, we will thrive to represent the core community’s interest and allow every community member to be heard, including those who do not wish to open a GitHub account to comment. 

## Points of interest

1. 50k TRAC minimum required per full node
2. New stake slashing mechanism replacing litigations
3. Current default stake slashing values: 5% of TRAC locked for 2 years
4. Highest stake winning the bid
5. Retiring a node
6. Data replication on all R1
7. Node backups
8. Epochs lengths
9. Lambda

## Feedback

### 1. **50k TRAC minimum required per full node**

The general consensus seems to be a positive one regarding the increased amount to run a node. Given the current market conditions, this is equivalent to 8,500$ USD as a minimum amount, which could be a hurdle for smaller TRAC holders. Smaller TRAC holders might also not attract enough delegators to run a node. In addition, the concern with this higher amount would be whether the number of nodes would be enough to meet sufficient decentralization across all neighborhoods (i.e. max amount of nodes would be probably around 5-6k) and whether that number can change based on a higher token price in the future (i.e. at 6$ TRAC token price, 300,000$ USD would be required to run a full node). Is there a mechanism for this 50k tokens amount to change? Will it be an automatic mechanism or manual? Will we know the parameters?



### 2. **New stake slashing mechanism replacing litigations**

This is a welcome change as litigations prior to v5 would punish the node runner harder by completely removing the node runner’s stake. Slashing, or locking up a certain amount of tokens for a fixed duration, rendering the tokens useless in the meantime, serves as a good deterrent to node runners and promotes good behavior. In the community, it is an unanimous agreement that slashing instead of litigation is an improvement to the ecosystem. 

The disagreement lies within the stake slashing default values. 


### 3. **Current default stake slashing values: 5% of TRAC locked for 2 years**

These values seem to be quite high without knowing the specifics. Node runners need to know a clearly defined definition of stake slashing. In other words, how long can a node remain offline without triggering a slash ? How does a node know, despite being online, that it is functional and detected by the network ? Is slashing multiplicative or additive ? Is slashing possible by several assets I hold, several times a day, or is it capped to one slashing per 24 hours ? Will the slashed amount be affecting delegators as well or just the full node runner ?

A poorly designed slashing method could break the entire ecosystem. The benefits of running a node must always outweigh the risk of locking up funds. In real life, no centralized system is up 100% of the time. The stake slashing must have more metrics to distinguish bad actors from accidental outages. 

In the event of a datacenter fire or any events causing a complete loss of data, how does a full node recover from that after rebooting using the same credentials, but without any datasets ? If a backup is available but is 1 week old, how likely is slashing if 1 week of assets have been lost ? These are all questions that need to be answered for node runners to better plan their node maintenance. 

There is an agreement in the community that both metrics (5% of TRAC locked for 2 years) seem a bit high, without knowing more details. For example, failing an epochs check for an assertion worth 0.01 TRAC and risking a lock for 2 years of 2500 TRAC (for a 50k full node) seems a bit high of a punishment, if that is how slashing works. The stake slashing must be relative to the assertion amount and duration and be a lot more reasonable. 2 years in crypto time is a lot and way too big of a deterrent for node runners - a number such as 6 months should be considered instead. 5% of available TRAC for a 50k TRAC full node is 2500 TRAC which seems a bit high if one low paying service can trigger a slash. 

What happens to your node if it has the minimum stake of 50k tokens and gets slashed by 5%? Is it disqualified from bidding for service agreements? Is the slashing pro-rata to the delegated trac or is it pro-rata to how the rewards are paid out? i.e. if the Node runner owns 50% of the stake but gets 75% of the reward, and the delegators own 50% of the stake but gets 25% of the reward (example numbers), does the slashing hit the node runner and delegator equally or do they split it 75:25 in line with what their rewards would have been?

A hold in the stake slashing mechanism should also be considered at the start of V6 mainnet to make sure the slashing mechanism operates as designed in production.


### 4. **Highest stake winning the bid**

This is a hot topic among the node runner community. This black-or-white system might push node runners to always one up their peers. For instance, node runner X with 50,000 TRAC will add 1 TRAC to beat node runner Y with 50,000 TRAC in the same neighborhood to win every single assertion when bidding against each other. The difference in their staked amount does not necessarily represent their quality of service and slashing, if it happens, would almost represent an almost identical amount, making the risk similar but reward skewed towards node runner X. If this type of behavior continues, we will find ourselves with a huge amount of mega nodes and hurting decentralization in the end. 

A great alternative would be to erase the all-or-nothing system and replace it with a probabilistic system. 

Here is an example:

The total R1 (set of nodes bidding on the assertion) has a total amount of 500,000 TRAC. Each node has a fixed probability of becoming R0 (winning the assertion). 

R1:

Node A = 50,000 TRAC = 50/500 = 10%

Node B = 50,000 TRAC = 50/500 = 10%

Node C = 100,000 TRAC = 100/500 = 20%

Node D = 150,000 TRAC = 150/500 = 30%

Node E = 150,000 TRAC = 150/500 = 30%

The dices are thrown and the R0=3 group becomes:
Node B,C,E

An alternative method would have the dice thrown 3 times (if R0=3) instead of once, with each throw removing the previous winner.

Another issue with the above example is how each node is pitted against a randomly assigned neighborhood. Node E may have 150,000 TRAC with a 30% chance of winning the service, however if randomly assigned to another neighborhood with much bigger nodes, that chance can go down to 10% such as Node A (example number). In other words, a node can have either 30% or 10% chance of winning a service based on a completely random factor. The win percentage could be based on all nodes in all neighborhoods to make it fair. The neighborhood should be used to determine “opportunistic” assertion replications only, not win percentage. 


### 5. **Retiring a node** 

More details are needed to understand the process of retiring a node without triggering a slash. There needs to be a way to remove our commitment in a reasonable amount of time and responsibly. 

In order to balance supply and demand, both supply and demand must be flexible. As seen in versions prior to V6, node numbers did not go down despite lower demand, simply due to the fact that node runners were obliged to finish their jobs or risk being litigated, so they might as well keep accepting new jobs. This caused a race to the bottom with nodes accepting jobs for a negative return which shouldn't happen on this next iteration of the DKG. 

Now, with the introduction of epochs checkpoints where node runners get rewarded after proving that they did their job, it is a perfect opportunity to allow the full node to retire responsibly and allowing R1 to bid on the retiring node’s ongoing services. That way, it will not cause bad behavior (since the node still risks getting slashed if not able to provide proof of service), while promoting responsible continuation of the service through another bidding within the neighborhood and allowing the node to retire safely. This, in turn, will allow the supply of nodes to go down in a flexible manner to match demand if node returns are low. 


### 6. **Assertions replication on all R1**

It would be ideal if we get some clarity on what is the process of node assignments to neighborhoods in both initial node inception, and later when a new neighborhood is created. How would the system decide whether more nodes are required in a certain neighborhood ? What if the neighborhood depreciates ? And how would the DKG ensure all nodes are having fair access to opportunities to host data uploaded on the DKG, so a full node does not end up in some forsaken N that gets no new assertions ?

Full node runners must also have the option to choose whether they want to hold “opportunistic” assertion replications within their neighborhood. Currently, all of N are forced to replicate the same assertions while only a select few, R0, are being rewarded. The full node runner must be offered the choice to host assertions opportunistically in order to be able to perform “self-healing” of replicas or not. 

Another point of interest on this neighborhood system is how node runners could want to "re-roll" to close out their node and make a new one to try and get into a more favorable neighborhood. Will this occur often going forward? Will nodes want to move out when a bigger node moves in and impacts their returns? Will we be constantly re-making our nodes with new node IDs chasing the weakest neighborhoods? Do we need a promotion system to counteract this so a high performing node gets promoted into tougher neighborhoods like the premiere league?


### 7. **Node backups**

Node backups also need to be discussed and how quickly we need to restore a node in case of an outage. The team must provide more guidance on the best ways possible to backup in order to prevent slashing. Some community members are discussing the possibility of backing up the node on the DKG itself.


### 8. **Epochs lengths**

Epochs, or checkpoints during service, should be lengthy enough to allow node runners some lee-way to fix their node in case of an outage. We need more information about the epochs' length, and whether they are fixed for all assertions or not.


### 9. **Lambda**

Lambda has been a hot issue plaguing v5 node runners and hasn't been mentioned once in this RFC. Can we have a word about how lambda has been adapted to V6 ? There was also a RFC-06 discussing automated lambda. Is that approach still relevant and would it be included sometime after v6 is released? Is it possible to not allow a negative lambda or a lambda of 0?

## Conclusion

Despite all the previous points, the overall community feedback towards OT-RFC-14 is a positive one. We understand this is an introductory RFC to the new tokenomics of V6 and are not given more technical details, however most of the aforementioned points would still hold true given similar circumstances, and we hope to continue working alongside the community and the core team to flesh out the best iteration of V6. 

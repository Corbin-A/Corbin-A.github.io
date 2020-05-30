---
layout: post
title: Could a Large Government Render Bitcoin Obsolete?
---
[]: # (Written on 2017-09-27)
![](/images/govt-bitcoin/bitcoin-img.jpg)

There is a lot of general skepticism surrounding bitcoin and blockchain technology, with endless comparisons to Tulip mania and other such irrational hyper-inflation of prices followed by irrecoverable crashes. When people talk of long-term viability, they talk about governments not being able to control capital flows, and their belief that this will lead to crippling restrictions or illegality.  This fear is overblown, and is not what I’m going to discuss today–rather, there is a much more fundamental way that any government could destroy Bitcoin or any other Proof of Work cryptocurrency.

### Bitcoin Background
For the uninitiated, Bitcoin is a digital currency, but what makes it interesting is the underlying technology–the ever so buzz-wordy blockchain. Long story short, this is a public ledger that anyone can download and have access to which displays a series of transactions between accounts. I know, sounds soooooo interesting doesn’t it? But what makes it novel is that these transactions can be trusted without the use of a third party. No need to trust a bank, or a credit card processor, or a government. It is governed by the laws of mathematics.

That’s extremely powerful. Ask Venezuela or Greece. Ask anyone with more than $250,000 in a bank that has gone bankrupt. There are serious issues with having to trust third parties with our capital. I would of course extend this to many other parts of our lives other than capital, and tell the tale of how Ethereum circumvents it, but it is ultimately necessary for this discussion.

### Let's get slightly more technical
But we need to dig a bit deeper than this surface understanding to follow the argument presented here. As Bitcoin transactions occur, they are placed in a block. When this block has “filled up”, it needs to be pushed to the chain of previous blocks. Anyways, how do we ensure that all these blocks are correct? This is where miners come into play.

#### Miners
Bitcoin miners are special-purpose computers that attempt to solve a very complex equation. The only way to solve it currently is via brute force, meaning that potentially every single possible combination must be tried before “cracking” the equation. This is called Proof of Work. When a miner has solved this puzzle, it is pushed to the rest of the network, which validates that every transaction was valid (i.e. that each sending account had the amount necessary that is it trying to send). If so, this block is appended to the chain. Specifically, the longest chain in existence, as this is considered the chain with the most support.

#### Longest Chain
You may be asking what this “longest chain” means. Bear in mind that the other miners only verify that the transactions are valid in the presently publishable block. when publishing, these miners assume that the longest chain is the one with the most support behind it, and consequently publish to that chain. Why would there be any other chain? One reason is because we have a bad actor. This is an entity that wants to modify the ledger in the past to, say, allow themselves to spend their coins multiple times.

#### Modifying Previous Transaction Blocks
This is difficult to do, as each block in the blockchain is entirely reliant on every block before it being exactly what was verified. This is accomplished through some technical crypto magic called hash functions. You can research hash functions, or you can take my word that the information contained in every block is placed through a special function that dramatically changes if any piece of information is altered. So if someone goes back 3 blocks and wants to change that information, they have to discard all the computation completed to validate that block and all subsequent blocks. They must then expend the time and resources to recompute the hash functions for all subsequent blocks based on the change in the prior block in an attempt to “catch up” to the longest chain. Once it has caught up and surpasses the old chain, this modified chain will be the assumed correct chain with the most PoW backing, which is then assumed correct and appended to.

*DEEP BREATH*

Yeah, that’s a bit of a mouthful. Let me just summarize what this implies. If someone has enough computational power (51% hash power), it can modify its own transactions on previous blocks and allow it to send the same coin as many times as it pleases. It allows it to control which blocks get posted to the network, allowing full monopoly over the system. If you don’t believe me, read the bitcoin whitepaper, the technical document describing the protocol. It fully rests on the condition that an entity does not contain a majority of the hash power. It quickly creates complete centralization, entirely defeating the point of bitcoin. That’s, well… not good.

#### 51% HASH POWER
So if anyone has access to 51% of the bitcoin protocol hashpower, they can make what is otherwise an immutable ledger, well, mutable. But what would it entail to get 51% Hash Power?

![](/images/govt-bitcoin/hashrate-hist.png')
Source: https://blockchain.info/charts/hash-rate

The current hash power is ~7.5 million TeraHashes per second, but it has nearly reached 10MM, so we’ll use this number. Assuming a state government didn’t have any mining operations, they would need to generate 10.4MM TH/s. This would bring the total to 20.4MM, with said gov’t owning ~51%.

So a government can now change the blockchain, dictate which blocks are posted to the ledger, and begin to build its monopoly as other miners are forced out of business. I suspect that bitcoin would fall drastically. Why wouldn’t it?

### How much would it cost?
As bitcoin grows larger and more miners join the pool, this task gets harder and harder for any gov’t to achieve. That’s a lot of computational power. But what would it cost a government to render bitcoin useless starting from scratch, buying all brand new equipment?

Without getting into the details of why it is the best piece of equipment to mine with, pretty much everyone uses what is called and ASIC, or Application Specific Integrated Circuits. These are specially designed chips made solely for the purpose of mining bitcoin. Well, if Bi Wang brings their announced ASIC to market soon, $68,000 will net you 1 PH/s, or 1,000 TH/s. We would need 10,400 of these bundles for a total cost of, wait for itttttttt………. ~$700MM. Well that’s… Not really that much, is it? I mean, that’s 0.1% of what the government spent on TARP to bail out insurance companies and the like in 2008. It’s 0.05% of the US’s discretionary budget expenditures for 2018. Even if we want to be conservative and double or triple this cost, I think it is safe to say that for any country with a large budget, this is feasible. The US and China are top of the list.

### Would they do it?
Well, if the USA starts thinking that Bitcoin is a serious threat to its own financial infrastructure, it would probably just make it illegal to buy or trade bitcoin. Can it enforce this? Probably not if people go through TOR or other IP address obfuscating means. But it creates a significant barrier and I can guarantee you it would have a significant impact on its price. Just look what happened when China mentioned shutting down exchanges these past few weeks. But this would not be wholly effective. If they wanted to really stop bitcoin, they would need to make it obsolete, and to do that, they could execute a 51% attak.

### Well damn, what to do?!
I’m not trying to spread FUD (Fear, Uncertainty and Doubt)–I am personally invested (and probably over-extended) in cryptocurrencies of all sorts, and I love the potential of the underlying technology. But I am trying to make sure everyone is aware of this possibility. This problem that I have spelled out in this post refers only to Proof of Work, while I think the general idea is still completely valid for blockchains that use proof-of-stake. With such significant buying power, a nation-state could buy a majority stake in a PoS coin and have it run into the same problem. Ultimately, we’ll have to hope that the computational power grows to such a level that countries cannot hope to catch up. But this will also mean less incentivization of just anyone starting up a mining operation, as is currently the case, leading to further centralization.

### Conclusion
I think what this means is that ASIC resistance will be necessary for long-term viability and lack of government manipulation of the ledger. PoS will likewise need to come up with clever solutions to deal with the inevitable issue of centralized concentration as nation-states buy up majority positions in their coins. I think this is something that has been brushed under the table because “it would never happen” which is always the case until, well, it does. I’d love to hear why I’m wrong, or some solutions to the problem in the comments below. Hope to hear some interesting perspectives!

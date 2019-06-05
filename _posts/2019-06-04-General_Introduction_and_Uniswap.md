---
layout: post
mathjax: true
date:   2019-06-04 14:15:00 +0000
title:  "Disruption or disillusion? | Upcoming Exchange concepts - A farewell to the order book? | Part 1"
headerimg: header1.jpg
---


# Disruption or disillusion? 

## Upcoming Exchange concepts - A farewell to the order book?

![]({{site.baseurl}}/assets/img/header1.jpg)

<p style="text-align: center;">Part 1 - General Introduction and Uniswap</p>

Cryptoprojects often praise themselves as disruptive "all new" projects. If you take a look behind the scenes, in most projects disruption becomes disillusion. Scam, bad copy-cats, ideas far beyond reality, mooning marketing concepts and "making already existing solutions just more inefficient", is predominant in the blockchain scene. Fortunately, people got more and more suspicious after the first bubble bursted. Hence, it became harder for bullshit to survive and more and more promising projects evolve. But are these project really disruptive? Do they have the potential to take over what we used to know? 

I am a finance PhD student - currently employed as an auditor at Chainsecurity (one of the leading blockchain security companies in the world). We audit big projects and get unique insights into them. I will introduce my favorite (often - but not only finance related) projects in my blog series: **Disruption or disillusion?** If you are interested follow me @ecofork (twitter) or subscribe here. Please, don't let this be a one-man show and start a lively discussion about these topics. 
Topic: **Upcoming Exchange concepts - A farewell to the order book?** *Part 1 - General Introduction and Uniswap*

Quick reminder on how common markets are classified and how they work. If you know it, feel free to skip the next two paragraphs. 

We usually differ between three different market types. 
-   Dealer market
-   Broker market
-   Exchange

We won't go into detail here for Dealer and broker markets. This can be looked up quickly in the [linked articles][1]. Let us focus on Exchanges (very high-level and simplified). Exchanges try to connect the two parties (buyer and seller) directly. Usually done by an auction based market. In an auction based market buyers enter competitive bids and sellers submit competitive offers. The exchange keeps track of all bids and offers (asks) in a so called [orderbook](https://en.wikipedia.org/wiki/Order_book_(trading)). An exchange tries to match two orders if possible. The current price is the price where the last bid/ask match was possible. The bid ask spread is the price different between the bid and ask orders closest to the current price.
The example below illustrates an order-book with trades. Here are is a [Youtube video][3].

*Illustration*

The description above is very high-level but it is not necessary to go into further detail here. Just some quick addition: There are different ways to match the orders and the auction implementation may vary a little. Even though, it might be a little too general, let us refer to these types of exchanges "order book based" (sometimes referred as Central Limit Order Book CLOB - I did not want to use this term because it can be misleading) exchanges.

Exchanges (Order book based), brokers and dealer markets is what we are used to, in common finance. But there is more. Besides [Request for quotation (RFQ)][4] exchanges which might still sound familiar to some ([KYBER](https://kyber.network/) and [AIRSWAP](https://www.airswap.io/) are using this technique), there are projects like [Uniswap](https://uniswap.io/) and [Bancor](https://www.bancor.network/). This article will focus on [Uniswap](https://uniswap.io/). A project which has enormous support in the community and [increasing volume][5]. It is backed by the Ethereum Foundation and has lately been [funded by Paradigma](https://www.theblockcrypto.com/2019/04/23/paradigm-backs-decentralized-exchange-protocol-uniswap/). To make markets they use an algorithm. This technique is sometimes referred to as "Automatic Market Maker". I do not like this term. Today, everything is somehow automated. This makes it quite confusing. The particular variant [Uniswap](https://uniswap.io/) uses, is called **Constant Product Market Maker Model (CPMMM)**. The CPMMM is a simple deterministic function. And CPMMM discribes what is done pretty accurate - as we will see below.

I do not want to call it a new type because I do not know if they are new (PLEASE CONTACT ME IF YOU HAVE INFORMATION). Most likely this technique has been around for quite some time but lead an obscure existence. 

*A market without an orderbook. How does the CPMMM work?*

I will summarize the Constant Product Market Maker Model briefly. For further information, please refer to the provided links at the end of the article TODO FOOTNOTE. In [Uniswap](https://uniswap.io/) there is no order book. The CPMMM always provide liquidity. The price is a function depending on supply and demand. Given a pair of assets $$Asset_A$$ and $Asset_B$ e.g. DAI and ETH. The function is:

$$supplyAsset_A*supplyAsset_B=C$$

The $supplyAsset_A$ is the amount of Asset A currently available on the exchange and the same applies to Asset B. 

The product is some value $$ C $$.

For example: 
$$ 100_{DAI}*100_{ETH}=10000_{DAIxETH} $$. So far, so good.

Two participants exist on [Uniswap](https://uniswap.io/). So called **liquidity provider** and the **common traders**. 
First, let us focus on the trader who wants to buy $$5_{DAI}$$ for $$ETH$$. Given the function above and the example liquidity of $$100_{DAI}$$ and $$100_{ETH}$$ on the exchange, the trader can calculate the price they have to pay for $$5_{DAI}$$. The simple rule is: *Keep the product constant*. Hence, after the trade has been executed, the product still needs to be $$10000_{DAIxETH}$$. Let's see how much ETH the trader needs to put into the ETH liquidity pool to take out $$5_{DAI}$$ and keep the product constant. This can easily be calculated by $$(100_{DAI} - 5_{DAI}) * (100_{ETH} + x_{ETH}) = 10000_{DAIxETH}$$. We subtract $$5_{DAI}$$ because they are taken out of the pool. We add $$x_{ETH}$$ because that is what the trader needs to pay (put into the pool) for taking the $$5_{DAI}$$ out. Solving for $$x_{ETH}$$ gives $$x_{ETH} = \frac{10000_{DAIxETH}}{95_{DAI}} - 100_{ETH}$$. Hence, the trader need to pay $$x_{ETH} = 5.263158_{ETH}$$ into the ETH pool for taking out $$5_{DAI}$$. This price seems reasonable because we started with a 1:1 ration of DAI and ETH. If one asset has high demand, the liquidity pool will have less and less of this asset. Hence, it gets more and more expensive. Obviously, the function is a multiplication and therefore, this does not scale linearly. This can easily be visualized by plotting the function and all possible prices. I also added two example trades. More information on the trades is below the image.

![]({{site.baseurl}}/assets/img/CPMMM_plot.png)

In this example, let us assume we have 100 token x and 100 token y. Hence, the product $C$ would be $$C=100*100=10000$$.The initial start from which prices are calculated, would be the point A in the picture. Let us assume trader B will buy $$20_y$$ token. Hence, trader B has to pay (put into the liquidity pool): $$(100_y-20_y)*(100_x+x_x)=10000_{x*y}$$. Therefore, $$x_x=\frac{10000_{x*y}}{(100_y-20_y)}-100_x$$. Thus, we end up at point B (bue) in the illustration above.

Let us assume another trader C. This trader wants to buy 75 x token. Hence, trader C has to pay (put into the liquidity pool): $$(80_y+x_y)*(125_x-75_x)=10000_{x*y}$$. Thus, $$x_x=\frac{10000_{x*y}}{(125_x-75_x)}-80_y$$. We end up at point C (red) in the illustration above. It is obvious how the price shifts on the line.

| Initial | price to pay | new | 
| ------ | ------- | ------ |
| $$100_x$$ : $$100_y$$ | $$25_x$$ for $$20_y$$ | $$125_x$$ : $$80_y$$ |
| $$125_x$$ : $$80_y$$  | $$120_y$$ for $$50_x$$ | $$50_x$$ : $$200_y$$ |

It is easy to see that the price impact gets less if the liquidity gets bigger relative to the order size. But this is similar to "common" exchanges. In the above example the last oder was over 60 percent of the whole liquidity of token y. Most likely it would have been very hard to fill this order at once on a "common" exchange. As you can see this is not rocket since. I hope this is clear so far. If not I provided links on the bottom of the page to other blog post. They do explain the same in other words. Ok, let us move on.

Above, we assumed an initial liquidity pool aka supply of $$100_{DAI}$$ and $$100_{ETH}$$. Where did this come from? Let us look behind the scenes and see how liquidity is added to an exchange contract. Therefore, so called liquidity provider can deposit DAI and ETH into the liquidity pool. Let us assume a newly created exchange. No DAI and no ETH liquidity is deposited. Liquidity provider, as the name suggests, provide liquidity. But it is a little bit different to what most readers might be used. A liquidity provider always needs to provide both assets. In our example they need to provide ETH and DAI.
A liquidity provider cannot just add ETH or DAI. This would not make sense in the CPMM model. Hence, the liquidity provider needs to deposit liquidity for both sides. In our example they need to add ETH and DAI in the correct ratio. The correct ratio is given by the current price. Let us assume the price is $$10_{\frac{DAI}{ETH}}$$. Hence, they need to deposit ten times more DAI than ETH. E.g. $$1000_{DAI}$$ and $$100_{ETH}$$. If the price does not change, the next liquidity provider will add liquidity for both assets in the same ratio. If the price changes the liquidity provider will adjust the ratio. In case, they would not, arbitrageurs will immediately correct the price. 

*Illustration*

Liquidity provider get so called liquidity token to keep track of their stake in the liquidity pool. They can redeem their token for the corresponding liquidity pool share. In a nutshell, that's all. This sounds a little bit too simple. But maybe this is what makes this idea efficient and brilliant. What are the implications and drawbacks? Can the system collapse? Let's go into further detail and work through the questions. 

Implications and drawbacks

The attentive reader will quickly realize that liquidity provider, in contrast to traders, are exposed to a risk. Additionally, they need to lock down their funds to provide the liquidity. Hence, they do have opportunity costs for the locked down capital. Therefore, it will not be discussed further. Therefore, let's check the risk a liquidity provider bears. In this example let's assume the fair value of $$1_{DAI}$$ is $$1_{ETH}$$ (I know... it's for illustration purpose only).

*Scenario 1:*

No trades happen

Value on Uniswap

| $$t_0$$ | $$t_1$$ | $$t_2$$ |
| -------- | -------- | -------- |
| 100 DAI | 100 DAI | 100 DAI | 
| 100 ETH | 100 ETH | 100 ETH | 

Total value in $$t_2$$

| Currency | Value | 
| -------- | -------- | 
| DAI | 200 DAI | 
| ETH | 200 ETH | 
| mixed | 100 DAI 100 ETH|

(Assuming another exchange provides enough volume at the current $$1_{ETH} = 1_{DAI}$$ price. Because, in case, the liquidity provider is the only one, another exchange is needed to convert the corresponding funds.)

-TBD Kurvenbild-


In $$t_3$$ the liquidity provider withdraws his funds and gets back what he put in initially ($$100_{DAI}$$ and $$100_{ETH}$$). Hence, the liquidity provider only has opportunity costs because they did not earn any interest on the capital in this time. The opportunity cost for locked down capital is pretty obvious. The liquidity provider could use the capital and e.g. earn interest rates on it (e.g. on compound.finance or xxx). 

*Scenario 2:*

Trader 1 buys 5 DAI for ETH.

| $$t_0$$ | $$t_1$$ | $$t_2$$ | 
| -------- | -------- | -------- | 
| 100 DAI | 95 DAI | 95 DAI |
| 100 ETH | 105.263158 ETH | 105.263158 ETH |

Total value in $$t_2$$

| Currency | Value | 
| -------- | -------- | 
| DAI | $$95_{DAI} + \frac{105.263158_{ETH}}{5.263158_{\frac{ETH}{DAI}}}*5=195_{DAI}$$ | 
| ETH | $$95_{DAI}*\frac{5.263158_{\frac{ETH}{DAI}}}{5} + 105.263158_{ETH} = 205.263158_{ETH}$$ | 
| mixed | 100 DAI 100 ETH |

(Assuming another exchange provides enough volume at the current $$\frac{5.263158_{ETH}}{5} := 1_{DAI}$$ price. Because, in case, the liquidity provider is the only one, another exchange is needed to convert the corresponding funds.)

- TBD Kurvenbild-

This time, the liquidity provider gets $$95_{DAI}$$ and $$105.263158_{ETH}$$ back. Now DAI is worth more than ETH. Therefore, the total value in DAI or ETH changes according to the currency used for evaluation. But overall, the value does not change. As before, the liquidity provider only has opportunity costs.


*Scenario 3:*

Trader 1 buys 5 DAI for ETH $$5.263158_{\frac{ETH}{DAI}}$$.
     
Trader 2 buys 5 DAI for ETH $$5.84795_{\frac{ETH}{DAI}}$$.

| $$t_0$$ | $$t_1$$ | $$t_2$$ | 
| -------- | -------- | -------- | 
| 100 DAI | 95 DAI | 90 DAI |
| 100 ETH | 105.263158 ETH | 111.111 ETH |

Total value in $$t_2$$

| Currency | Value | 
| -------- | -------- | 
DAI | $$90_{DAI} + \frac{111.111_{ETH}}{5.84795_{\frac{ETH}{DAI}}} *5 = 185_{DAI}$$ | 
ETH | $$90_{DAI}*\frac{5.263158_{\frac{DAI}{ETH}}}{5} + 111.111_{ETH} = 216.3741_{ETH}$$ | 
mixed | 99.49991 DAI 100 ETH |

(Assuming another exchange provides enough volume at the current $$\frac{5.263158_{ETH}}{5} := 1_{DAI}$$ price. Because, in case, the liquidity provider is the only one, another exchange is needed to convert the corresponding funds.)

- TBD Kurvenbild-

Now, it gets interesting. The liquidity provider would get back $$90_{DAI}$$ and $$111.111_{ETH}$$. But in total the liquidity provider lost $$0.50009_{DAI}$$ (or the corresponding amount in ETH). This is the additional risk the liquidity provider bears. To get back his initial investment the liquidity provider always needs to trade the asset which lost worth against the one which gained worth. As soon as the price starts moving into one direction, the liquidity provider will get the latest (but worst) price, to trade back his funds. In case the latest price was not the price to which all trades happened, a loss will be the result. In our example there was one trade at $$5.263158_{\frac{ETH}{DAI}}$$ and one at $$5.84795_{\frac{ETH}{DAI}}$$. To get back the initial investment of $$100_{DAI}$$ and $$100_{ETH}$$ the liquidity provider would need to trade $$5.84795_{ETH}$$ for $$5_{DAI}$$ and $$5.263158_{ETH}$$ for another $$5_{DAI}$$. But $$5.263158_{\frac{ETH}{DAI}}$$ is history. The current exchange rate is $$5.84795_{\frac{ETH}{DAI}}$$ and therefore, worse. Hence, the liquidity provider needs to exchange $$11.111_{ETH}$$ at $$5.84795_{\frac{ETH}{DAI}}$$. Thus, they lose $$0.5000898=10_{DAI}-\frac{11.111_{ETH}}{5.84795_{\frac{ETH}{DAI}}}*5$$. The loss increases if more trades happened at a more favorable price and/or the price gap increases between the last price and the prices before.

What is the compensation for someone to become a liquidity provider? They do get a fee which is charged with each trade. The million dollar question is, if or when do the fees compensate the risk plus the opportunity costs.


I do not want to write the articles too long. Therefore, I will stop here. 

What makes Uniswap so interesting? 

Pros:

   -   simplicity
   -   always liquidity
   -   ... TBD

Cons:

   -   No limit orders
   -   ...

Conclusion

I sometimes read that large orders on Uniswap are more expensive. I need object that this only happens if they are large compared to the provided liquidity. A large order which drains a big share of the liquidity on a "common" exchange will also be expensive or not executed at all.

To be done

I love the simplicity and als the research opportunity that come up with the CPMM. It totally changes the market microstructure. Deterministic price changes and the transparent structure make it (imho) to an amazing research topic. (TBD maybe mention paper project topics) Can you come up with more research topics?

Right now, Uniswap does not want to replace existing exchanges (Link). Furthermore, they see themselves as a kind of supplementary exchange and welcome arbitrage traders to adjust the prices.
Hence, Uniswap is depended on other exchanges to keep the rates balanced.
Uniswap is still beta and highly experimental. But this also makes it extremely interesting to think about, when it could break or collapse. 
In the end, it would be interesting if Uniswap theoretically could replace existing exchange/markets types. Would this be a market type which could make it out of the crypto space and disrupt the predominant exchange types? Has it major drawbacks or limits? What do you think?

If you like this article please subscribe. Tell me if you additionally would prefer podcasts or Youtube videos.

Upcoming topics: 
   -  Does it make sense to become a liquidity provider for Uniswap?
   -  arbitrage opportunities (at best this should be done by liquidity providers)
   -  Can the system collapse?
   -  How is the code implementation?
   -  Bancor another concept

If you are not into my wording, there are multiple articles explaining more or less the same with other words. Check them out:

https://medium.com/scalar-capital/uniswap-a-unique-exchange-f4ef44f807bf


[1]: https://www.investopedia.com/terms/d/dealersmarket.asp und https://www.investopedia.com/ask/answers/06/brokerandmarketmaker.asp

[3]: https://www.youtube.com/watch?v=Iaiw5iGjXbw

[5]: https://mikemcdonald.github.io/eth-defi/

----------------------------------------------------------
Part 2 - When does it make sense to be a liquidity provider on Uniswap

In the first part, we covered the very basics of Uniswap. An exchange which has no orderbook but a so called Constant Product Market Model (CPMM). It's simple yet elegant. If you missed the first part, you can find it [here]().

A Uniswap liquidity provider gets a compensation for their risk and opportunity costs. This compensation is a fee. Currently it is $$0.3\%$$. This value seems arbitrary. I could not find any theoretical foundation which proofs that this fee and the risk/opportunity costs are balanced. It might be that a liquidity provider gets way too much or not enough. 

Let's see.

The liquidity provider has the following costs: *costs = opportunity costs + risk*. The fee needs to, at least, be marginal higher than the costs. Therefore, we need to check if $$costs < fee$$. The opportunity costs represent, what income an alternative investment would have generated. 

----------------------------------------------------------
Part 3 - Uniswap's Market-microstructure and some theory

----------------------------------------------------------
Part 4 - How to use Uniswap

----------------------------------------------------------
Part 5 - Uniswap's code implementation



----------------------------------------------------------
----------------------------------------------------------

NOTES LEFT OVERS AND REMINDERS - DELETE FOR LIVE VERSION

----------------------------------------------------------

Value on another Exchange

| $$t_0$$ | $$t_1$$ | $$t_2$$ | $$t_3$$ |
| -------- | -------- | -------- | -------- |
| 100 DAI | 100 DAI | 100 DAI | 100 ETH |
| 100 ETH | 100 ETH | 100 ETH | 100 ETH |


<Kurvenbild-


The project was created by Hayden Adams, a former mechanical engineer.

Request for quotation (RFQ) exchanges for example. Crypto projects like KYBER or AIRSWAP make use this technique for trading. RFQ is pretty simple. The trade basically asks for quotes and market maker provide quotes. The trader picks the best one.

Gas efficiency is just one of the advantages of the Uniswap protocol, more advantages include:

    Uniswap is decentralized, so, it does not rely on third parties for its operation. Furthermore, Uniswap is freely accessible to anyone wishing to connect to the protocol.
    Cost of executing a trade on Uniswap is relatively cheap compared to other digital asset exchanges.
    Uniswap allows any user to create an exchange contract for any given ERC20 token.

Uniswap, however, does come with its limitations:

    Uniswap does rely on arbitrage trading in order to keep the exchange prices of tokens on the protocol in check. This means that Uniswap is relying on the existence of other digital asset exchanges to keep exchange rates balanced.
    Uniswap is still very much experimental, more development is required on the protocol to see just how effective it can be in facilitating digital asset exchange.

Danach Bancor
Danach wieivel das eigentlich genutzt wird (transactionen ansehen)
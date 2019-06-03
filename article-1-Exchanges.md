# Disruption or disillusion? 

## Upcoming Exchange concepts - A farewell to the order book?
Part 1 - General Introduction and Uniswap

Cryptoprojects often praise themselves as disruptive "all new" projects. If you take a look behind the scenes, in most projects disruption becomes disillusion. Scam, bad copy-cats, ideas far beyond reality, mooning marketing concepts and "making already existing solutions just more inefficient", is predominant in the blockchain scene. Fortunately, people got more and more suspicious after the first bubble bursted. Hence, it became harder for bullshit to survive and more and more promising projects evolve. But are these project really disruptive? Do they have the potential to take over what we used to know? 

I am a finance PhD student - currently employed as an auditor at Chainsecurity (one of the leading blockchain security companies in the world). We audit big projects and get unique insights into them. I will introduce my favorite (often - but not only finance related) projects in my blog series: **Disruption or disillusion?** If you are interested follow me @ecofork (twitter) or subscribe here. Please, don't let this be a one-man show and start a lively discussion about these topics. 
Topic: **Upcoming Exchange concepts - A farewell to the order book?** *Part 1 - General Introduction and Uniswap*

Quick reminder on how common markets are classified and how they work. If you know it, feel free to skip the next two paragraphs. 

We usually differ between three different market types. 
-   Dealer market
-   Broker market
-   Exchange

We won't go into detail here for Dealer and broker markets. This can be looked up quickly in the [linked articles][1]. Let us focus on Exchanges (very high-level and simplified). Exchanges try to connect the two parties (buyer and seller) directly. Usually done by an auction based market. In an auction based market buyers enter competitive bids and sellers submit competitive offers. The exchange keeps track of all bids and offers (asks) in a so called [orderbook][2]. An exchange tries to match two orders if possible. The current price is the price where the last bid/ask match was possible. The bid ask spread is the price different between the bid and ask orders closest to the current price.
The example below illustrates an order-book with trades. Here are is a [Youtube video][3].

*Illustration*

The description above is very high-level but it is not necessary to go into further detail here. Just some quick addition: There are different ways to match the orders and the auction implementation may vary a little. Even though, it might be a little too general, let us refer to these types of exchanges "order book based" (sometimes referred as Central Limit Order Book CLOB - I did not want to use this term because it can be misleading) exchanges.

Exchanges (Order book based), brokers and dealer markets is what we are used to, in common finance. But there is more. Besides [Request for quotation (RFQ)][4] exchanges which might still sound familiar to some ([KYBER](https://kyber.network/) and [AIRSWAP](https://www.airswap.io/) are using this technique), there are projects like [Uniswap](https://uniswap.io/) and [Bancor](https://www.bancor.network/). This article will focus on [Uniswap](https://uniswap.io/). A project which has enormous support in the community and [increasing volume]5. It is backed by the Ethereum Foundation and has lately been [funded by Paradigma][https://www.theblockcrypto.com/2019/04/23/paradigm-backs-decentralized-exchange-protocol-uniswap/]. To make markets they use a deterministic function. They call this technique **Constant Product Market Maker Model (CPMMM)**. This describes pretty exactly what they do.
I do not want to call it a new type because I do not know if they are new (PLEASE CONTACT ME IF YOU HAVE INFORMATION). Most likely this technique has been around for quite some time but lead an obscure existence. 

*A market without an orderbook. How does the CPMMM work?*

I will summarize the Constant Product Market Maker Model briefly. For further information, please refer to the provided links at the end of the article TODO FOOTNOTE. In [Uniswap](https://uniswap.io/) there is no order book. The CPMMM always provide liquidity. The price is a function depending on supply and demand. Given a pair of assets $`Asset_A`$ and $`Asset_B`$ e.g. DAI and ETH. The function is:
```math
supplyAsset_A*supplyAsset_B=C
```

The $`supplyAsset_A`$ is the amount of Asset A currently available on the exchange and the same applies to Asset B. 

The product is some value $`C`$. 

For example: $`100_DAI x 100_ETH = 10000_DAIxETH`$. So far, so good.

Two participants exist on [Uniswap](https://uniswap.io/). So called **liquidity provider** and the **common traders**. 
First, let us focus on the trader who wants to buy 5 DAI for ETH. Given the function above and the example liquidity of 100 DAI and 100 ETH on the exchange, the trader can calculate the price they have to pay for 5 DAI. The simple rule is: Keep the product constant. Hence, after the trade the product still needs to be $`10000_DAIxETH`$. Let's see how much ETH the trader needs to put into the ETH liquidity pool to take out 5 DAI and keep the product constant. This can easily be calculated by $`100_DAI - 5_DAI * 100_ETH + x_ETH = 10000 DAIxETH`$. We substract $`5_DAI`$ because they are taken out of the pool. We add $`x_ETH`$ because that is what the trader needs to pay (put into the pool) for taking the $`5_DAI`$ out. Solving for $`x_ETH`$ gives $`x_ETH = 10000_DAIxETH / 95_DAI - 100_ETH`$. Hence, $`x_ETH = 5.263158_ETH`$. This price seems reasonable because we started with a 1:1 ration of DAI and ETH. If one asset has high demand, the liquidity pool will have less and less of this asset. Hence, it gets more and more expensive.
Below there are further example trades and how the price changes.

*Illustration or Table*

Above, we assumed an initial liquidity pool aka supply of 100 DAI and 100 ETH. Where did this come from? Let us look behind the scenes and see how liquidity is added to an exchange contract. Therefore, so called liquidity provider can deposit DAI and ETH into the liquidity pool. Let us assume a newly created exchange. No DAI and no ETH liquidity is deposited. Liquidity provider, as the name suggests, provide liquidity. But it is a little bit different to what most readers might be used. A liquidity provider always needs to provide both assets. In our example they need to provide ETH and DAI.
A liquidity provider cannot just add ETH or DAI. This would not make sense in the CPMM model. Hence, the liquidity provider needs to deposit liquidity for both sides. In our example they need to add ETH and DAI in the correct ratio. The correct ratio is given by the current price. Let us assume the price is 10 DAI/ETH. Hence, they need to deposit ten times more DAI than ETH. E.g. 1000 DAI and 100 ETH. If the price does not change, the next liquidity provider will add liquidity for both assets in the same ratio. If the price changes the liquidity provider will adjust the ratio. In case, they would not, arbitrageurs will immediately correct the price. 

*Illustration*

Liquidity provider get so called liquidity token to keep track of their stake in the liquidity pool. They can redeem their token for the corresponding liquidity pool share. In a nutshell, that's all. This sounds a little bit too simple. But maybe this is what makes this idea efficient and brilliant. What are the implications and drawbacks? Can the system collapse? Let's go into further detail and work through the questions. 

Implications and drawbacks

The attentive reader will quickly realize that liquidity provider, in contrast to traders, are exposed to a risk. Additionally, they need to lock down their funds to provide the liquidity. Hence, they do have opportunity costs for the locked down capital. Therefore, it will not be discussed further. Therefore, let's check the risk a liquidity provider bears. In this example let's assume the fair value of 1 DAI is 1 ETH (I know... it's for illustration purpose only).

Scenario 1:
     No trades happen

Value on Uniswap

| $`t_0`$ | $`t_1`$ | $`t_2`$ | $`t_3`$ |
| -------- | -------- | -------- | -------- |
| 100 DAI | 100 DAI | 100 DAI | 100 DAI |
| 100 ETH | 100 ETH | 100 ETH | 100 ETH |

Total value in

| DAI | ETH | mixed |
| -------- | -------- | -------- |
| 200 DAI | 200 ETH | 100 DAI 100 ETH|

(Assuming another exchange provides enough volume at the current $`1 ETH = 1 DAI`$ price. Because, in case, the liquidity provider is the only one, another exchange is needed to convert the corresponding funds.)

<Kurvenbild>


In $`t_3`$ the liquidity provider withdraws his funds and gets back what he put in initially (100 DAI and 100 ETH). Hence, the liquidity provider only has opportunity costs because they did not earn any interest on the capital in this time. The opportunity cost for locked down capital is pretty obvious. The liquidity provider could use the capital and e.g. earn interest rates on it (e.g. on compound.finance or xxx). 

Scenario 2:
     Trader 1 buys 5 DAI for ETH.

| $`t_0`$ | $`t_1`$ | $`t_2`$ | $`t_3`$ |
| -------- | -------- | -------- | -------- |
| 100 DAI | 95 DAI | 95 DAI | 95 ETH |
| 100 ETH | 105.263158 ETH | 105.263158 ETH | 105.263158 ETH |

Total value in 

| DAI | ETH | mixed |
| -------- | -------- | -------- |
| $`95 DAI + 105.263158 ETH / 5.263158 ETH/DAI *5=195 DAI`$ | $`95*(5.263158/5) + 105.263158 = 205.263158 ETH`$ | 100 DAI 100 ETH |

(Assuming another exchange provides enough volume at the current $`(5.263158 ETH/5) = 1 DAI`$ price. Because, in case, the liquidity provider is the only one, another exchange is needed to convert the corresponding funds.)

<Kurvenbild>

This time, the liquidity provider gets 95 ETH and 105.263158 ETH back. Now DAI is worth more than ETH. Therefore, the total value in DAI or ETH changes according to the currency used for evaluation. But overall, the value does not change. As before, the liquidity provider only has opportunity costs.


Scenario 3:
     Trader 1 buys 5 DAI for ETH (5.263158 ETH/DAI).
     Trader 2 buys 5 DAI for ETH (5.84795  ETH/DAI).

| $`t_0`$ | $`t_1`$ | $`t_2`$ | $`t_3`$ |
| -------- | -------- | -------- | -------- |
| 100 DAI | 95 DAI | 90 DAI | 90 DAI |
| 100 ETH | 105.263158 ETH | 111.111 ETH | 111.111 ETH |

Total value in 
| DAI | ETH | mixed |
| -------- | -------- | -------- |
| $`90 DAI + 111.111 ETH / 5.84795 ETH/DAI *5 = 185 DAI`$ | $`90*(5.263158/5) + 111.111 = 216.3741 ETH`$ | 99.49991 DAI 100 ETH |

(Assuming another exchange provides enough volume at the current $`(5.263158 ETH/5) = 1 DAI`$ price. Because, in case, the liquidity provider is the only one, another exchange is needed to convert the corresponding funds.)

<Kurvenbild>

Now, it gets interesting. The liquidity provider would get back 90 DAI and 111.111 ETH. But in total the liquidity provider lost $`0.50009`$ DAI (or the corresponding amount in ETH). This is the additional risk the liquidity provider bears. To get back his initual investment the liquidity provider always needs to trade the asset which lost worth against the one which gained worth. As soon as the price starts moving into one direction, the liquidity provider will get the latest (but worst) price, to trade back his funds. In case the latest price was not the price to which all trades happened, a loss will be the result. In our example there was one trade at $`5.263158 ETH/DAI`$ and one at $`5.84795 ETH/DAI`$. To get back the initial investment of 100 DAI and 100 ETH the liquidity provider would need to trade $`5 ETH`$ at $`5.84795 ETH/DAI`$ and 5 at $`5.263158 ETH/DAI`$. But  $`5.263158 ETH/DAI`$ is history. The current exchange rate is $`5.84795 ETH/DAI`$ and therefore, worse. Hence, the liquidity provider needs to exchange $`10 ETH`$ at $`5.84795 ETH/DAI`$ and the loss occurs. The loss increases if more trades happened at a more favorable price and/or the price gap increases between the last price and the prices before.

What is the compensation for someone to become a liquidity provider? They do get a fee which is charged with each trade. The million dollar question is, if or when do the fees compensate the risk plus the opportunity costs.


I do not want to write the articles too long. Therefore, I will stop here. 

What makes Uniswap so interesting? Pros?

Cons?

Conclusion
Is it a thread for real world exchanges? 
Where are the limits?
What research can be done?

If you like this article please subscribe. Tell me if you additionally would prefer podcasts or Youtube videos.

Upcoming topics: 
   -  Does it make sense to become a liquidity provider for Uniswap?
   -  arbitrage opportunities (at best this should be done by liquidity providers)
   -  Can the system collapse?
   -  How is the code implementation?
   -  Bancor another concept

[1]: https://www.investopedia.com/terms/d/dealersmarket.asp und https://www.investopedia.com/ask/answers/06/brokerandmarketmaker.asp
[2]: https://en.wikipedia.org/wiki/Order_book_(trading)
[3]: https://www.youtube.com/watch?v=Iaiw5iGjXbw
[4]: https://www.investopedia.com/terms/r/request-for-quote.asp
[5]: https://mikemcdonald.github.io/eth-defi/
----------------------------------------------------------

Value on another Exchange

| $`t_0`$ | $`t_1`$ | $`t_2`$ | $`t_3`$ |
| -------- | -------- | -------- | -------- |
| 100 DAI | 100 DAI | 100 DAI | 100 ETH |
| 100 ETH | 100 ETH | 100 ETH | 100 ETH |


<Kurvenbild>


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
 Disruption or disillusion? 

The end of common exchanges?
A farewell to the order book.

Cryptoproject often praise themselfs as disruptive all new projects. If you take a look behind the scenes, most projects disruption becomes disillusion. Scam, bad copy-cats, ideas far beyond reality, mooning marketing concepts and making already existing solutions just more inefficient, is predominant in the blockchain world. Fortunately, people got more and more suspicious after the first bubble bursted. Hence, it became harder for bullshit to survive and more and more promising projects evolve. But are these project really disruptive? Do they have the potential to take over what we used to know? 

I am a finance PhD student - currently employed as an auditor at Chainsecurity (one of the leading blockchain security companies in the world). We audit big projects and get unique insights into them. I will introduce my favorite (oftenof - but not only finance related) projects in my blog series "Disruption or disillusion?". If you are interested follow me @ecofork (twitter) or subscribe here. Don't let this be a one-man show and please start a xyz discussion about these topics. This is article one. Topic: **The end of common exchanges?** *Upcoming Exchange concepts - a farewell to the order book?*

Quick reminder on how common markets are classified and how they work. If you know it, feel free to skip this part. We usually differ between three different market types. 
(1) Dealers/OTC (Over-The-Counter)
(2) Exchanges
(3) Brokers

We won't go into detail here for Dealer and broker markets. This can be looked up quickly in the linked wiki articles. Let us focus on very high-level on Exchanges. Exchanges try to connect the two parties (buyer and seller) directly. Usually done by an auction based market. In an auction based market buyers enter competitive bids and sellers submit competitive offers. The exchange keeps track of all bids and offers (asks) in a so called order book. The exchanges try to match two orders if possible. The current price is the price where the last bid/ask match was possible. The bid ask spread is the price different between the bid and ask orders closest to the current price.
The example below illustrates an order-book with trades.

<Illustration>

The description above is very high-level but it is not necessary to go into further detail here. Just some quick addition: There are different ways to match the orders and the auction implementation may vary a little. Even though it might be a little too general, let us refer to these types of exchanges "order book based"FOOTNOTE(Often referred as Central Limit Order Book CLOB. I did not want to use this term because it is kind of misleading.) exchanges.

Exchanges (Order book based), brokers and dealer markets is what we are used to, in common finance. But there is more. Besides Request for quotation (RFQ) exchanges which might still sound familiar to some (KYBER and AIRSWAP are using this technique), there are projects like Uniswap and bancor. This article will focus on Uniswap. A project which has enormous support in the community. It is backed by the Ethereum Foundation and has latly been founded by Paradigma FOOTNOTE(https://www.theblockcrypto.com/2019/04/23/paradigm-backs-decentralized-exchange-protocol-uniswap/). To make markets they use a deterministic function. They call this technique Constant Product Market Maker Model (CPMMM). This describes pretty exactly what they do.
I do not want to call it a new type because I do not know if they are new FOOTNOTE PLEASE CONTACT ME IF YOU HAVE INFORMATION. Most likely this technique has been around for quite some time but lead an obscure existence. 

How does the CPMMM work?
We will summarize the Constant Product Market Maker Model briefly. For further information, please refer to the provided links FOOTNOTE. In Uniswap there is no order book. Their CPMMM always provide liquidity. The price is a function depending on supply and demand. Given a pair of assets Asset_A and Asset_B e.g. DAI and ETH. The function is:
$supplyAsset_A*supplyAsset_B=C$ The $supplyAsset_A$ is the amount of Asset A locked in in the exchange contract and the same applies to Asset B. The product is some value $C$. For example 100 DAI x 100 ETH = 10000 DAIxETH. 
Two participants exist on Uniswap. So called **liquidity provider** and the **common trader**. 
Let us focus on the trader who wants to buy 5 DAI for ETH. Given the function above and the example liquidity of 100 DAI and 100 ETH on the exchange, the trader can calculate the price they have to pay for 5 DAI. The simple rule is: Keep the product constant. Hence, after the trade the product still needs to be 10000 DAIxETH. Let's see how much ETH the trader needs to put into the ETH liquidity pool to take out 5 DAI and keep the product constant. This can easily be calculated by 100 DAI - 5 DAI (the amount the trader did take) * 100 + x (the amount the trader needs to put in the pool for taking out 5 DAI) = 10000 DAIxETH. Solving for x gives x = 10000 DAIxETH / 95 DAI - 100ETH. Hence, x = 5.263158 ETH. This price seems reasonable because we started with a 1:1 ration of DAI and ETH. If one asset has high demand, the liquidity pool will have less and less of this asset. Hence, it gets more and more expensive.
Below there are further example trades and how the price changes.


We assumed an initial liquidity pool aka supply of 100 DAI and 100 ETH. Where did this come from? Let us look behind the scenes and see how liquidity is added to an exchange contract. Therefore, so called liquidity provider can deposit DAI and ETH into the liquidity pool. Let us assume a newly created exchange. No DAI and no ETH liquidity is deposited. A liquidity provider cannot add just ETH or just DAI. This would not make sense in the CPMM model. Hence, the liquidity provider will add ETH and DAI in the correct ratio. The correct ratio is given by the current price

Liquidity provider, as the name suggests, provide liquidity. But it is a little bit different to what most readers might be used. A liquidity provider always needs to provide t

This all sounds a little bit too simple. But this is what makes this idea efficient and brilliant.


How is it implemented?

What makes Uniswap so interesting? Pros?

Cons?

Conclusion
Is it a thread for real world exchanges? 
Where are the limits?
What research can be done?

If you like this article please subscribe. Tell me if you additionally would prefer podcasts or Youtube videos.



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
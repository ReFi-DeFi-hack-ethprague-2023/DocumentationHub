# LeverageReFi
## Flow

Alice, based in New York, decided to buy Ecological assets for $120k, which will be used to impact investment of new New York Green City Project: 
- `SCC`: Sky Scrapper Cow - bring farms to the top of NYC sky scrappers.
- `MilkyWay` - new fresh water river in NYC.
- `FucSEC` - project related alternative means of payment.

She wants to keep them as a long term investment. However, she doesn't want to lock the value.
Lending systems allow to take long positions and unlock the value.
Alice enters the `ReFiUmee` system, which has the `ReFi Leverage` lending pool and integrates with the vast Gho Aave inter-chain facilitator. 
She supplies and collaterizes the ReFi tokens at `ReFiUmee`. Then she leverages her position and borrows `100k Gho`. Aave inter-chain facilitator validates the request from the `ReFiUmee` using Axelar bridge, and mints `Gho` to Alice in the Optimism layer-2.
In the meantime a new bull market started. She used `50k` of liquid `Gho` to purchase optimistic, shit NFTs. Optimism is the new them of the bull run and she managed to  sell them for `300k` making `250k`.

The whole `ReFi Leverage` module is designed to get Gho and leverage ReFi assets. The fees are extreamly low, because she borrows from the system, rather than another liquidity provider. The fee is used only to compensate the risk, and will depend on the market conditions and system performance. At the beginning the fee is set to 1% / year.

3 years later, Alice decides to close her position. Her collateral is worth now `$200k`, the interest she had to pay is `100k (1.01**3 - 1) = 3.03k`. In summary, she was able to keep her long position with ecological assets: initial purchase of `120k` worth of `SCC, MilkyWay` and `Fuc*SEC` , she was able to use `100k` liquid `Gho`. At the end she has `250k - 100k - 3.03k = 146.07k Gho` and liquid (uncollaterized) `A, B, C` eco credits. Soon after that the market wants to celebrate the success of the _New York Green City Project_ and provides a way to bundle the ReFi tokens into an immortal _optimistic green_ NFT. Her NFT is worth `400k`.

The Green City project has just been completed, and now she enjoys her city even more, breathing a fresh air :smiley: 


## How we did it - EVM Side
We deploy a mock Aave GHO token contract and implement our own facilitator for it that is allowed to mint GHO tokens. The facilitator is informed by the Axelar bridge (which connects to the Cosmos chain) to mint tokens and also, upon burning, would bridge that state change back. 

In the Aave GHO token contract, the Facilitator contract is registered with its own mint limit and current mint level, which enables it to mint & burn GHO according to the IGhoToken spec.  

**Minting**
Axelar bridge calls the minting function, passing in the recipient and amount of new tokens.

**Burning**
User approves the Facilitator in the GHO token contract, then calls ```burn(amount)``` to transfer the tokens from his account to the Facilitator and burn them there. Only the Facilitator is allowed burn. Then the state change is bridged back to Cosmos. 

Check out the Solidity contracts repo! [link](https://github.com/ReFi-DeFi-hack-ethprague-2023/solidity-contracts)

## Cosmos Side 

More information: https://hackmd.io/Nw4kEV8ATbutKhzVbGrcHA?view

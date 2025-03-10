# QubicBay-Proposal

**NFT MARKETPLACE PROPOSAL**

Available Options:

Option 0: No, I don’t want

Option 1: Yes, approve the proposal.

**Project Overview**

We have developed the first Smart Contract that will allow NFT technology to be brought to Qubic tickchain. New blood, new users will be attracted by this possibility, creating greater interest and attention for the entire ecosystem.

**Marketplace functionality**

**Functions Specifications**

The Smart contract contains all the necessary functions expected from a typical NFT Marketplace, which are: 

- mint

- buy

- sell

- transfer

- exchange

- auction

- floor price

- make an offer

- accept offer

- getting NFT info

Thanks to this Smart Contract we will be able to launch an NFT Marketplace on Qubic tickchain, where users will be able to create/drop/mint NFTs/collections, buy/sell and trade NFTs.

**Fee Structure**

For each resale of NFTs on the secondary market, the Marketplace will retain a percentage of the total resale equal to 3%, which will be distributed as follows: 

2% will be retained by the Marketplace to cover management costs and future developments
1% will be sent to shareholders (check 'shareholder revenues' paragraph for more details)

**Shareholder revenues**

Shareholders will receive as revenue 1% of all sales made on the secondary market, only and exclusively where the sale is made with $Qubic as the payment method. 
If sales on the secondary market are paid with $CFB token, shareholders will not receive any percentage as revenues.

**Coins/Tokens accepted on the Marketplace**

Both $CFB and $Qubic will be accepted on the Marketplace, and both can be used by users to buy/sell NFTs on the secondary market.

However, there are some exclusive functions reserved for each: 

Only $Qubic will be accepted for minting NFTs (primary market)

On the other hand, $CFB will have a reserved exclusive function: the purchase of packages.

**What are packages?**

Packages (slots) explained

Whenever creators wants to launch a new collection of NFTs on our Marketplace, they will necessarily have to purchase a package of mintable NFTs (slots), the cost of which will vary based on the number of NFTs that will be part of the collection, i.e. for a collection of 1000 NFTs users will have to purchase a package worth 200 USDT of $CFB and so on up to a maximum of a package of 10,000 pieces of NFTs worth 2000 USDT in $CFB. 
 

**Creator earnings**

When creating a new collection, creators will be able to decide whether to withhold a percentage from future resales of the NFTs created, up to a maximum of 10%. This percentage, chosen by them, is necessary to support the work of creators and encourage them to use our platform.

**Technical Details**

Scope of service and Platform Features

**Platform Design:**

Web3 Interface for seamless NFT trading and management
Smart Contract integration for secure NFT transactions
Responsive Frontend & Backend Development for optimal user experience

**Core Functionalities:**

NFT Minting: Create and launch new NFT collections
NFT Trading: Buy, sell and transfer NFTs
Collection Management: Create and manage NFT collections
Marketplace Features: Listings, offers, auctions

**Smart Contract Integration:**

Wallet Integration via Qubic connect (metamask, walletconnect and ledger - as soon it is available)
Secure transaction handling
 
**SC Storage management**

Datasets (holder address, URI for NFT) are stored in the smart contract. The metadata, however, is stored on dedicated services (IPFS). Based on current estimates, users are able to create exactly up to 4194304 NFTs on 1GB storage, i.e. if one collection includes 3~4k NFTs, our platform can support up to 1000 collections. Furthermore, in the future, the storage capacity of Smart Contracts will be increased to 8-16 GB.

**Qbay MarketPlace Smart Contract**

Technical implementation for the collection and NFT in Qbay Smart Contract

All the collections and NFTs will be saved inside 1GB Storage that can be saved the state data and also it can be integrated in PFP MarketPlace

The info for NFT is as follows.

struct InfoOfNFT
{

 ``` id creator;                          // Identity of NFT creator
  id possesor;			     // Identity of NFT possesor
  id askUser;			     // Identity of Asked user
  id creatorOfAuction;		     // Creator of Auction
  sint64 salePrice;		     // This price should be set by possesor
  sint64 askMaxPrice;		     // This price is the max of asked prices
  uint64 currentPriceOfAuction;	     // This price is the start price of auctions
  uint32 startTimeOfAuction;	     // The start time of auction
  uint32 endTimeOfAuction;	     // The end time of auction
  uint32 royalty;			     // Percent from 0 ~ 100
  uint32 NFTidForExchange;	     // NFT Id that want to exchange
  Array<uint8, 64> URI;	             // URI for this NFT
  uint8 statusOfAuction;		     // Status of Auction(0 means that there is no auction, 1 means that tranditional Auction is started, 2 means that one user buyed the NFT in traditinoal auction)
  bit statusOfSale;		     // Status of Sale, 0 means possesor don't want to sell
  bit statusOfAsk;		     // Status of Ask
  bit paymentMethodOfAsk;		     // 0 means the asked user want to buy using $Qubic, 1 means that want to buy using $CFB
  bit statusOfExchange;		     // Status of Exchange
  bit paymentMethodOfAuction;	     // 0 means the user can buy using only $Qubic, 1 means that can buy using only $CFB
```

  };

constexpr uint32 PFP_MAX_NUMBER_NFT = 2097152;

Array NFTs;

As you can see above, the max number of NFTs is 2097152. it means that this smart contrat holds the NFTs up to 2097152.
The capacity of one NFT is 238byte and total capacity for 2097152 NFTs is less than 1GB.
All the infos(creator, possesor, URI, status, price, ... ,) for NFT will be saved in this NFT struct.
The implementation for collection is same with implementation of NFT. there is a struct for info of collection.

All features in PFP MarketPlace

`settingCFBAndQubicPrice` procedure

The only Marketplace owner can set the price for Qubic and CFB. it will be expressed as the amount of Qubic and CFB for 1 USD;
If other's try to use this procedure, it will be rejected by procedure.
If the Qubic smart contract supports the connection with Oracles in the future, this procedure would be removed and the Oracles would be connected for price of Qubic and CFB.

`createCollection` procedure

The user can create their collection. The CFB payment is only available to create the collection.
When the user creates the collection, he can set the type of collection weither the collection is for own or Dropping NFTs.

`mint` procedure

The user can mint the NFT in two option(minting a single NFT or a NFT using the collection). If user want to mint the NFT using his collection, he can mint the NFT without any fee, at this time, the creator and possessor of NFT should be creator of collection.
If user want to mint the single NFT without his collection, he need to pay the 5M $Qubic in Marketplace.

`mintOfDrop` procedure

The user can mint the NFTs using the Drop collection.
The user need to pay the fee(it will be set when the collection is created by the collection creator) to creator of collection. the creator of NFT would be creator of collection and the possessor would be the user who mint this NFT.

`transfer` procedure

The user can transfer their NFT to another user without fee.

`listInMarket` procedure

The user can list the NFT in the Market without fee when he want to sell the NFT. it means the status of sale is 1.
The user will set the price for sale in the amount of Qubic.

`buy` procedure

The user can buy the NFT if the status of sale for NFT is 1. the user can use the both of Qubic and CFB to pay the price of NFT.
If the user selects the CFB to pay the price, the price will be converted and calculated as CFB.
At this time, the fee will be distributed according to the set percent.

`cancelSale` procedure

The user can cancel the sale without fee.

`listInExchange` procedure

The user can list the NFT in the Exchange when he want to exchange his NFT with another NFT. it means that the status of another NFT(want to exchange) is 1;
If the another user already asked to exchange with his NFT, the possessor of NFT will be converted each other.
At this time, there is no fee.

`cancelExchange` procedure

The user can cancel the status of exchange without fee. it means that the status of another NFT(wanted to exchange) is 0.

`makeOffer` procedure

The user can make the offer with the price(he want to buy) if he want to buy the NFT. the user can use the both of Qubic and CFB to pay the price of NFT. also the price should be sent to marketplace at first.
If the user does not pay the price, the offer can not be made.
If another user make the offer with high price, the askUser and price will be changed with new user.
the user need to make in high price additional QBAY_MIN_DELTA_SIZE over than previous user.
The payment for previous user will be transferred to previous user.

`acceptOffer` procedure

If the user want to sell to the user who made the offer, the user can accept the offer.

`cancelOffer` procedure

If user want to cancel the Offer, he can use this proceudure. at this time, the paid amount of user who made the offer will be transferred to user who made the offer.

`createTraditionalAuction` procedure

The user can create the auction. user need to set the method of payment for price($Qubic or $CFB). Other users must bid in set mothed of payment.
The start and end time will be decided by creator of auction.

`bidOnTraditionalAuction` procedure

The users can bid in auction. the user need to bid in high price additional QBAY_MIN_DELTA_SIZE over than previous user.
The possessor of NFT will be changed whenever the user succeed in bid and the previous user receives the paid amount. and also the fee will be distributed reasonablly.

`changeStatusOfMarketPlace` procedure

Marketplace owner need to change the status of market. The users can create the collection and mint the NFT after marketplace owner changes the status as 1.
Marketplace owner want to create hie collection and NFT before other user creates the collection and NFT usint this smart contract.
So other users can create the collection and mint the NFT after marketplace owner changes the status of marketplace.

`END_EPOCH` procedure

All earnings will transfer at the end of epoch by this procedure.

The user can make the only one action regarding transferring the NFT. For example, the user listed the NFT in Market using listInMarket procedure, he can not use the other procedures like transfer, listInExchange, makeOffer, createTraditionalAuction regarding the transferring the NFT.

If he want to do other action regarding trasferring the NFT, he need to cancel the made action.

Fee

```constexpr uint32 QBAY_FEE_COLLECTION_CREATE_201_1000 = 200;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_1001_2000 = 400;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_2001_3000 = 600;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_3001_4000 = 800;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_4001_5000 = 1000;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_5001_6000 = 1200;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_6001_7000 = 1400;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_7001_8000 = 1600;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_8001_9000 = 1800;
constexpr uint32 QBAY_FEE_COLLECTION_CREATE_9001_10000 = 2000;
constexpr uint32 QBAY_FEE_NFT_SALE_MARKET = 20;
constexpr uint32 QBAY_FEE_NFT_SALE_SHAREHOLDERS = 10;```

The shareHolders fee will be calculated for only $Qubic payment. There is no shareHolders fee in payment for $CFB.

Query functions

```REGISTER_USER_FUNCTION(getInfoOfNFTUserPossessed, 2);
REGISTER_USER_FUNCTION(getInfoOfMarketplace, 3);
REGISTER_USER_FUNCTION(getInfoOfCollectionByCreator, 4);
REGISTER_USER_FUNCTION(getInfoOfCollectionById, 5);
REGISTER_USER_FUNCTION(getIncomingAuctions, 6);
REGISTER_USER_FUNCTION(getInfoOfNFTById, 7);
REGISTER_USER_FUNCTION(getUserCreatedCollection, 8);
REGISTER_USER_FUNCTION(getUserCreatedNFT , 9);```

These query functions required for frontend.

```REGISTER_USER_FUNCTION(getInfoOfNFTUserPossessed, 2);
REGISTER_USER_FUNCTION(getInfoOfMarketplace, 3);
REGISTER_USER_FUNCTION(getInfoOfCollectionByCreator, 4);
REGISTER_USER_FUNCTION(getInfoOfCollectionById, 5);
REGISTER_USER_FUNCTION(getIncomingAuctions, 6);
REGISTER_USER_FUNCTION(getInfoOfNFTById, 7);
REGISTER_USER_FUNCTION(getUserCreatedCollection, 8);
REGISTER_USER_FUNCTION(getUserCreatedNFT , 9);```

These query functions required for frontend.

All procedures and functions was tested by qubic-cli and google test. also the frontend was integrated in SC.

**Future improvements**

Integration with a mobile wallet: as the platform grows we will also integrate the Marketplace with the mobile wallet, this way we will allow users to mint/buy/sell NFTs from a mobile phone or tablet.

We will also continue to invest in and improve the Marketplace. It remains clear, in fact, that the one currently developed is an MVP version of the Marketplace, since, as is known, the costs to develop a full Marketplace is very expensive.

**Tech Stack**

**Frontend** 

- React

- Typescript

- Vite

- Qubic connect (metamask snap, walletconnect and ledger)

**Backend**

- Node.js

- Typescript

- REST API

**Database**

- PostgreSQL

**Smart Contract Infrastructure**

- AWS or Heroku

**Team**

- Pepito: Project leader and $CFB ideator 

- Poly: Smart Contract developer 

- Serendipity: Frontend and Backend developer 

**Conclusion**

We believe that an NFT Marketplace is necessary to bridge the gap between Qubic, understood as an ecosystem, and the most famous and established blockchains. NFTs have the ability to attract that segment of more casual users, i.e. that user necessary to become mainstream. Furthermore, NFTs would also and above all pave the way for artists who would be pushed to create on an emerging ecosystem, creating new life and new possibilities for future developments. This is the opportunity to show to the crypto space the potential of our ecosystem!

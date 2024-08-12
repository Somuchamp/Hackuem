
Auction Marketplace Module
This module provides a basic implementation of an auction marketplace on the Aptos blockchain. The marketplace allows users to list their NFTs for auction, place bids, and claim either the NFT or the bid amounts once the auction ends. The module uses various Aptos Framework components such as coins, tokens, tables, and events.

Features
Initialize Auction: Sets up the necessary data structures for auction management.
Sell NFT: Allows a user to list an NFT for auction with a specified price and duration.
Bid on NFT: Users can place bids on NFTs that are currently on auction.
Claim Token: The winning bidder can claim the NFT after the auction ends.
Claim Coins: The seller can claim the locked coins after the auction ends.
Module Structure
Constants
MODULE_ADMIN: The address that administers the module.
INVALID_ADMIN_ADDR: Error code for invalid admin address.
Data Structures
AuctionItem:

Holds details about each auction including the seller, starting price, duration, current bid, current highest bidder, and the token being auctioned.
AuctionData:

Stores all auction items and associated events.
CoinEscrow:

Handles the escrow for coins during the bidding process.
AuctionEvent:

Event emitted when an auction is initialized.
BidEvent:

Event emitted when a new bid is placed.
ClaimTokenEvent:

Event emitted when a token is claimed by the highest bidder.
Functions
initialize_auction(admin: &signer)

Initializes the auction marketplace by setting up the required global storage.
Only callable by the MODULE_ADMIN.
sell_nft(seller: &signer, creator: address, collection_name: vector<u8>, name: vector<u8>, sell_price: u64, duration: u64)

Allows a user to list an NFT for auction by specifying the sell price and duration.
Withdraws the NFT from the seller and locks it in the contract until the auction ends.
bid(bidder: &signer, creator: address, collection_name: vector<u8>, name: vector<u8>, bid: u64)

Places a bid on an active auction.
The current highest bid is locked in escrow until a higher bid is placed or the auction ends.
claim_token(higher: &signer, creator: address, collection_name: vector<u8>, name: vector<u8>)

The winning bidder can claim the NFT after the auction has ended.
claim_coins(seller: &signer, creator: address, collection_name: vector<u8>, name: vector<u8>)

The seller can claim the locked bid amount after the auction has ended.
is_auction_active(start_time: u64, duration: u64): bool

Checks if an auction is still active.
is_auction_complete(start_time: u64, duration: u64): bool

Checks if an auction has completed.
Testing
A test-only function is provided:

isLockedToken(tokenId: TokenId): bool
Checks if a given token is locked in the auction.
Usage
Deploy the module: Deploy the module to the Aptos blockchain.
Initialize the auction: Call initialize_auction to set up the required structures.
List NFTs: Use sell_nft to list your NFTs for auction.
Bid on NFTs: Place bids using the bid function.
Claim Tokens or Coins: After the auction ends, the winning bidder can use claim_token, and the seller can use claim_coins.
Error Codes
1: Generic error code used for various assertions, such as invalid bidding amount, unauthorized actions, or invalid token claims.
Events
AuctionEvent: Triggered when a new auction is created.
BidEvent: Triggered whenever a bid is placed.
ClaimTokenEvent: Triggered when the highest bidder claims the NFT.
License
This project is licensed under the MIT License - see the LICENSE file for details.
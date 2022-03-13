# Tips

## Transfers

For users, it is more gas optimal to transfer bulk minted tokens in ascending token ID order.

For example, if you have have bulk minted token IDs (33, 34, ..., 99),  
you should transfer in the order (33, 34, ..., 99).

The is due to how the lazy-initialization mechanism works initernally:  
it scans uninitialized slots in descending order until it finds an initialized slot.

## Popularity

The more popular your NFT collection, the larger the expected savings in transaction fees.

See [Design: Lower Fees](design.md#lower-fees).

## Aux

Consider using [`ERC721A._getAux`](erc721a.md#_getAux) and 
[`ERC721A._setAux`](erc721a.md#_setAux) to get / set per-address variables  
(e.g. number of whitelist mints per address).

This can help remove an extra cold `SLOAD` and `SSTORE` operation.

## Minting

For typical artwork collections, consider using `_mint` over `_safeMint` if you don't expect users to mint to contracts.

## Batch Size

To prevent overly expensive transfer fees for tokens that are minted in large batches.

- Restrict the max batch size for public mints to a reasonable number.

- Break up excessively large batches into mini batches internally when minting. 

- Look into [`ERC721AOwnersExplicit`](erc271a-owners-explicit.md). 

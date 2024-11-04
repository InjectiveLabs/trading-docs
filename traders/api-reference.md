# API Reference

## Rate Limits

The public mainnet and testnet nodes have a request rate limit associated to the requester IP address. The limits are:

* 20 requests/second for the "chain" group
* 50 requests/second for the "indexer" group

Each endpoint's section in this document clarifies which group the endpoint belongs to. When the limit is reached the server will respond sending an error response with code 429.

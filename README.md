# AVAX-Explorer API Documentation: Token Transfer and Blockchain Interaction

The AVAX-Explorer API provides developers with the tools to interact programmatically with the Avalanche (AVAX) blockchain. It enables users to perform common blockchain operations such as token transfers, wallet management, querying block data, and monitoring network status.

This documentation outlines the key API endpoints and provides code examples for each use case, helping you integrate AVAX functionality into your decentralized applications (dApps) or other blockchain-related projects.

https://medium.com/@elliotpearce01/using-the-avalanche-api-for-development-with-avax-explorer-gateway-api-e56de9b2fc04

## Account Management

The Account Management API allows you to create wallets, manage keys, and recover accounts using a mnemonic phrase. This section covers how to generate a new keypair and how to create an account from a mnemonic phrase.
Create Keypair

This endpoint generates a new wallet with a private and public key. These keys are returned in base58 format.
Request

GET https://avax-explorer.co/api/create/keypair

Response

{
  "private_key": "5JrYt7WkXYiXb3AkZGzjpP7zy8Tt9Kf1cv...",
  "public_key": "WkXYiXb3AkZGzjpP7zy8Tt9Kf1cv..."
}

You can use these keys to interact with the Avalanche network, including signing transactions and transferring AVAX tokens.

## Create Account by Mnemonic

If you already have a mnemonic phrase (a list of words used to generate a wallet), you can use this endpoint to create or restore an account.
Request

POST https://avax-explorer.co/api/create/account/by_mnemonic

Payload

{
  "mnemonic": "apple banana orange grape ...",
  "account_name": "MyAVAXAccount"
}

Response

{
  "account_address": "X-avax1...",
  "public_key": "PublicKey...",
  "private_key": "5JrYt7WkXYiXb3AkZGzjpP7zy8Tt9Kf1cv...."
}

You can use the private_key to sign transactions and manage the wallet, while the account_address is used to receive AVAX tokens.

## Token Operations
### Transfer AVAX

The /api/transfer/avax endpoint allows you to transfer AVAX tokens from one wallet to another. To perform a transfer, you need to provide the sender's private_key, the recipient’s public_address, and the amount of AVAX to send.
Request

POST https://avax-explorer.co/api/transfer/avax

Payload

{
  "private_key": "5JrYt7WkXYiXb3AkZGzjpP7zy8Tt9Kf1cv...",
  "recipient_address": "X-avax1fWk2vC9BfHSJXkH65kxxDYNzZpGv5Jb9U...",
  "amount": 10.5
}

Response

{
  "status": "success",
  "transaction_id": "2G5s1...",
  "blockchain": "Avalanche"
}

    private_key: The sender’s private key (base58 format).
    recipient_address: The public address of the recipient.
    amount: The amount of AVAX to transfer.

After calling this endpoint, you will receive a transaction_id which can be used to track the status of the transfer on the blockchain.

## Transactions

The Transactions API allows you to submit custom transactions to the Avalanche network. This can be used to send AVAX or interact with smart contracts.

### Submit a Transaction

This endpoint submits a transaction to the Avalanche network. You must include the sender's private_key and the transaction_data.
Request

POST https://avax-explorer.co/api/transactions
Payload

{
  "private_key": "5JrYt7WkXYiXb3AkZGzjpP7zy8Tt9Kf1cv...",
  "transaction_data": {
    "amount": 10.5,
    "recipient": "X-avax1fWk2vC9BfHSJXkH65kxxDYNzZpGv5Jb9U..."
  }
}

Response

{
  "status": "success",
  "transaction_id": "2G5s1..."
}

The transaction_data typically contains the amount and recipient address, but it can vary depending on the type of transaction.

### Blockchain Data

AVAX-Explorer offers several endpoints to retrieve information about the blockchain and specific blocks. This is useful for tracking block confirmations, understanding the state of the chain, and analyzing transaction data.
Get Block Information

This endpoint retrieves information about a specific block on the Avalanche blockchain.

Request

GET https://avax-explorer.co/api/blocks/{block_id}

Response

{
  "block_id": 1000001,
  "block_data": "Block data",
  "timestamp": "2024-11-26T12:00:00Z"
}

    block_id: The ID of the block you wish to retrieve.
    block_data: General information about the block.
    timestamp: The block’s creation timestamp.

## Get Latest Ledger Data

This endpoint retrieves information about the latest block and ledger state on the Avalanche network.
Request

GET https://avax-explorer.co/api/blockchain/ledger

Response

{
  "latest_block": "1000001",
  "timestamp": "2024-11-26T12:00:00Z"
}

This response includes the latest_block and timestamp, indicating the most recent block on the blockchain.

## Network Information

You can monitor the status and health of the Avalanche network using the Network Information endpoint.
Get Network Status

This endpoint provides details about the current state of the Avalanche network, including peer count and uptime.
Request

GET https://avax-explorer.co/api/network/info

Response

{
  "network_status": "healthy",
  "peer_count": 25,
  "uptime": "99.9%"
}

    network_status: Indicates the health of the network (e.g., "healthy").
    peer_count: The number of peers connected to the network.
    uptime: The percentage of time the network has been operational.

## Conclusion

The AVAX-Explorer API offers a comprehensive suite of endpoints for interacting with the Avalanche blockchain. Whether you're transferring AVAX tokens, querying blockchain data, or managing accounts, the API provides the necessary tools to build decentralized applications on the Avalanche network.

Here is a summary of the core features covered in this documentation:

    Account Management: Generate wallets, restore accounts from mnemonic phrases, and manage keys.
    Token Operations: Transfer AVAX tokens between wallets securely using private keys.
    Transactions: Submit custom transactions to the Avalanche network.
    Blockchain Data: Query information about specific blocks and the latest ledger state.
    Network Information: Monitor the health and status of the Avalanche network.

By following this documentation, you can integrate AVAX-related functionalities into your application, whether it’s for financial transactions, data tracking, or interacting with the Avalanche blockchain. Always ensure that sensitive data, such as private keys, is handled securely to protect user assets.

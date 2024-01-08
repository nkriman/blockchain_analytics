# Blockchain Data Model

As a data scientist exploring blockchain, it's crucial to understand its fundamental data model. The blockchain data model forms the backbone of its security. Let's dive into the specifics of this model.

## Core Components of the Blockchain Data Model

### Blocks
- **Purpose**: Serve as the primary storage units in a blockchain.
- **Key Elements**:
  - `Id`: A unique identifier (BIGINT) for each block.
  - `Hash`: A unique cryptographic hash (BINARY(32)) for each block.
  - `Time`: Timestamp (BIGINT) indicating when the block was created.

### Transactions
- **Purpose**: Record all individual transactions within a block.
- **Key Elements**:
  - `Id`: Unique identifier (BIGINT) for each transaction.
  - `Hash`: Unique cryptographic hash (BINARY(32)) for each transaction.
  - `blockID`: Foreign key (BIGINT) linking the transaction to its block.

### Outputs
- **Purpose**: Represent the outcomes of transactions, like cryptocurrency transfers.
- **Key Elements**:
  - `Id`: Unique identifier (BIGINT) for each output.
  - `dstAddress`: Destination address (CHAR(36)) for the output.
  - `Value`: Cryptocurrency value/amount (BIGINT) transferred.
  - `txID`: Foreign key (BIGINT) linking the output to its transaction.
  - `Offset`: Sequence number (INT) of the output in the transaction.

### Inputs
- **Purpose**: Specify the sources for the funds in transactions.
- **Key Elements**:
  - `Id`: Unique identifier (BIGINT) for each input.
  - `outputID`: Foreign key (BIGINT) referencing the previous output used in the transaction.
  - `txID`: Foreign key (BIGINT) linking the input to its transaction.
  - `Offset`: Sequence number (INT) of the input in the transaction.

## Relational Model

In this relational model, `Blocks` serve as the fundamental entities containing `Transactions`, which in turn consist of `Inputs` and `Outputs`. 


```mermaid

erDiagram
    Blocks ||--o{ Transactions : "contains"
    Transactions ||--o{ Outputs : "has"
    Transactions ||--o{ Inputs : "uses"

    Blocks {
        BIGINT Id "Unique identifier of a block"
        BINARY(32) Hash "Unique hash identifier of a block"
        BIGINT Time "Block’s timestamp (Unix epoch)"
    }

    Transactions {
        BIGINT Id "Unique identifier of a transaction"
        BINARY(32) Hash "Unique hash identifier of a transaction"
        BIGINT blockID "Foreign key to Blocks"
    }

    Outputs {
        BIGINT Id "Unique identifier of an output"
        CHAR(36) dstAddress "Output’s destination address"
        BIGINT Value "Output’s cryptocurrency value/amount"
        BIGINT txID "Foreign key to Transactions"
        INT Offset "Incremental sequence number of the output"
    }

    Inputs {
        BIGINT Id "Unique identifier of an input"
        BIGINT outputID "Foreign key to Outputs"
        BIGINT txID "Foreign key to Transactions"
        INT Offset "Incremental sequence number of the input"
    }

```

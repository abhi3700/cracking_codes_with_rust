# Merkle Tree

Merkle trees are a way to verify the integrity of data which means if you have a small/medium/large datasets & want to form a group. Now, in order to prove if a data element is a part of the group, then you can use Merkle tree to verify it.

Merkle trees are used in blockchains to verify if a transaction is a part of a block or not. It is also used in IPFS to verify if a file is a part of a directory or not.

```mermaid
flowchart LR
    A[Block 1] --> B[Block 2]
    B --> C[Block 3]

    subgraph B[Block 2]
        direction BT
        D[Tx-1] -->|Hash| E[Merkle Root]
        F[Tx-2] -->|Hash| E
        G[Tx-3] -->|Hash| E
        H[Tx-4] -->|Hash| E
    end
```

Each block contains merkle root irrespective of transactions. The merkle root is calculated by hashing the hashes of all transactions in the block. This merkle root is then used to verify if a transaction is a part of the block or not.

Ethereum uses Patricia Merkle tree to store the state of the blockchain. It is a modified version of Merkle tree.

> For any immutable data (i.e. no change required) like txs added in blocks, standard merkle tree is enough. But, for mutable data (i.e. change required) like state of blockchain, Patricia merkle tree is used as it also stores the changelog of the data.

## Tree formation

### Even leaves

```mermaid
graph TD;
    A[Merkle Root] --> B[Hash AB]
    A --> C[Hash CD]
    B --> D[Hash A]
    B --> E[Hash B]
    C --> F[Hash C]
    C --> G[Hash D]
    D --> H[Tx A]
    E --> I[Tx B]
    F --> J[Tx C]
    G --> K[Tx D]
    style A fill:#f9d,stroke:#333,stroke-width:2px
```

### Odd leaves

```mermaid
graph TD;
    A[Merkle Root] --> B[Hash ABCD]
    A --> C[Hash EE]
    B --> D[Hash AB]
    B --> E[Hash CD]
    C --> F[Hash E]
    C --> G[Hash E]
    D --> H[Hash A]
    D --> I[Hash B]
    E --> J[Hash C]
    E --> K[Hash D]
    F --> L[Tx E]
    G --> M[Tx E]
    H --> N[Tx A]
    I --> O[Tx B]
    J --> P[Tx C]
    K --> Q[Tx D]

    style A fill:#f9d,stroke:#333,stroke-width:2px
```

## Proof

### Single

This is about proving if a transaction is a part of a block or not. So, here the transaction is the leaf node & block has a merkle root field.

#### Even leaves

```mermaid
graph TD;
    A[Merkle Root] --> B[Hash AB]
    A --> C[Hash CD]
    B --> D[Hash A]
    B --> E[Hash B]
    C --> F[Hash C]
    C --> G[Hash D]
    D --> H[Tx A]
    E --> I[Tx B]
    F --> J[Tx C]
    G --> K[Tx D]
    style A fill:#f9d,stroke:#333,stroke-width:2px
    style E fill:#fc0,stroke:#333,stroke-width:2px
    style C fill:#fc0,stroke:#333,stroke-width:2px
    style H fill:#0f0,stroke:#333,stroke-width:2px
```

#### Odd leaves

```mermaid
graph TD;
    A[Merkle Root] --> B[Hash ABCD]
    A --> C[Hash EE]
    B --> D[Hash AB]
    B --> E[Hash CD]
    C --> F[Hash E]
    C --> G[Hash E]
    D --> H[Hash A]
    D --> I[Hash B]
    E --> J[Hash C]
    E --> K[Hash D]
    F --> L[Tx E]
    G --> M[Tx E]
    H --> N[Tx A]
    I --> O[Tx B]
    J --> P[Tx C]
    K --> Q[Tx D]

    style A fill:#f9d,stroke:#333,stroke-width:2px
    style C fill:#fc0,stroke:#333,stroke-width:2px
    style E fill:#fc0,stroke:#333,stroke-width:2px
    style I fill:#fc0,stroke:#333,stroke-width:2px
    style N fill:#0f0,stroke:#333,stroke-width:2px
```

### Multiple

Verifying multiple txs in a block. So, the proof size would be lesser in size than that of single tx proof.

# Learning TON

Notes on the TON (The Open Network) blockchain and smart contract development.

## Resources

- https://docs.ton.org/start-here
- https://ton.org/en/mini-apps

## TON

- Users
- Validators
- Developers

### Built on Blockchains (Smart Contracts)

- DApps, DEXs
- Tokens
  - currencies
  - collectibles
  - utility tokens
- Auctions
- Domain names

### Complex Apps

- Main contracts
- Satellite contracts

## TON Blockchain

- Ledger of state transitions
- Contracts are isolated
- Contracts can be async
  - get contract state through messages
- No guarantee how long a message will take, but a guarantee that the message will be delivered
- Focus on contract consistency and possible scenarios
- TON validators/sharding
  - can be infinitely sharded
  - recorded in the masterchain

### Messages vs Transactions

- A **message** is between two contracts, and carries coins and arbitrary data to a contract address
- A **transaction** is contract activity:
  - running contract code
  - updating contract state
  - emitting new messages
- Preventing double spend
  - Proof of Stake, consensus of validators

### Accounts

- own storage
- unique address
- balance of Toncoins
- program code

### Contracts

- change data/code of the contract
- transfer coins
- send messages to other contracts

### Limitations

- Contracts have no visibility into anything outside themselves: isolated, infinitely scalable.

### Blockchain Guarantees

- Verify the address of incoming messages
- Guarantee delivery of messages

## TON vs BTC/ETH

### Bitcoin

- 1st crypto/blockchain
- Censorship-resistant digital cash transfers
- Multiple input/output transactions
- Verified by PoW consensus
- Securing transactions with Bitcoin's scripting language

### Ethereum

- Code
- Internal storage
- Account state transitions
- Developer-friendly, but has scalability issues

### TON

- Individual accounts
- Accounts can't see global state, only local state
- Contracts can be sharded, and they communicate via messages
- Infinite developer flexibility
- Infinite scalability
- The model is hard to understand

## Accounts/Contracts

- address = hash of the initial state
- contracts can only communicate changes via messages
- User account: wallet contract
  - parses signatures
  - routes to other contracts
- Multi-signature contract
  - multiple users
  - verifies users' right to change state
- Tokens:
  - state
  - attributes
  - ownership
- Fees
  - gas cost
  - rent
  - message routing fees
- Frozen contracts
  - Contracts running out of tokens will be frozen; data will be stored as a cryptographic hash of the state
  - Reinstating/unfreezing a contract requires a snapshot of the data that matches the hash

## Tokens

- custom assets
- tokenization = breaking down value into chunks
- token transfers are scalable and don't interfere with each other
- fungible / non-fungible

## TVM and Memory Layout

### Cell

- the building block; all data structures are built on top of cells
- Each cell has
  - up to 1023 bits of data and
  - up to four references to other cells
- Stored in a bag of cells
  - effectively compresses all individual objects into one repository
- Can create a Merkle proof of any portion of data in the blockchain, at any state

### TON Virtual Machine

- Receives an incoming message
- TVM runs with:
  - the current state of the contract
  - the current code
- Outputs an error code or a new state

### Memory Layout

- HashMap: tree/prefix tree
  - logarithmic cost of accessing your data
- Unpacking cells is expensive
  - jumping from one cell to another
- Don't store a lot in one place
- Only store small amounts of data
- Millions of users?
  - use tokens for participation instead of storing a list of users
- Cells have a built-in deterministic hashing scheme
  - can identify cells uniquely
- Expensive:
  - large data structures
  - deep chains of cells

## Message Types and Computation Phases

### Incoming Messages

- **External**
  - any arbitrary data
- **Internal**
  - can carry any amount of coins from another contract
  - securely authenticated by the address of the sending contract
- Opcodes

### Transactions

- changes to the state of the contract
- the message is only the input
- the transaction creates a new state and a list of outgoing actions

### 5 Phases of Transactions

1. **Storage phase**: charge rent before transaction execution begins
2. **Credit phase**: coins attached to internal messages are credited to the contract
3. **Computation phase**: TVM executes code, verifies the operation, tracks gas usage, and generates output actions
4. **Action phase**: process actions and update contract state
   - the new state of the contract is recorded
   - outgoing messages are routed to other contracts
5. **Bounce phase**: if the contract failed, remaining funds are sent back to the sender
   - rollback, if the incoming message has the bounceable flag

Always keep some amount of coins in the balance.

## Authorization of Messages in Contracts

### Signature for External Messages

- stores TON coin balance
- stores public key
- checks the 64 bits of the signature

### Message Sender for Internal Messages

- internal message authentication
- compare the message sender with a stored address

### DNA Check for Trusted Code

- contracts have the same code
- double-check data is correct by executing the code

### Lack of Authentication for Censorship Resistance

- lack of censorship
- quick

## Transaction Fees

- Calculation is expensive

### Model of Transaction Cost and Fees

- Gas cost
- Rent
- Message fees

### Gas Cost

- operations have a nominal gas cost
- gas price is a global parameter
  - the price of gas depends on the load of the blockchain
- gas quantity × gas price
- who pays for the gas?
  - put the gas cost on the sender, make gas cost predictable

### Rent

- the cost of a single bit of data that the contract stores per unit of time
- rent = (current time - previous transaction time) × size of storage

### Message Fees

- importing and creating outgoing messages, per byte

### Pitfalls

- Don't let the contract run out of gas limit and balance

### Make Sure the Contract Exists and Doesn't Run Out of Gas/Rent

- anyone can send TON coins to any contract to refill its balance
- Contracts should not run out of gas and rent.
- If you put the cost of gas and execution on the sender, you may not always be able to guarantee a specific cost of execution, but you can guarantee an upper bound.
- Strive to design contracts with constant cost in terms of storage and computation, so rent and gas costs are more predictable.

## Scalable Contracts

- TON can scale down to the granularity of individual contracts
- Take advantage of the entire scalability of the blockchain
- Don't create bottlenecks in your own contracts

### Problems

- growing cost of rent
- users pay larger and larger transaction fees

### Guidelines for Scalable and Affordable Contracts

Contracts with constant storage and constant operating costs:

1. Avoid variable-length data.
2. Keep data lists short and bounded.
3. Make sure a contract with big dynamic data is owned by a single user.
   - DNS
   - list of plugins in a wallet
4. For large lists or dictionaries, scale using:
   - the blockchain itself as an array
   - an individual contract instance for each user (the user is the owner)

### Classic Business Problems

- Tokens in other blockchains don't scale well

## Smart Contract Dev Lifecycle

- A TON smart contract is like a satellite
  - Local setup
  - TL-B scheme
  - Local tests
    - TypeScript for local tests
  - Testnet and after-deploy on-chain tests
  - Mainnet production deployment
- Smart contract code
  - FunC → Fift → Bytecode

### FunC

- `impure` specifier
  - function affects state

### dApps

- Backend = smart contracts
- Frontend = client-side and open-source

## Smart Contract Security

### Smart Contract Entry Points

- `recv_internal`
- `recv_external`
- `run_ticktock`

### Recommendations

- Only have `recv_internal`
- TON requires much more design effort from the developer to avoid "unbounded data structures" and to allow the "infinite sharding paradigm".
- Even with the correct design and the "carry-value pattern", TON developers have to take into account the async nature of TON messages.
- Accepting Jettons requires careful manual payload analysis and condition checking.
- Return value via `sender_address`, since messages can be forged.
- TON requires deliberate effort from developers to manage gas: calculate the spending and check if enough was provided.
- Gas cost can rise over time if "unbounded data structures" are used.
- TON recommends returning excesses to the sender, which is also on the developer.
- If gas runs out, the transaction will be partially executed. That can be a critical issue.

# Roadmap

This file is a non-enforced informative document, detailing concrete goals of the Citizen platform.

## Initial Development stages

1. **Virtual computer milestone.**
  - Virtual computer
    - Dependently typed for proof verification
    - Can execute code written in a high level language
    - Can be compiled to succinct binary format
    - Modular, versioned libraries
    - Global state with hashable diff
    - Fair, standard costing of execution spacetime


2. **Blockchain milestone.** In any order:  
  - Node
    - Can find peers from seed list on the web, then bootstrap a complete list
    - Can rebroadcast new well-formed blocks, pull old blocks
    - Can broadcast/rebroadcast well-formed transactions, maintain transaction pool
  - Blockchain
    - Can verify blocks
    - Can create transactions
  - Blockmaker
    - Can create new blocks from transaction pool when triggered
  - Portfolio
    - Can create new addresses, maintain list of addresses
  - Virtual computer
    - Can create, patch contracts in global context


3. **Self-hosting milestone.** In any order:
  - Portfolio
    - Transactional secrecy through crypto
    - UI for contract creation and interaction (messaging?)
    - Local encryption with password
    - One agent is created per node
    - Create prime agent with all privileges
    - [For discussion] Global contract context could be pushed to github from here. Should it be?
  - Upgrader
    - Introduce virtual computer IO primitive "Update", with corresponding transaction. Only accessible by a named contract
    - Prime agent creates genesis block, containing resource reference to codebase
    - Create Upgrade contract
      - "Update" only callable by prime agent
      - "Patch" callable by whitelist of agents
      - "Manage Whitelist" only callable by prime agent
    - Endow Upgrader with code replacement ability, genesis block must perform identity update on existing code.
    - Integrate Upgrader with Github, Travis, etc. Ensure the codebase will always be publicly available.
  - Resource manager
    - Introduce IO primitives "Request resource" and "Return resource"
    - Allocate CPU and disk space, within user specified limits, according to Request message.
    - Create Reed-Solomon shards and maintain file-shard mapping


4. **Community milestone.** In any order:
  - Curatables contract (protocol)
    - Contracts extending Curatables have the following data:
      - List of agents, seeded with prime agent
      - Set of actions
      - Stream of actions per agent
      - State for targeting by actions (forum)
      - Set of roles applicable to agents
      - Set of requirements per role (for evaluation of agents wrt forum)
    - Unifies all data collected by curatable contracts per agent, along with access authority
    - "Extends itself" to manage self patches (Meta forum), development of analysis methodologies that can securely target data aggregated over all agents
    - Extends Tradeables, with issuance based on status of requirements per agent
    - Patch Upgrader to extend Curatable (Dev forum), with Managing and Contributing roles, Patch action, tradeable royalty payment for use (final decision by Dev forum consensus)
    - Introduce IO primitive "Make Block", wrap blockmaker in Curatable Blockmaker contract. For housing proof of work, stake, etc authority as resource requirements
    - Wrap resource manager in Curatable Resource contract, which administers challenge/response hashing, and peer rewards/punishments
  - Tradeables contract (protocol)
    - Contracts extending Tradeables have the following data:
      - List of agents, seeded with prime agent
      - Token balance per agent
    - Extends Curatables (Economic forum), with Policymaker and Trader roles. Tradeable tokens may opt to be managed through policy actions when initialised
    - Patch Upgrader to extend Tradeable, issuance mechanism defined by Dev forum, supply managed by Economic forum
    - Wrap blockmaker in Tradeable Blockmaker contract, managed by Economic forum.
    - Wrap resource manager in Tradeable Resource contract, managed by Economic forum.
  - Bazaar contract, provides market-clearing service.
  - Unit, a Tradeable contract. All tradeables with a market must deal in Units. Supply managed by Economic forum
  - Prelude contract (library), which provides well-known datatypes etc.
  - Portfolio
    - Move VC language (katsuo) binary compiler here
    - Wrap in a resourceful contract, for housing plugins such as alternative contract languages
    - Simple, standard UI for direct interaction with contracts through portfolio
  - Web server
    - Publish data and provide interactive UI for the minimal node
    - Publish download link
    - Publish documentation
    - PR surface - news, press releases, opinion columns, discussion forum/memes (rehost reddit?), tutorials, etc
    - Provide hosting, domain name management, etc as resource requests

At this point it should be possible to manage the development of the project entirely within the project itself through the forums, especially the Dev, Meta and Economic forums. Milestones from this point on apply to the effective development of the community and growth goals.

## Early Growth stages

### Rough notes

- Handing over final Update authority to the consensus process
- Formulating clear economic policy in relation to other cryptocurrencies/national currencies.
- Formulating clear, transparent steering policy based on game theoretic analysis
- Fostering local initiatives

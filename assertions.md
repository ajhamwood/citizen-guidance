# Assertions Master Document

## 0. Preamble

### 0.0 General statements

* **0.0.1** This is a human-interpreted, normative, informal document which contains POTENTIALLY FAILING ASSERTIONS about the Citizen project, in the style of a unit test suite. Contributors with standing shall determine if assertions become PASSING ASSERTIONS according to the consensus process outlined in section 1. Let the spirit of the document as a whole guide contributions, and to the greatest extent possible avoid legalistic interpretation of the clauses herein. Also, this writing style is absolutely an affectation so don't feel as though you have to follow it.
* **0.0.2** The documents contained in this repository (that is, the one currently viewable at https://github.com/ajhamwood/citizen-guidance) have no legal force in any jurisdiction, other than that expressed by any applicable copyright notices.
* **0.0.3** This preamble shall consist of pre-assertions which cannot be considered passing or failing, but ought to guide the writing of all and any assertions.
* **0.0.4** Changes to the preamble or editing rules by anyone other than **@ajhamwood** shall be introduced as an clause which effectively describes the amendment, to be included under the "Pending non-assertion amendments" section. The introducing person or persons must indicate their Github user name(s) along with each clause. Support or rejection can be expressed with a +1 or -1 respectively and your Github user name below the clause, and is non-binding. Whether it is applied or not is up to **@ajhamwood** alone (subject to change in the future).
* **0.0.5** New clauses or subsections in the amendments section can only be added by **@ajhamwood** (also subject to change in the future).
* **0.0.6** Assertions shall be expressed as copulative (a *is* b) statements, with the option of including informative statements according to taste.

### 0.1 Principle of primacy of people over content

* This project should operate under the principle that the specific content which is produced exists entirely thanks to the efforts of many individuals. In recognition of this, human activity which contributes to the project shall be explicitly treated as the fundamental building block of the platform as a whole.

### 0.2 Principle of greatest development

* This project should strive to touch as many lives as it can, and at each opportunity make the best possible effort to enable stakeholders to develop themselves.

## 1. Rules governing the editing of this document

### 1.0 Method to establish consensus for assertions

* **1.0.1** To express judgement that an assertion is PASSING, just cosign it with a +1 and your Github user name underneath the indicated clause, thanks. Please try to not mess up the formatting. Amendments to assertions are assertions, too.
* **1.0.2** Consensus is reached when 90% of users with standing have cosigned the clause.
* **1.0.3** An amendment to an assertion can replace the active assertion if it reaches 90% support. If that happens, the active assertion shall be moved below to become an amendment, without requiring indication of authorship, and both clauses shall lose all consensus information.

### 1.1 Method to propose amendments to assertions

* **1.1.1** Include the rewritten assertion below the clause it is to replace, or if there is a section expressing support for or rejection of the clause, below that. Include your Github user name immediately after the amendment, preferably on the same line.
* **1.1.2** The amendment shall have substantial unique content and consist of a functional replacement to the indicated assertion, or may be deleted at will by **@ajhamwood**.
* **1.1.3** To express judgement that an amendment should replace the active assertion, edit in a +1 along with your Github user name under the clause.
* **1.1.4** To indicate rejection of an assertion, edit in a -1 along with your Github user name under the support section. Expressions of rejection for an assertion are non-binding, but if they numerically exceed expressions of support, the clause may be deleted at will by **@ajhamwood**.

### 1.2 List of users with standing in regard to this document

* **1.2.1** Only those Github user names contained in the following list have standing:  
**@ajhamwood**  
**@kendricktan**
* **1.2.2** Actions taken using a Github account are assumed to express the intention of the person who owns the account.

## 2. Pending non-assertion amendments

No pending amendments.

## 3. Assertions

### 3.0 General properties of the Citizen platform

* **3.0.1** While the Citizen project remains non-self-hosted, the master repository is available at https://github.com/ajhamwood/citizen .

* **3.0.2** The Citizen platform consists conceptually of at least the following subsystems:  
**3.0.2a** The **Upgrader**;  
**3.0.2b** The **Virtual Computer**;  
**3.0.2c** The **Blockchain**;  
**3.0.2d** The **Blockmaker**;  
**3.0.2e** The **Node**;  
**3.0.2f** The **Portfolio**;  
**3.0.2g** The **Resource Manager**; and,  
**3.0.2h** The **Web Server**.

* **3.0.3** The codebase *fulfils equivalent purposes* in at least the following modes:  
**3.0.3a** A **Minimal** node, designed for access by the greatest number of people possible. In this mode it is deployed as a web application.  
**3.0.3b** A **General Purpose** node, designed to be run on a PC. In this mode the method of deployment is not indicated. Golang? Rust? Haskell?  
**3.0.3c** A **Full** node, designed to make use of locally available resources of indefinite scale and nature. Also without indicated method of deployment.

* **3.0.4** The virtual computing environment is initially loaded with at least *some* of the following general purpose "sponsored" contracts:  
**3.0.4a** "**Prelude**", a standard library.  
**3.0.4b** "**Curatable**", which provides a minimal consensus system. Participating users ("curators") are evaluated on the persuasiveness of their arguments, and are paid a tradeable token measured in man-hours (?) for each curation context ("forum").  
**3.0.4c** "**Tradeable**", which provides a minimal market-making system. Users may participate as a "trader" to deal in specialised tokens (eg. reward for hosting a node?), or as a "policymaker" to manage the health of tradeables markets in a curated economic forum.  
**3.0.4d** "**Unit**", a tradeable metacoin managed by the economic forum.  
**3.0.4e** "**Bazaar**", an automated market-clearing service. Allows tradeables to be sold in baskets, with counter-offers.  
**3.0.4f** "**Escrow**", a curated market for refundable payments in Units, with optional attachment of off-chain evidential data (eg. passport photo?).  
**3.0.4g** "**Upgrade**", the maintainer forum (only one contract may validly invoke the **Update** operation). Evaluates patches, manages Github, Travis, etc integration.  
**3.0.4h** "**Certify Contract**" ..?, the virtual computer environmental management forum (only one contract may validly invoke the **Activate Contract** operation). (This is a fundamental design decision which needs to be debated thoroughly. Why not introduce a virtual resource cost?)  
**3.0.4i** "**Make Block**", the block making forum (only one contract may validly invoke the **Make Block** operation). "Blocks made" is a tradeable resource, and blocks failed will reduce a user's standing in the forum.  
**3.0.4j** "**Storage**", which provides a market in data warehousing.  
**3.0.4k** "**Compute**", which provides a market in performant computing.  
**3.0.4l** "**Bug Bounty**", which provides a market in failing tests.  
**3.0.4m** "**Disruptor**", which can be requested to act as an adversarial agent, to test contract robustness.  
**3.0.4n** "**Content**", the creatives forum. Create content on the main website.

### 3.1 About the Upgrader

* **3.1.1** The entire Citizen codebase exists as a content-level property of the blockchain.
* **3.1.2** The initial commit is performed functionally by one or more transactions within the genesis block of the blockchain (or some equivalent set of objects and operations).
* **3.1.3** Updates to the codebase are introduced by a special **Update** operation which can only be performed by a single, privileged contract (the Upgrade contract) as the result of some consensus mechanism among members with standing in relation to the codebase. The "Upgrader" updates Citizen's local files according the diff at the storage location provided in the transaction.
* **3.1.4** Updates are compiled from single-issue patches which can be submitted by anyone. Submission is performed by invoking the **Patch** operation. Judgement regarding which patches are accepted into an update, how the patches are merged, the timing of the Update transaction, and the invocation of any related transactions required by Upgrade, are performed through consensus-based transactions contained in Upgrade.
* **3.1.5** The codebase is versioned, and the interaction of Citizen nodes of differing version ought to be managed by each update.
* **3.1.6** Upgrade is created with a genesis block transaction, and is itself an upgradeable contract. However, it must not be able to lose any property required for it to be functionally consensus-based.

### 3.2 About the Virtual Computer

* **3.2.1** The natural content of the Citizen platform is introduced to the blockchain (or any data structure fulfilling an equivalent purpose) by transactions executed in the context of a distributed virtual computer. Before the general features of this component are finalised, contributors are directed to keep an open mind about the design of the computing context, as computation is an extremely general property which is wont to show up in the strangest of situations...

* **3.2.2** We recognise the potential for badly designed smart contracts to wreak havoc on a large scale, so the virtual computer executes programs written in a consistent, dependently typed language, with theorem proving. Smart contract developers are encouraged to publish values inhabiting the Identity type in conjunction with advertising the claimed properties of the contract.

* **3.2.3** The virtual computer state acts as a kind of glue connecting the resources of disparate nodes ("connecting" in the sense of allowing them to be used together in a constructive way). For this reason, the virtual computer is adapted for correctness first, and efficiency second; the representation of state, however, is adapted to the mode of deployment.

* **3.2.4** In addition to language constructs, and a standard set of primitives over all deployment modes, the following list of IO operations are available:  
**3.2.4a** "**Update**" (upgrades the codebase);  
**3.2.4b** "**Patch**" (request a change to the codebase);  
**3.2.4c** "**Send Transaction**" (submits code to the transaction pool..? How should transactions reach the execution context?);  
**3.2.4d** "**Submit Contract**" (submit a contract for curation);  
**3.2.4e** "**Activate Contract**" (dispatch a contract to the global execution context);  
**3.2.4f** "**Make Block**" (publish a block to the network);  
**3.2.4g** "**Create Address**" (initialise an address to the network);  
**3.2.4h** "**Request Resource/Return Resource**" (interface with an off-chain data or compute resource);  
**3.2.4i** "**Register Server Resource**"..? (provide a "storage + compute + bandwidth" resource to serve the official website from). Why should this be separate to 3.2.4h?

* **3.2.5** References to contracts must explicitly include their version when being invoked in a transaction or as a library. Version number is incremented by submitting the number to be incremented when invoking **Submit Contract**.

### 3.3 About the Blockchain

* **3.3.1** Acceptably preserves transactional consistency across the network (ie. functions as a blockchain).
* **3.3.2** Does not burden PC users, is even simply a real thing for web app users.

### 3.4 About the Blockmaker

* **3.4.1** Creates and verifies blocks according to the requirements of 3.3.1.
* **3.4.2** Validates transactions and maintains the transaction pool (if that truly is the best way to manage the execution environment).

### 3.5 About the Node

* **3.5.1** Manages peer connection, maintains list of peers.
* **3.5.2** Pulls/broadcasts peers, blocks, and transactions.
* **3.5.3** Is robust against attack, or at least protects the network from attack.

### 3.6 About the Portfolio

* **3.6.1** Securely stores one-time addresses.
* **3.6.2** Preserves transactional anonymity (ring signature? snark?), and creates valid and correct transactions.
* **3.6.3** Securely stores local data associated with contracts.
* **3.6.4** Requests full-chain verification of the state of older addresses.
* **3.6.5** Houses plugins? Eg. the high-level contract language.

### 3.7 About the Resource Manager

* **3.7.1** Allocates disk and CPU resources according to received, valid requests.
* **3.7.2** Manages creation of Reed-Solomon shards and file-shard mapping.
* **3.7.3** Fulfils challenge/response hashing and broadcasting.
* **3.7.4** Executes and returns jobs.
* **3.7.5** Peer reward/punishment protocol is well balanced.

### 3.8 About the Web Server

* **3.8.1** Extremely strict linting requirements enable served pages to exhibit equivalent behaviour in 99.99% of navigation events. Enforced WACG compliance provides equivalent experience for the greatest possible range of user ablenesses.
* **3.8.2** Provides UI for data regarding: the blockchain, blocks, transactions, addresses, contracts, the codebase, patches, stored files, compute entrypoints, tradeables markets.
* **3.8.3** Provides UI for interactive objects such as: the portfolio, storage contracting, compute contracting, curatables forums.
* **3.8.4** Provides download links to the various editions of the node.
* **3.8.5** Provides a branded "messaging" surface (in the marketing sense) with regular consumable content.

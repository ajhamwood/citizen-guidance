# Citizen 2019 - Notes

This time round, we are writing the VM in Agda.

### Roadmap: Virtual Computer milestone

1. Dependently typed for proof verification: can be done in Agda.
2. Can execute code written in a high level language: can be done, with practise.
3. Can be compiled to a succint binary format: => look into Treeless mode, write my own (Haskell).
4. Modular, versioned libraries: =>
    * The point here is that contracts can be loaded into and executed in the blockmaker environment quickly.  
      => compile at author's expense (using compute network), run at network's expense (execution time limit)
5. Global state with hashable diff: => choose limited set of traditional data types, can be expanded easily later
6. Fair, standard costing of execution spacetime: => author must provide **proof** of run time using a provided cost semantics


To do:
- Write a library to space-efficiently serialise contracts (using Treeless mode? target pre-elaboration representation?)
- Separate calls to Agda typechecker and evaluator, in lieu of typechecking by Certifier contract
- Select data structures to expose based on diff efficiency (Traversable?)
- Write the VM **in Agda**, as simply as I like, including a library to cost typechecked contracts  
  * => To get a contract verified, developers must submit their contract in the citizen language, and proof terms in Agda which satisfy the publicised requirements, to a Certifier. If it passes verification, the author can ask the Certifier to do whatever with it - eg publish to a well-known forum for discovery (new contract which assumes DHT! - App Store? as Curatable).

### VM requirements
- Research computation models with tractable/known costing functions  
  [see http://dlicata.web.wesleyan.edu/pubs/dlr15inductive/dlr15inductive.pdf ]  
  => Simply typed lambda calculus with data constructors (glue for resources, eg compute), in Agda  
  =>
- Binary Show - for transfer and storage
- Differentiability still important => Diff or Zipper for storage types  
  [see http://eelco.lempsink.nl/thesis.pdf]
- What is the underlying storage representation? => Binary key-value store
- Associated Identity type on some Cost, which the app must typecheck on

=>

- Programs must typecheck for:
  - a type-level maximum spacetime cost according to cost semantics judgement rules (Katsuo language written in Agda)
- VM is a monad which:
  - loads and runs programs according to system judgement rules (requests modules from statedb)
  - exposes resource effects (API including literal operations over local statedb file [lmdb-like], API over local storage & compute [kubernetes]) (later: contract patches, codebase patches)
  - keeps track of concrete running cost of programs (write to statedb) (later: general analytics?)

- [Excisions]
  - [~~keeps track of local database state (content, recent transactions, freshness)~~] <- database in rust
  - [~~exposes statedb content and program-initiated transactions to consensus mechanism~~] <- dht/consensus in rust

=>

- Citizen project initialisation (non-self-hosted):
  - The "Author" contract is hardcoded into the prime Citizen node, which when initialised creates the first regular Citizen node, then publishes "Author", "Verifier", "App Store" and "Web Server" contracts to it.
  - The first node must activate the "Web Server" contract so that subsequent nodes can be downloaded, which signals the prime node to delete itself.
  - All subsequent nodes initially download the "App Store" contract.
- Contract initialisation
  - A contract writer creates a contract in the Katsuo language.
  - Optionally: using the Katsuo-reasoning Agda library, they create proofs of desired program behaviour, including a required proof of spacetime bounds when run in VM.
  - Using the Author contract in their citizen account, they send contract + proofs to a Verifier resource for verification (later: if a proof isn't supplied, then at the author's expense).
  - The Verifier receives verification requests, and uses a specialised Agda docker image to verify well-formedness and that proofs pass typechecking.
  - The Verifier compiles the Katsuo contract to Haskell (for the general node) and Javascript (for the minimal node) and keeps file hashes for integrity verification.
  - The Author can request the contract be published to the App Store where any user can download a copy, or sent back unadvertised.
  - Local copies of contracts are stored in a lmdb-like simple database ("statedb").
- Using an initialised contract
  - Users interact with contracts inside their Portfolio where a standard form UI will be generated.
  - Off-chain engagement happens by the contract calling local resources, which causes the node to request a local container be run, and perform operations on log streams.
  - Authors can write contracts which depend on "library" contracts written by others (called programs contribute to calling program's behaviour constraints).
  - Authors can patch contracts using the above process, with Verifiers releasing both the full project files and a diff for incremental update.


### VM Build [[CURRENT TASK]]

- Debug agda-alpine
- Dependently typed language based on old katsuo code, pi-forall..
- Lexer, Parser, Pretty in rust => send intermediate form to agda-alpine as string
- Simple Parser, Abstract Syntax Tree & Type Checker in agda
- Need to port: Typedefs, Telescopes, Erasure
- Level constraint solver with hidden levels a la idris
- Modules saved in statedb, retrieved interactively after building dependency graph

---

Dev environment:  
curl -sSL https://get.haskellstack.org/ | sh  
git clone --depth 1 -b v2.6.0 https://github.com/agda/agda.git  
[see https://github.com/andreyk0/docker-haskell-platform-alpine/blob/master/Dockerfile ]  
[see https://github.com/JLimperg/docker-agda-stdlib/blob/master/2.6.0_1.0.1/Dockerfile ]  
[see https://github.com/agda/agda/blob/master/stack-8.6.5.yaml ]

---

Holochain notes:
- It's bittorrent for web components. Good idea!
- It's like the dual category to blockchain  
  * => Define the objects in the category of blockchains:  
    - monoids (?) on blocks equipped with a construct operation (mining etc)
    - blocks as the product of a block ordering relation (merkle etc) and a set of context extensions (transactions), and
    - sets of computational contexts (wallets)
  * => Consensus mechanisms would then be structures on the blockchain over agencied contexts with the property that Nash equilibrium coincides with asymptotic convergence of contexts.
  * Holochain on the other hand rotates the relations between objects such that context extensions are wrapped in a binary operation on contexts, and the goal of terms having certain desired properties across all contexts is achieved not by convergence of contexts, but by simply forming terms that already have those properties.
  * => Thus for the category of holochain-likes we have:
    - computational contexts equipped with a mutual context extension operation
    - sets of these contexts
  * => The specifically used consensus mechanism combines probabilistic broadcast of evaluated terms on each context extension operation, and a partial mapping of contexts to subcontexts on each context (DHT). This can be generalised to any structure on agencied contexts with the property that Nash equilibrium coincides with integrity of the mutual extension operation
  * => The onus of ensuring the properties of terms is shifted entirely to app developers

Smart contracts are always about marshalling resources. In Citizen's case: data and compute, CRUD on contracts, and patches on the codebase - no more blockchain!
- Contracts must be verified by Certifiers ('Certify' contract)

### Other notes
- Promote the adversarial sub-network ('Disruptor' contract) as integral to security

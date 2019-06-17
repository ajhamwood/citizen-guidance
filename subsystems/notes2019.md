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

### VM requirements [[NEXT TASK]]
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
  - a type-level maximum spacetime cost according to cost semantics judgement rules
- Program type must expose:
  - binary compiler for transfer
- VM is a monad which:
  - loads and runs programs according to system judgement rules
  - exposes resource effects (local statedb file, local storage & compute, contract patches, codebase patches)
  - keeps track of local database state (content, recent transactions, freshness)
  - exposes statedb content and program-initiated transactions to consensus mechanism
  - keeps track of concrete running cost of programs


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

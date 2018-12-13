# Virtual Computer

This file is a semi-structured and non-enforced collection of notes, relevant to the Virtual Computer. Just add to it however you feel like.

### *Current job:*

- Simply typed lambda calculus
- Lambda Pi (Loeh) w/o eliminators
- Understand sweirich/pi-forall ==>  
  **Add data declarations, pattern matching, erasure**~~, following Cockx Dependent Pattern Matching for Agda without-k~~
- Primitives & Builtins
- Holes
- Prelude
- Program costing approaches
- Modules after blockchain

TODO: split Katsuo git into browser and nodejs branches

### What is the virtual computer in Citizen?

- Contracts are programs written by people in some high level language
- If the program does not type check, it won't be encoded.
- If it works, the program is encoded into a binary form at the client side, using tools discoverable through the Portfolio.
- The program is embedded in a transaction, ready to be sent from the client node.
- At the step of injecting the program to a meaningful context, there are two design options:  
  1. The encoded program is submitted to a certifying forum with the Submit Contract transaction (?). Certify Contract is a Curatable contract with decision-makinng authority.  
     If the program is judged by consensus to pass certification, it is sent to the blockmaker node with the Activate Contract transaction.  
     Alternatively,
  2. The encoded program is submitted to the transaction pool, which is a reservoir of transactions offering tokens in exchage for inclusion into a block.  
     The transaction may then be chosen by the blockmaker for inclusion in a block.
- If the transaction is forged into a block, the blockmaker broadcasts the block over the network, along with evidence of authority to do the forging.
- If other nodes accept the evidence, the block is included in their blockchain, and the transactions it contains are executed against their local model of the virtual computer.
  1. The contract in the transaction is parsed into a raw term expression in the virtual context.  
  2. The raw term is elaborated into a completely annotated expression. (?)  
  3. The expression is evaluated into a quotable value (in terms of primitives) (?)
  4. The value is executed and the state is updated (?)
- Nodes check their calculation of the new local state against the state diff hash in the blocks broadcast by their peers. They then update local state if it was different to consensus state.

=> This is assuming a central context. Can't consistent state be ensured based on neighbourhood context rules only? Maybe using a tree-like adjacency structure -> hierarchies of node neighbourhoods, with confirmation by walking the tree between the party nodes, up to 4 neighbourhoods per node (3d space) (?), ping-based movement between neighbourhoods. Larger tree-distances between parties means longer expected confirmation times. How to prevent colluding on ping?

### Univalence-compatible pattern matching in virtual computer

- ~~With Transport, could programs potentially take advantage of eg contract cost optimisations by transporting data structures to structures on primitives? Ie explicitly targeting compiler optimisations... something like a *view*?  
  ==> Proof terms can be transported, so programs can be transported. This is crazy awesome, because given a correct description within the virtual computer of Citizen's subsystems, we can introduce proofs of external behaviour within contracts!~~
- Cubical is not even ready in Agda yet, put outside scope for now


### Name for the high level language?

K A T S U O

### Fake code

- Don't fuck around with DSLs. Just hardcode common syntaxes ((1, "2", 3.0), [1, 2..], do; y <\- x, etc)  
  ==> This means I need built-in Pair, List, Monad...
- I wonder... could `trust_me` be expressed as a set of assumptions injected into context before the program runs?
- For user purposes, nothing is lost by identifying `Type1` with `Type`

```
# Peano naturals
data Nat : Type {
  Z : Nat
  S : (n : Nat) -> Nat
}
data Nat' { Z | S Nat' }

# Primitives
n : Float
n := 5.367e10

s := "Hello'''" : String

# Functions
plus : Nat -> Nat -> Nat {
  @ Z n := n
  @ (S m) n := S (plus m n)
}


# Pi types, aka type family (t is pi bound, so in scope between the braces):
data Vec (t : Type) : Nat -> Type {
  Nil : Vec t Z
  (:: r5) : n ==> (x : t) -> (xs : Vec t n) -> Vec t (S n)
}

# How to do implicit arguments? Erasure?
# id := ({t}, x => x) : (t : Type) ==> a -> a
id := (x => x) : (a : Type) ==> a -> a
const := (x, y => x) : (a, b : Type) ==> (b -> b) -> a -> (b -> b)

# W types (difficult?)
data Tree (a : Type) : Type {
  Node : (label : a) -> [Tree a] -> Tree a
}
data Tree' a : (a : Type) ==> Type { Node' a [Tree' a] }


# Builtin syntax, telescope composition (??)
data Pair (a; b : Type) : a -> b -> Type {
  MkPair : a -> b -> (a, b)
}
data DPair (a : Type); (b : a -> Type) : Type {
  MkDPair : (x : a) -> b x -> (x | b x)
}

# Let binding
mirror : (a : Type) ==> List a -> List a {
  @ xs := xs ++ xs'
  xs' := reverse xs
}

# Case
lookup_default : (a : Type) ==> Nat -> List a -> a -> a {
  @ i xs def := list_lookup i xs {
    Nothing := def
    Just x  := x
  }
}


# Classes/interfaces/records are constructed with signatures
data @ Functor (f : Type -> Type) : Type {
  map : (a, b : Type) ==> (a -> b) -> f a -> f b
}
data @ Applicative (f : Type -> Type) : Type {
  pure : (a : Type) ==> a -> f a
  (<*> l2) : (a, b : Type) ==> f (a -> b) -> f a -> f b
}

# Implementations are constructed with definitions
# Functor (f : Type -> Type) ==> Applicative f {...} ?
Functor Applicative {
  map := g, x => pure g <*> x
}

zipWith : (a, b : Type), (n: Nat) ==>
          Vec (a -> b) n -> Vec a n -> Vec b n {
  @ Nil       _         := Nil
  @ (f :: fs) (x :: xs) := f x :: (zipWith fs xs)
}

# Implicit pattern matching
replicate : (a : Type), (n : Nat) ==> a -> Vec a n {
  _ Z     @ x := []
  _ (S _) @ x := x :: replicate x
}

# Is there a good reason to separate parameters and indexes (eg in data Vec)?
Applicative (n : Nat) ==> a => Vec a n {
  pure := replicate
  (<*>) := zipWith
}

# Force an implementation
Functor (n : Nat) ==> a => Vec a n {
  map f [] := []
  map f (x::xs) := f x :: map f xs
}


# Identity type with propositional equality:
data Id (a : Type) ==> a : a -> Type { # Telescope, not Pi
  Refl : (x : a) ==> (= r4) x x
}
cong : (a, b : Type), (x, y : a) ==> (f : a -> b) -> x = y -> f x = f y {
  @ f Refl := Refl
}

# Example:
# (Idris version uses heterogeneous equality, so not allowed)
# vect_eq_length : (xs : Vect a n) -> (ys : Vect a m) -> (xs = ys) -> n = m
namespace VecEq {
  data (~=~ r4) : Vec a n -> Vec a m -> Type {
    nilCong : [] ~=~ []
    consCong x y : xs, ys ==> ((x = y) : a) -> (xs ~=~ ys) -> (x :: xs ~=~ y :: ys)
  }

  vec_eq_length : (n, m : Nat), (xs : Vec a n), (ys : Vec a m) ==>
                  xs ~=~ ys -> n = m {
    @ nilCong        := Refl
    @ (consCong _ e) := cong S $ vect_eq_length e
  }
}


# Univalence, but no computational behaviour without cubical
extensionality : (a : Type), (b : a -> Type), (f, g : (x : a) -> b x) ==>
                 Type -> Type {
  @ := (x ==> f x = g x) -> (f = g)
```

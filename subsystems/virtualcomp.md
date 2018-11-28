# Virtual Computer

This file is a semi-structured and non-enforced collection of notes, relevant to the Virtual Computer. Just add to it however you feel like.

### *Current job:*

Simply typed lambda + lexer + parser ==> Pi Lambda

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

- With Transport, could programs potentially take advantage of {contract cost optimisations} by transporting data structures to structures on primitives? Ie explicitly targeting compiler optimisations  
  => A something like a *view*?

### Name for the high level language?

### Fake code

Don't fuck around with DSLs. Just hardcode common syntaxes ((1, "2", 3.0), [1, 2..], do; y <- x, etc)

```
# Peano naturals
data Nat : Type {
  Z : Nat
  S : (n : Nat) -> Nat
}
# ...or...
data Nat { Z | S Nat }

# Primitives
n : Float
n := 5.367e10

s := "Hello'''" : String

# Functions
plus : Nat -> Nat -> Nat {
  @ Z n := n
  @ (S m) n := S (plus m n)
}


# Pi types (type family):
data Vec (t : Type) : t ==> Nat -> Type {
  Nil : Vec t Z
  (infixr 5 ::) : n ==> (x : t) -> (xs : Vec t n) -> Vec t (S n)
}

id := (x => x) : (a : Type) ==> a -> a
const := (x, y => x) : (a, b : Type) ==> (b -> b) -> a -> (b -> b)

# W types just with the pipe?


# Multiplication / addition on Types?
data Pair : (a, b : Type) ==> a -> b -> Type { MkPair a b }
data Either : (a, b : Type) ==> a -> b -> Type {
  Left : (l : a) -> Either a b
  Right : (r : b) -> Either a b
}

# Let binding
mirror : (a : Type) ==> List a -> List a {
  xs' := reverse xs
  @ xs = xs ++ xs'
}

# Class / implementation (??)
record Applicative m ==> Monad (m : Type -> Type) {
  (infixl 1 >>=) : (a, b : Type) ==> m a -> ((result : a) -> m b) -> m b
}


# Identity type with propositional equality:
data (infixr 4 =) : (a : Type) => a -> a -> Type { Refl : a = a }
cong : (f : t -> u) ==> f -> (a = b) -> f a = f b {
  @ Refl := Refl
}

# Example:
# (Idris version uses heterogenous equality, so not allowed)
# vect_eq_length : (xs : Vect a n) -> (ys : Vect a m) -> (xs = ys) -> n = m

namespace VecEq {  
  data (infixr 4 ~=~) : Vec a n -> Vec a m -> Type {
    nilCong : [] ~=~ []
    consCong x y : ((x = y) : a) -> (xs ~=~ ys) -> (x :: xs ~=~ y :: ys)
  }

  vec_eq_length : (n, m : Nat), (xs : Vec a n), (ys : Vec a m) ==> xs ~=~ ys -> n = m {
    @ nilCong        := Refl
    @ (consCong _ x) := cong S $ vect_eq_length x
  }
}


# Pi argument (is this even correct over small types?)
Extensionality : (a : Type, b : a -> Type) => a -> b -> Type -> Type {
  @ a b := (f, g : (x : a) -> b x) ==> (x ==> f x = g x) -> (f = g)
}
```

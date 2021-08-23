---
date: 2021-07-20T10:31
---

# GDP

A way to attach proofs to types and through that leveraging a more ergonomic API against modules/libraries.

You attach a name and a proof to a value and by the use of safe-coercion it is possible to get a compile-time safe API with strong guarantees without any extra run-time costs.

`The` typeclass is a uniform way to strip away phantom types from our names.

```haskell
class The d a | d -> a where
  the :: d -> a
  default the :: Coercible d a => d -> a
  the = coerce
```

```haskell
Ghosts of Departed Proofs Haskell ’18, September 27–28, 2018, St. Louis, MO, USA
module Sorted (Named, SortedBy, sortBy, mergeBy) where
import The
import Named
import Data.Coerce
import qualified Data.List as L
import qualified Data.List.Utils as U
newtype SortedBy comp a = SortedBy a
instance The (SortedBy comp a) a
sortBy :: ((a -> a -> Ordering) ~~ comp)
-> [a]
-> SortedBy comp [a]
sortBy comp xs = coerce (L.sortBy (the comp) xs)
mergeBy :: ((a -> a -> Ordering) ~~ comp)
-> SortedBy comp [a]
-> SortedBy comp [a]
-> SortedBy comp [a]
mergeBy comp xs ys =
coerce (U.mergeBy (the comp) (the xs) (the ys))
```

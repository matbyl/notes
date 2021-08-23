# Functor

A functor is a mapping between [[category|categories]].

In haskell the Functor typeclass is defined in the following way:

```haskell
class  Functor f  where
    fmap        :: (a -> b) -> f a -> f b
    (<$)        :: a -> f b -> f a
    (<$)        =  fmap . const
```

Basically a functor can map from one source type `a` to another source type `b`.

Some common functors are:
 * `List`
 * `Maybe`
 * `(->)`

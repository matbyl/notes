# Applicative

It is quite common that one wants to compute several actions in sequence, and the Haskell Prelude comes with such a function:

```haskell
sequence :: [IO a] -> IO [a]
sequence [] = return []
sequence [c:cs] = do
    x <- c
    xs <- sequence cs
    return (x:xs)
```

As you may notice we need to name the values, `x` and `xs`, that are collected from the computations. It is possible to avoid this wiring by the use of an 'effectful application'. One such function lives in the standard Monad library:

```haskell
ap :: m (a -> b) -> m a -> m b
ap mf mx = do
    f <- mf
    x <- mx
    return (f x)
```

Using the function we could redefine sequence in the following way:

```haskell
    sequence :: [IO a] -> IO [a]
    sequence [] = return []
    return [c:cs] = return (:) `ap` c `ap` sequence cs
```

As you may notice this is expressed in a way that abstracts away most of the effectful stuff and better explains what should be done and not how, i.e. more declaritive less imperative.

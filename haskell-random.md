Since haskell is a pure funtional language it is common that a generator is introduced when producing pseudo-random numbers.

The following is an example from `System.Random`:

```haskell
let rolls :: RandomGen g => Int -> g -> [Word]
    rolls n = take n . unfoldr (Just . uniformR (1, 6))
    pureGen = mkStdGen 137
in
    rolls 10 pureGen :: [Word]
```

`uniformR` takes a range and a `RandomGen g` and returns a tuple with a random number between 1 and 6 a new generator. If the same function is run again with the same generator it will produce the same result since the function is pure. To get a new random number you can provide the new generator that was returned by the previous function.

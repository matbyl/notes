# List Monad
---

The list Monad is defined in the following way:

```haskel
instance Monad []  where
    {-# INLINE (>>=) #-}
    xs >>= f             = [y | x <- xs, y <- f x]
    {-# INLINE (>>) #-}
    (>>) = (*>)
```
`return` just wraps an `a` in a list.

`[1,2,3] >>= return . (*) 2` -- Result: [2,4,6] 

`[1,2,3] >>= \x -> [1,2,3] >>= \y -> return $ x * y` -- Result: [1,2,3,2,4,6,3,6,9]  
Is the same as:  
`[y | x <- [1,2,3], y <- [y' | x' <- [1,2,3], y' <- [x * x']]]`

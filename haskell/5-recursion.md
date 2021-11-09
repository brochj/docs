# Recursion

### maximum

```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty list"
maximum' [x] = x
maximum' (x:xs)
    | x > maxTail = x
    | otherwise = maxTail
    where maxTail = maximum' xs
```

Now the third pattern is where the action happens. We use pattern matching to split a list into a head and a tail. This is a very common idiom when doing recursion with lists, so get used to it. We use a where binding to define `maxTail` as the maximum of the rest of the list. Then we check if the head is greater than the maximum of the rest of the list. If it is, we return the head. Otherwise, we return the maximum of the rest of the list.

Let's take an example list of numbers and check out how this would work on them: `[2,5,1]`. If we call maximum' on that, the first two patterns won't match. The third one will and the list is split into 2 and `[5,1]`. The where clause wants to know the maximum of `[5,1]`, so we follow that route. It matches the third pattern again and `[5,1]` is split into 5 and `[1]`. Again, the where clause wants to know the maximum of `[1]`. Because that's the edge condition, it returns 1.

Finally! So going up one step, comparing `5` to the maximum of `[1]` (which is `1`), we obviously get back `5`. So now we know that the maximum of `[5,1]` is `5`. We go up one step again where we had `2` and `[5,1]`. Comparing `2` with the maximum of `[5,1]`, which is `5`, we choose `5`.

---

An even clearer way to write this function is to use `max`. If you remember, `max` is a function that takes two numbers and returns the bigger of them. Here's how we could rewrite `maximum'` by using `max`:

```haskell
maximum' :: (Ord a) => [a] -> a
maximum' [] = error "maximum of empty list"
maximum' [x] = x
maximum' (x:xs) = max x (maximum' xs)
```

### replicate

```haskell
replicate' :: (Num i, Ord i) => i -> a -> [a]
replicate' n x
    | n <= 0    = []
    | otherwise = x:replicate' (n-1) x
```

> Note: `Num` is not a subclass of `Ord`. That means that what constitutes for a number doesn't really have to adhere to an ordering. So that's why we have to specify both the `Num` and `Ord` class constraints when doing addition or subtraction and also comparison.

### take

```haskell
take' :: (Num i, Ord i) => i -> [a] -> [a]
take' n _
    | n <= 0   = []
take' _ []     = []
take' n (x:xs) = x:take' (n-1) xs
```

Notice that we use a guard, but **without an** `otherwise` part. That means that if `n` turns out to be more than 0, the **matching will fall through to the next pattern**.

The third pattern breaks the list into a head and a tail. And then we state that taking `n` elements from a list equals a list that has x as the head and then a list that takes `n-1` elements from the tail as a tail. Try using a piece of paper to write down how the evaluation would look like if we try to take, say, 3 from `[4,3,2,1]`.

### reverse

```haskell
reverse' :: [a] -> [a]
reverse' [] = []
reverse' (x:xs) = reverse' xs ++ [x]
```

### zip

```haskell
zip' :: [a] -> [b] -> [(a,b)]
zip' _ [] = []
zip' [] _ = []
zip' (x:xs) (y:ys) = (x,y):zip' xs ys
```

Zipping `[1,2,3]` and `['a','b']` will eventually try to zip `[3]` with `[]`.

The edge condition patterns kick in and so the result is `(1,'a'):(2,'b'):[]`, which is exactly the same as `[(1,'a'),(2,'b')]`.

### elem

```haskell
elem' :: (Eq a) => a -> [a] -> Bool
elem' a [] = False
elem' a (x:xs)
    | a == x    = True
    | otherwise = a `elem'` xs
```

# quicksort

```haskell
quicksort :: (Ord a) => [a] -> [a]
quicksort [] = []
quicksort (x:xs) =
    let smallerSorted = quicksort [a | a <- xs, a <= x]
        biggerSorted = quicksort [a | a <- xs, a > x]
    in  smallerSorted ++ [x] ++ biggerSorted
```

So if we have, say `[5,1,9,4,6,7,3]` and we want to sort it, this algorithm will first take the head, which is 5 and then put it in the middle of two lists that are smaller and bigger than it. So at one point, you'll have `[1,4,3] ++ [5] ++ [9,6,7]`.

We know that once the list is sorted completely, the number `5` will stay in the fourth place since there are 3 numbers lower than it and 3 numbers higher than it. Now, if we sort `[1,4,3]` and `[9,6,7]`, we have a sorted list! We sort the two lists using the same function. Eventually, we'll break it up so much that we reach empty lists and an empty list is already sorted in a way, by virtue of being empty.

```haskell
[5,    1,    9,    4,    6,    7,    3]
-- first run
--  smallerSorted           head                 biggerSorted
    [1, 4, 3]     ++        [5]     ++          [9, 6, 7]

[]++[1]++[4, 3]                         [6, 7]++[9]++[]

            [3]++[4]++[]            []++[6]++[7]

      []++[3]++[]                              []++[7]++[]
```

So when trying to think of a recursive way to solve a problem, try to think of when a recursive solution doesn't apply and see if you can use that as an edge case, think about identities and think about whether you'll break apart the parameters of the function (**for instance, lists are usually broken into a head and a tail via pattern matching**) and on which part you'll use the recursive call.

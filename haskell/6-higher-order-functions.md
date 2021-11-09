# Higher order functions

[higher-order-functions](http://learnyouahaskell.com/higher-order-functions)

Haskell functions can take functions as parameters and return functions as return values.

A function that does either of those is called a higher order function.

## Curried functions

Every function in Haskell officially only takes one parameter.

```sh
ghci> max 4 5
5
ghci> (max 4) 5
5
```

Putting a space between two things is simply function application.

The `space` is sort of like an operator and **it has the highest precedence**

Let's examine the type of max. It's `max :: (Ord a) => a -> a -> a`.

That can also be written as `max :: (Ord a) => a -> (a -> a)`.
That could be read as: `max` takes an a and returns (that's the `->`) a function that takes an `a` and returns an `a`.

So how is that beneficial to us? Simply speaking, if we call a function with too few parameters, we get back a **partially applied** function, meaning a function that takes as many parameters as we left out.

Using **partial application** (calling functions with too few parameters, if you will) **is a neat way to create functions on the fly** so we can pass them to another function or to seed them with some data.

```haskell
multThree :: (Num a) => a -> a -> a -> a
multThree x y z = x * y * z
```

```haskell
-- Remember that this function's type could also be written as
multThree :: (Num a) => a -> (a -> (a -> a))
```

What really happens when we do `multThree 3 5 9` or `((multThree 3) 5) 9` ?

```sh
ghci> multThree 3 5 9
135

ghci> ((multThree 3) 5) 9
135
```

- First, `3` is applied to `multThree`, because they're separated by a space.

- That **creates a function that takes** one parameter and returns a function.

```haskell
-- What really happens when we do multThree 3 5 9

-- step 0 calling the function
((multThree 3) 5) 9

-- step 1
hiddenFunc = multThree 3 -- "save" the function with on paramenter applied
-- (hiddenFunc 5) 9

-- step 2
hiddenFunc_2 = hiddenFunc 5
-- hiddenFunc_2 9
```

- So then `5` is applied to that, which creates a function that will take a parameter and multiply it by 15.

- `9` is applied to that function and the result is 135

```sh
ghci> let multThreeWith = multThree 3
ghci> let multFifteenWith = multThreeWith 5
ghci> multFifteenWith 9
135
```

By calling functions with too few parameters, so to speak, we're creating new functions on the fly.

### Infix partial application

Infix functions can also be partially applied by using sections.

- To section an infix function, simply surround it with parentheses and only supply a parameter on one side.

That creates a function that takes one parameter and then **applies it to the side that's missing an operand.**

```haskell
divideByTen :: (Floating a) => a -> a
divideByTen = (/10)
```

Calling, say, `divideByTen 200` is equivalent to doing 200 / 10, as is doing `(/10) 200`

```haskell
isUpperAlphanum :: Char -> Bool
isUpperAlphanum = (`elem` ['A'..'Z'])
```

> The only special thing about sections is using `-`. From the definition of sections, `(-4)` would result in a function that takes a number and subtracts 4 from it. However, for convenience, `(-4)` means minus four. So if you want to make a function that subtracts 4 from the number it gets as a parameter, partially apply the `subtract` function like so: `(subtract 4)`

## Some higher-orderism is in order

we're going to make a function that takes a function and then applies it twice to something!

```haskell
applyTwice :: (a -> a) -> a -> a
applyTwice f x = f (f x)
```

- First of all, notice the type declaration. Before, we didn't need parentheses because -> is naturally right-associative. However, here, they're mandatory.

- They indicate that the first parameter is a function that takes something and returns that same thing.

- The function can also be `Int -> Int` or `String -> String` or whatever. But then, the second parameter to also has to be of that type.

```sh
ghci> applyTwice (+3) 10
16
ghci> applyTwice (++ " HAHA") "HEY"
"HEY HAHA HAHA"
ghci> applyTwice ("HAHA " ++) "HEY"
"HAHA HAHA HEY"
ghci> applyTwice (multThree 2 2) 9
144
ghci> applyTwice (3:) [1]
[3,3,1]
```

### zipWith

It takes a function and two lists as parameters and then joins the two lists by applying the function between corresponding elements. Here's how we'll implement it:

```haskell
zipWith' :: (a -> b -> c) -> [a] -> [b] -> [c]
zipWith' _ [] _ = []
zipWith' _ _ [] = []
zipWith' f (x:xs) (y:ys) = f x y : zipWith' f xs ys
```

- The first parameter is a function that takes two things and produces a third thing. `(a -> b -> c)`
- The second and third parameter are lists `[a]` and `[b]`
- The result is also a list `[c]`

```sh
ghci> zipWith' (+) [4,2,5,6] [2,6,2,3]
[6,8,7,9]

ghci> zipWith' max [6,3,2,1] [7,3,1,5]
[7,3,2,5]

ghci> zipWith' (++) ["foo ", "bar ", "baz "] ["fighters", "hoppers", "aldrin"]
["foo fighters","bar hoppers","baz aldrin"]

ghci> zipWith' (*) (replicate 5 2) [1..]
[2,4,6,8,10]

ghci> zipWith' (zipWith' (*)) [[1,2,3],[3,5,6],[2,3,4]] [[3,2,2],[3,4,5],[5,4,3]]
[[3,4,6],[9,20,30],[10,12,12]]
```

### flip

```haskell
flip' :: (a -> b -> c) -> (b -> a -> c)
flip' f = g
    where g x y = f y x
```

we can define this function in an even simpler manner.

Here, we take advantage of the fact that functions are curried.

```haskell
flip' :: (a -> b -> c) -> b -> a -> c
flip' f y x = f x y
```

When we call `flip' f` without the parameters `y` and `x`, it will return an `f` that takes those two parameters but calls them flipped.

## Maps and Filters

### map

takes a function and a list and applies that function to every element in the list, producing a new list. Let's see what its type signature is and how it's defined.

```haskell
map :: (a -> b) -> [a] -> [b]
map _ [] = []
map f (x:xs) = f x : map f xs
```

The type signature says that it takes a function that takes an `a` and returns a `b`, a list of `a`'s and returns a list of `b`'s

```sh
ghci> map (+3) [1,5,3,1,6]
[4,8,6,4,9]

ghci> map (++ "!") ["BIFF", "BANG", "POW"]
["BIFF!","BANG!","POW!"]

ghci> map (replicate 3) [3..6]
[[3,3,3],[4,4,4],[5,5,5],[6,6,6]]

ghci> map (map (^2)) [[1,2],[3,4,5,6],[7,8]]
[[1,4],[9,16,25,36],[49,64]]

ghci> map fst [(1,2),(3,5),(6,3),(2,6),(2,5)]
[1,3,6,2,2]
```

Using map, we can also do stuff like `map (*) [0..]`, **if not for any other reason than to illustrate how currying works and how (partially applied**) functions are real values that you can pass around to other functions or put into lists (you just can't turn them to strings).

- **Applying only one parameter to a function that takes two parameters returns a function that takes one parameter.**

- If we map `*` over the list `[0..]`, we get back a list of functions that only take one parameter, so `(Num a) => [a -> a]`.

- `map (*) [0..]` produces a list like the one we'd get by writing `[(0*),(1*),(2*),(3*),(4*),(5*)`...

```sh
ghci> let listOfFuns = map (*) [0..]
ghci> (listOfFuns !! 4) 5
20
```

### filter

```haskell
filter :: (a -> Bool) -> [a] -> [a]
filter _ [] = []
filter p (x:xs)
    | p x       = x : filter p xs
    | otherwise = filter p xs
```

```sh
ghci> filter (>3) [1,5,3,2,1,6,4,3,2,1]
[5,6,4]

ghci> filter (==3) [1,2,3,4,5]
[3]

ghci> filter even [1..10]
[2,4,6,8,10]

ghci> let notNull x = not (null x) in filter notNull [[1,2,3],[],[3,4,5],[2,2],[],[],[]]
[[1,2,3],[3,4,5],[2,2]]

ghci> filter (`elem` ['a'..'z']) "u LaUgH aT mE BeCaUsE I aM diFfeRent"
"uagameasadifeent"

ghci> filter (`elem` ['A'..'Z']) "i lauGh At You BecAuse u r aLL the Same"
"GAYBALLS"
```

> **All of this could also be achived with list comprehensions by the use of predicates**.

> There's no set rule for when to use `map` and `filter` versus using `list comprehension`, you just have to decide what's more readable depending on the code and the context.

---

Let's find the largest number under 100,000 that's divisible by 3829. To do that, we'll just filter a set of possibilities in which we know the solution lies.

```haskell
largestDivisible :: (Integral a) => a
largestDivisible = head (filter p [100000,99999..])
    where p x = x `mod` 3829 == 0
```

### takeWhile

It takes a predicate and a list and then goes from the beginning of the list and returns its elements while the predicate holds true.

Once an element is found for which the predicate doesn't hold, it stops.

```sh
ghci> takeWhile (/=' ') "elephants know how to party"
"elephants"
```

Example: The sum of all odd squares that are smaller than 10,000.

```sh
ghci> sum (takeWhile (<10000) (filter odd (map (^2) [1..])))
166650
```

We start with some initial data (the infinite list of all natural numbers) and then we map over it, filter it and cut it until it suits our needs and then we just sum it up

We could have also written this using list comprehensions:

```sh
ghci> sum (takeWhile (<10000) [n^2 | n <- [1..], odd (n^2)])
166650
```

### dropWhile

**`dropWhile` is the inverse of `takeWhile`**

```sh
ghci> dropWhile (>3) [8,4,2,1,5,6]
[2,1,5,6]

ghci> takeWhile (>3) [8,4,2,1,5,6]
[8,4]
```

## Lambdas

- Lambdas are basically anonymous functions that are used because we need some functions only once.

- Normally, we make a lambda with the sole purpose of passing it to a higher-order function.

- To make a lambda, we write a `\` and then we write the parameters, separated by spaces. After that comes a `->` and then the function body.

- We usually surround them by parentheses, because otherwise they extend all the way to the right.

Example

```haskell
(\xs -> length xs > 15)
```

Like normal functions, lambdas can take any number of parameters:

```sh
ghci> zipWith (\a b -> (a * 30 + 3) / b) [5,4,3,2,1] [1,2,3,4,5]
[153.0,61.5,31.0,15.75,6.6]
```

## Folds

A fold takes a binary function, a starting value (I like to call it the accumulator) and a list to fold up. The binary function itself takes two parameters. The binary function is called with the accumulator and the first (or last) element and produces a new accumulator. Then, the binary function is called again with the new accumulator and the now new first (or last) element, and so on. Once we've walked over the whole list, only the accumulator remains, which is what we've reduced the list to.

> **The type of the accumulator value and the end result is always the same when dealing with folds**

**Folds can be used to implement any function where you traverse a list once, element by element, and then return something based on that. Whenever you want to traverse a list to return something, chances are you want a fold.**

### left fold `foldl`

It folds the list up from the left side.

Let's implement sum again, only this time, we'll use a fold instead of explicit recursion.

```haskell
sum' :: (Num a) => [a] -> a
sum' xs = foldl (\acc x -> acc + x) 0 xs
```

```sh
ghci> sum' [3,5,2,1]
11
```

```haskell
-- This is what is happening
0  + 3
    [3,5,2,1]

3  + 5
    [5,2,1]

8  + 2
    [2,1]

10 + 1
    [1]
11
```

we can write this implementation ever more succinctly, like so:

```haskell
sum' :: (Num a) => [a] -> a
sum' = foldl (+) 0
```

The lambda function `(\acc x -> acc + x)` is the same as `(+)`. We can omit the xs as the parameter because calling `foldl (+) 0` will return a function that takes a list.

> Generally, if you have a function like `foo a = bar b a`, you can rewrite it as `foo = bar b`, because of currying.

### right fold `foldr`

- The right fold, `foldr` works in a similar way to the left fold, only the accumulator eats up the values from the right.

- Also, the left fold's binary function has the accumulator as the first parameter and the current value as the second one (so `\acc x -> ...`), the right fold's binary function has the current value as the first parameter and the accumulator as the second one (so` \x acc -> ...`).

- It kind of makes sense that the right fold has the accumulator on the right, because it folds from the right side.

```sh
map' :: (a -> b) -> [a] -> [b]
map' f xs = foldr (\x acc -> f x : acc) [] xs
```

If we're mapping `(+3)` to `[1,2,3]`, we approach the list from the right side. We take the last element, which is 3 and apply the function to it, which ends up being 6. Then, we prepend it to the accumulator, which is was `[]`. `6:[]` is `[6]` and that's now the accumulator.

- We apply `(+3)` to 2, that's 5 and we prepend (`:`) it to the accumulator, so the accumulator is now `[5,6]`. We apply `(+3)` to 1 and prepend that to the accumulator and so the end value is `[4,5,6]`.

### `foldr1` and `foldl1`

The `foldl1` and `foldr1` functions work much like `foldl` and `foldr`, only you don't need to provide them with an explicit starting value.

They assume the first (or last) element of the list to be the starting value and then start the fold with the element next to it.

```sh
ghci> foldr (*) 1 [1,2,34,4]
272

ghci> foldr1 (*) [1,2,34,4]
272

```

Because they depend on the lists they fold up having at least one element, they cause runtime errors if called with empty lists

```sh
ghci> foldr1 (*) []
*** Exception: Prelude.foldr1: empty list
```

Just to show you how powerful folds are, we're going to implement a bunch of standard library functions by using folds:

```haskell
maximum' :: (Ord a) => [a] -> a
maximum' = foldr1 (\x acc -> if x > acc then x else acc)

reverse' :: [a] -> [a]
reverse' = foldl (\acc x -> x : acc) []

product' :: (Num a) => [a] -> a
product' = foldr1 (*)

filter' :: (a -> Bool) -> [a] -> [a]
filter' p = foldr (\x acc -> if p x then x : acc else acc) []

head' :: [a] -> a
head' = foldr1 (\x _ -> x)

last' :: [a] -> a
last' = foldl1 (\_ x -> x)
```

## scan

`scanl` and `scanr` are like `foldl` and `foldr`, only they report all the intermediate accumulator states in the form of a list.

There are also `scanl1` and `scanr1`, which are analogous to `foldl1` and `foldr1`.

```sh
ghci> scanl (+) 0 [3,5,2,1]
[0,3,8,10,11]

ghci> scanr (+) 0 [3,5,2,1]
[11,8,3,1,0]

ghci> scanl1 (\acc x -> if x > acc then x else acc) [3,4,5,3,7,9,2,1]
[3,4,5,5,7,9,9,9]

ghci> scanl (flip (:)) [] [3,2,1]
[[],[3],[2,3],[1,2,3]]
```

When using a `scanl`, the final result will be in the last element of the resulting list while a `scanr` will place the result in the head.

## Function application with $

`($)` allows functions to be chained together without adding parentheses to control evaluation order:

First of all, let's check out how it's defined:

```sh
($) :: (a -> b) -> a -> b
f $ x = f x
```

What the heck? What is this useless operator? It's just function application!

Well, almost, but not quite! Whereas normal function application (putting a space between two things) has a really high precedence, the **`$` function has the lowest precedence.**

- Consider the expression `sum (map sqrt [1..130])`. Because `$` has such a low precedence, we can rewrite that expression as `sum $ map sqrt [1..130]`.

**When a `$` is encountered, the expression on its right is applied as the parameter to the function on its left.**

```haskell
ghci> sqrt (3 + 4 + 9)
4.0

ghci> sqrt $ 3 + 4 + 9
4.0
```

- That's why you can imagine a `$` being sort of the equivalent of writing an opening parentheses and then writing a closing one on the far right side of the expression.

- **Well, because `$` is right-associative, `f (g (z x))` is equal to `f $ g $ z x`**

## Function composition

We do function composition with the `.` function, which is defined like so:

```sh
(.) :: (b -> c) -> (a -> b) -> a -> c
f . g = \x -> f (g x)
```

he expression `negate . (* 3)` returns a function that takes a number, multiplies it by 3 and then negates it.

**The compose operator `(.)` creates a new function without specifying the arguments:**

```sh
ghci> let second x = head $ tail x
ghci> second "asdf"
's'

ghci> let second = head . tail
ghci> second "asdf"
's'
```

### Examples

#### 1.1 Using lambda functions

```sh
ghci> map (\x -> negate (abs x)) [5,-3,-6,7,-3,2,-19,24]
[-5,-3,-6,-7,-3,-2,-19,-24]
```

#### 1.2 Using function composition

```sh
ghci> map (negate . abs) [5,-3,-6,7,-3,2,-19,24]
[-5,-3,-6,-7,-3,-2,-19,-24]
```

---

#### 2.1 Using lambda functions

```sh
ghci> map (\xs -> negate (sum (tail xs))) [[1..5],[3..6],[1..7]]
[-14,-15,-27]
```

#### 2.2 Using function composition

```sh
ghci> map (negate . sum . tail) [[1..5],[3..6],[1..7]]
[-14,-15,-27]
```

---

#### 3.1 Using lambda functions

```sh
Prelude> map (\x -> head $ tail $ tail x) ["asdf", "qwer", "1234"]
"de3"
```

#### 3.2 Using function composition

```sh
Prelude> map (head . tail . tail) ["asdf", "qwer", "1234"]
"de3"
```

**The expression `f (g (z x))` is equivalent to `(f . g . z) x`**

But what about functions that take several parameters?

`sum (replicate 5 (max 6.7 8.9))` can be rewritten as

`(sum . replicate 5 . max 6.7) 8.9` or as `sum . replicate 5 . max 6.7 $ 8.9`

---

If you have

`replicate 100 (product (map (*3) (zipWith max [1,2,3,4,5] [4,5,6,7,8])))`

you can write it as

`replicate 100 . product . map (*3) . zipWith max [1,2,3,4,5] $ [4,5,6,7,8]`

TIP: **If the expression ends with three parentheses, chances are that if you translate it into function composition, it'll have three composition operators.**

### point free style

Another common use of function composition is defining functions in the so-called point free style (also called the pointless style). Take for example this function that we wrote earlier:

```haskell
sum' :: (Num a) => [a] -> a
sum' xs = foldl (+) 0 xs
```

The `xs` is exposed on both right sides. Because of currying, we can omit the `xs` on both sides, because calling `foldl (+) 0` creates a function that takes a list. Writing the function as `sum' = foldl (+) 0` is called writing it in point free style. How would we write this in point free style?

```haskell
fn x = ceiling (negate (tan (cos (max 50 x))))
```

```haskell
fn x = ceiling . negate . tan . cos . max 50 $ x
```

We can't just get rid of the `x` on both right right sides. The `x` in the function body has parentheses after it. `cos (max 50)` wouldn't make sense. You can't get the cosine of a function. What we can do is express `fn` as a composition of functions.

```haskell
fn = ceiling . negate . tan . cos . max 50
```

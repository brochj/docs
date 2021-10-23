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









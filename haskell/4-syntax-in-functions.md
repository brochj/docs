# Syntax in Functions

## Pattern matching

When defining functions, you can define separate function bodies for different patterns. 

This leads to really neat code that's simple and readable. You can pattern match on any data type — numbers, characters, lists, tuples, etc. Let's make a really trivial function that checks if the number we supplied to it is a seven or not.

```haskell
lucky :: (Integral a) => a -> String  
lucky 7 = "LUCKY NUMBER SEVEN!"  
lucky x = "Sorry, you're out of luck, pal!"  
```

When you call `lucky`, the **patterns will be checked from top to bottom** and when it conforms to a pattern, the corresponding function body will be used. The only way a number can conform to the first pattern here is if it is 7. If it's not, it falls through to the second pattern, which matches anything and binds it to x. 

```sh
ghci> lucky 7
"LUCKY NUMBER SEVEN!"
ghci> lucky 10
"Sorry, you're out of luck, pal!"
```

**That's why order is important when specifying patterns and it's always best to specify the most specific ones first and then the more general ones later.**


```haskell
charName :: Char -> String  
charName 'a' = "Albert"  
charName 'b' = "Broseph"  
charName 'c' = "Cecil"  
```
#### When making patterns, **we should always include a catch-all pattern** so that our program doesn't crash if we get some unexpected input.

```sh
ghci> charName 'a'  
"Albert"  
ghci> charName 'b'  
"Broseph"  
ghci> charName 'h'  
"*** Exception: tut.hs:(53,0)-(55,21): Non-exhaustive patterns in function charName  
```

---
#### Example
##### Not using pattern matching

```haskell
addVectors :: (Num a) => (a, a) -> (a, a) -> (a, a)  
addVectors a b = (fst a + fst b, snd a + snd b) 
```

##### Using pattern matching

```haskell
addVectors :: (Num a) => (a, a) -> (a, a) -> (a, a)  
addVectors (x1, y1) (x2, y2) = (x1 + x2, y1 + y2)  
```
---

## Defining functions with typeclasses

```haskell
first :: (Num a, Integral b, Integral c) => (a, b, c) -> a  
first (x, _, _) = x  
```

- `a` is  a `Num` which could be a `Int`, `Integer`, `Float` or `Double`

- `b` and `c` are `Integral` so they could be a `Int` or `Integer`

```haskell
-- our version of head function
head' :: [a] -> a  
head' [] = error "Can't call head on an empty list, dummy!"  
head' (x:_) = x  
```

```haskell
tell :: (Show a) => [a] -> String  
tell [] = "The list is empty"  
tell (x:[]) = "The list has one element: " ++ show x  
tell (x:y:[]) = "The list has two elements: " ++ show x ++ " and " ++ show y  
tell (x:y:_) = "This list is long. The first two elements are: " ++ show x ++ " and " ++ show y  
```

> Note that `(x:[]) and (x:y:[])` could be rewriten as `[x]` and `[x,y]` (because its syntatic sugar, we don't need the parentheses)


```haskell
length' :: (Num b) => [a] -> b  
length' [] = 0  
length' (_:xs) = 1 + length' xs 
```

```haskell
sum' :: (Num a) => [a] -> a  
sum' [] = 0  
sum' (x:xs) = x + sum' xs  
```

## _as patterns_  (alias)

```sh
capital :: String -> String  
capital "" = "Empty string, whoops!"  
capital all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x]  
```

## Guards

guards are a way of testing whether some property of a value (or several of them) are true or false. 

That sounds a lot `like an if statement` and it's very similar. The thing is that **guards are a lot more readable** when you have several conditions and they play really nicely with patterns.

```haskell
bmiTell :: (RealFloat a) => a -> String  
bmiTell bmi  
    | bmi <= 18.5 = "You're underweight, you emo, you!"  
    | bmi <= 25.0 = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= 30.0 = "You're fat! Lose some weight, fatty!"  
    | otherwise   = "You're a whale, congratulations!"  
```

A **guard is basically a boolean expression**. If it evaluates to `True`, then the corresponding function body is used. If it evaluates to `False`, checking drops through to the next guard and so on.

Many times, the last guard is `otherwise`. `otherwise` is defined simply as `otherwise = True` and catches everything.

If all the guards of a function evaluate to `False` (and we haven't provided an otherwise catch-all guard), evaluation **falls through to the next pattern**. 

That's how patterns and guards play nicely together. If no suitable guards or patterns are found, an error is thrown.

```sh
<function_name> <parameters> <guards> = <return_expression>
```

```haskell
max' :: (Ord a) => a -> a -> a  
max' a b   
    | a > b     = a  
    | otherwise = b  
```

```haskell
myCompare :: (Ord a) => a -> a -> Ordering  
a `myCompare` b  
    | a > b     = GT  
    | a == b    = EQ  
    | otherwise = LT 
```
> Note: Not only can we call functions as infix with backticks, we can also define them using backticks. Sometimes it's easier to read that way.

```sh
ghci> 3 `myCompare` 2  
GT  
```

## where

We repeat ourselves three times.

```haskell
bmiTell :: (RealFloat a) => a -> a -> String  
bmiTell weight height  
    | bmi <= 18.5 = "You're underweight, you emo, you!"  
    | bmi <= 25.0 = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= 30.0 = "You're fat! Lose some weight, fatty!"  
    | otherwise   = "You're a whale, congratulations!"  
    where bmi = weight / height ^ 2  
```

The names we define in the where section of a function are only visible to that function, so we don't have to worry about them polluting the namespace of other functions

`where` **bindings aren't shared across function bodies of different patterns**. If you want several patterns of one function to access some shared name, you have to define it **globally**.

You can also use where bindings to pattern match! We could have rewritten the where section of our previous function as:

```haskell
...  
where bmi = weight / height ^ 2  
      (skinny, normal, fat) = (18.5, 25.0, 30.0)  
```

Just like we've defined constants in where blocks, you can also define functions.

```haskell
calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi w h | (w, h) <- xs]  
    where bmi weight height = weight / height ^ 2  
```

## Let in

`Let bindings` let you bind to variables anywhere and are expressions themselves, but are very local, so **they don't span across guards**. 


```haskell
cylinder :: (RealFloat a) => a -> a -> a  
cylinder r h = 
    let sideArea = 2 * pi * r * h  
        topArea = pi * r ^2  
    in  sideArea + 2 * topArea  
```
- The form is `let <bindings> in <expression>`

- The names that you define in the `let` part are accessible to the expression after the `in` part

- The difference is that `let bindings` are **expressions** themselves. `where bindings` are just syntactic constructs.

```haskell
ghci> 4 * (let a = 9 in a + 1) + 2  
42  
```

They can also be used to introduce functions in a local scope:

```sh
ghci> [let square x = x * x in (square 5, square 3, square 2)]  
[(25,9,4)] 
```

If we want to bind to several variables inline, we obviously can't align them at columns. That's why we can separate them with semicolons.

```sh
ghci> (let a = 100; b = 200; c = 300 in a*b*c, let foo="Hey "; bar = "there!" in foo ++ bar)  
(6000000,"Hey there!")  
```

They're very useful for quickly dismantling a tuple into components and binding them to names and such.

```sh
ghci> (let (a,b,c) = (1,2,3) in a+b+c) * 100  
600  
```

You can also put `let bindings` inside _list comprehensions_

```haskell
-- using where
calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi w h | (w, h) <- xs]  
    where bmi weight height = weight / height ^ 2  

-- using let bindings
calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi | (w, h) <- xs, let bmi = w / h ^ 2] 
```

We include a let inside a list comprehension much like we would a predicate, only **it doesn't filter the list**, it only binds to names.

The names defined in a `let` inside a list comprehension **are visible to the output function** (the part before the |) and **all predicates and sections that come after** of the binding. 

So we could make our function return only the BMIs of fat people:

```haskell
calcBmis :: (RealFloat a) => [(a, a)] -> [a]  
calcBmis xs = [bmi | (w, h) <- xs, let bmi = w / h ^ 2, bmi >= 25.0] 
```
We omitted the `in` part of the let binding when we used them in list comprehensions because the visibility of the names is already predefined there.


## Case expressions

### Example

#### Using pattern matching

```haskell
head' :: [a] -> a  
head' [] = error "No head for empty lists!"  
head' (x:_) = x 
```

#### Using case expressions

```haskell
head' :: [a] -> a  
head' xs = case xs of [] -> error "No head for empty lists!"  
                   (x:_) -> x  
```

```haskell
case expression of pattern -> result  
                   pattern -> result  
                   pattern -> result  
                   ...  
```


Whereas pattern matching on function parameters can only be done when defining functions, case expressions can be used pretty much anywhere. For instance:

```haskell
-- Using case expressions
describeList :: [a] -> String  
describeList xs = "The list is " ++ case xs of [] -> "empty."  
                                               [x] -> "a singleton list."   
                                               xs -> "a longer list."  
```

They are useful for pattern matching against something in the middle of an expression. 

**Because pattern matching in function definitions is syntactic sugar for case expressions**, we could have also defined this like so:

```haskell
-- Using pattern matching
describeList :: [a] -> String  
describeList xs = "The list is " ++ what xs  
    where what [] = "empty."  
          what [x] = "a singleton list."  
          what xs = "a longer list."
```























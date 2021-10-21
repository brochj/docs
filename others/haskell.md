[http://learnyouahaskell.com/introduction#about-this-tutorial](http://learnyouahaskell.com/introduction#about-this-tutorial)

> In purely functional programming you don't tell the computer what to do as such but rather you tell it what stuff is.

> If you say that a is 5, you can't say it's something else later because you just said it was 5. What are you, some kind of liar? So in purely functional languages, a function has no side-effects.


## Haskell

> Haskell is lazy. That means that unless specifically told otherwise, Haskell won't execute functions and calculate things until it's really forced to show you a result


## Intalling on Manjaro

Installing Haskell ghci on Manjaro Linux.
terminal:

`pacman -S stack`
`stack ghci`

then run the development environment with

`stack ghci`

and quit it with:

`:quit`

this is pretty simple but I had trouble with it so I thought why not help others. apparently there are warnings against installing haskell with pacman.

## Starting Out

Congratulations, you're in GHCI! The prompt here is `Prelude>` but because it can get longer when you load stuff into the session, we're going to use `ghci>`. If you want to have the same prompt, just type in `:set prompt "ghci> "`

 As you probably know, `&&` means a boolean and, `||` means a boolean or. `not` negates a `True` or a `False`.

```sh
ghci> 5 == 5  
True  
ghci> 1 == 0  
False  
ghci> 5 /= 5  
False  
ghci> 5 /= 4  
True  
ghci> "hello" == "hello"  
True   
```

 > Note: you can do `5 + 4.0` because `5` is sneaky and can act like an integer or a `floating-point` number. `4.0` can't act like an `integer`, so `5` is the one that has to adapt.





## Functions

In Haskell, functions are called by writing the function name, a space and then the parameters, separated by spaces. 

```sh
ghci> min 9 10  
9  
```

#### Order
Function application (calling a function by putting a space after it and then typing out the parameters) has the highest precedence of them all. What that means for us is that these two statements are equivalent.

```sh
ghci> succ 9 + max 5 4 + 1  
16  
ghci> (succ 9) + (max 5 4) + 1  
16    
```

So if you see something like `bar (bar 3)`, it doesn't mean that bar is called with bar and 3 as parameters. It means that we first call the function `bar` with `3` as the parameter to get some number and then we call `bar` again with that number. In C, that would be something like `bar(bar(3))`

### infix function
`*` is a function that takes two numbers and multiplies them. As you've seen, we call it by sandwiching it between them. This is what we call an _infix_ function

If a function takes two parameters, we can also call it as an infix function by surrounding it with backticks. For instance, the `div` function takes two integers and does integral division between them. Doing `div 92 10` results in a `9`. But when we call it like that, there may be some confusion as to which number is doing the division and which one is being divided. So we can call it as an infix function by doing 
 
 ```haskell
 92 `div` 10
 ```
 
 and suddenly it's much clearer.

### Creating functions

- Functions are defined in a similar way that they are called. 
- The function name is followed by parameters seperated by spaces. But when defining functions, there's a = and after that we define what the function does.
 
```haskell
doubleMe x = x + x  

doubleUs x y = x*2 + y*2  
```

Save this as `baby.hs` or something. Now navigate to where it's saved and run ghci from there. Once inside GHCI, do `:l baby`. Now that our script is loaded, we can play with the function that we defined.

## IF statement

The difference between Haskell's if statement and if statements in imperative languages is that the `else` **part is mandatory in Haskell**

```haskell
doubleSmallNumber x = if x > 100  
                        then x  
                        else x*2  
```

Another thing about the if statement in Haskell is that it is an expression. An expression is basically a piece of code that returns a value. `5` is an expression because it returns `5`, `4 + 8` is an expression, `x + y` is an expression because it returns the sum of `x` and `y`. Because the else is mandatory, an `if` **statement will always return something and that's why it's an expression**.

```haskell
doubleSmallNumber' x = (if x > 100 then x else x*2) + 1  
```

Note the `'` at the end of the function name. 
- That apostrophe doesn't have any special meaning in Haskell's syntax. 
- It's a valid character to use in a function name. 
- We usually use `'` to either denote a strict version of a function (one that isn't lazy) or a slightly modified version of a function or a variable. Because `'` is a valid character in functions, we can make a function like this.

```haskell
conanO'Brien = "It's a-me, Conan O'Brien!"   
```

## Lists
In Haskell, **lists are a homogenous data structure**. It stores several elements of the **same type**. 

> Note: We can use the `let` keyword to define a name right in GHCI. Doing `let a = 1` inside GHCI is the equivalent of writing `a = 1` in a script and then loading it.

```haskell
ghci> let lostNumbers = [4,8,15,16,23,42]  
ghci> lostNumbers  
[4,8,15,16,23,42]  
```

Strings are just lists of characters. `"hello"` is just syntactic sugar for `['h','e','l','l','o']`

### join lists
This is done by using the `++` operator

```sh
ghci> [1,2,3,4] ++ [9,10,11,12]  
[1,2,3,4,9,10,11,12]  

ghci> "hello" ++ " " ++ "world"  
"hello world"  

ghci> ['w','o'] ++ ['o','t']  
"woot"  
```

#### Watch out when repeatedly using the `++` operator on long strings.

When you put together two lists (even if you append a singleton list to a list, for instance: `[1,2,3] ++ [4])`, internally, Haskell has to walk through the whole list on the left side of `++`. That's not a problem when dealing with lists that aren't too big. But putting something at the end of a list that's fifty million entries long is going to take a while. However, putting something at the beginning of a list using the `:` operator (also called the cons operator) is instantaneous.

```sh
ghci> 'A':" SMALL CAT"  
"A SMALL CAT"  
ghci> 5:[1,2,3,4,5]  
[5,1,2,3,4,5]  
```

> Notice how `:` takes a number and a list of numbers or a character and a list of characters, whereas `++` **takes two lists**. Even if you're adding an element to the end of a list with `++`, **you have to surround it with square brackets so it becomes a list**.

##### Wrong

```sh
ghci> 2 + [1,3,4]

<interactive>:5:1: error:
    • Non type-variable argument in the constraint: Num [a]
      (Use FlexibleContexts to permit this)
    • When checking the inferred type
        it :: forall a. (Num a, Num [a]) => [a]
```

##### Correct

```sh
ghci> 2 : [1,3,4]
[2,1,3,4]
```

### `[1,2,3]` is actually just syntactic sugar for` 1:2:3:[]`. `[]` is an empty list. 

### Get Elements from list
If you want to get an element out of a list by index, use `!!`. 

The indices start at 0.

```sh
ghci> "Steve Buscemi" !! 6  
'B'  
ghci> [9.4,33.2,96.2,11.2,23.25] !! 1  
33.2  
```

### List can be compared

Lists can be compared if the stuff they contain can be compared. When using `<`, `<=`, `>` and `>=` to compare lists, they are compared in lexicographical order. First the heads are compared. If they are equal then the second elements are compared, etc.

```sh
ghci> [3,4,2,3,7,4] > [1] 
True
ghci> [3,4,2,3,7,4] > [2] 
True
ghci> [3,4,2,3,7,4] > [3] 
True
ghci> [3,4,2,3,7,4] > [4] 
False
ghci> [3,4,2,3,7,4] > [5,1] 
False
```

### List mehtods

#### `head` takes a list and returns its head. The head of a list is basically its first element.

```sh
ghci> head [5,4,3,2,1]  
5  
```

#### `tail` takes a list and returns its tail. In other words, it chops off a list's head.

```sh
ghci> tail [5,4,3,2,1]  
[4,3,2,1] 
```

#### `last` takes a list and returns its last element.

```sh
ghci> last [5,4,3,2,1]  
1   
```

#### `init` takes a list and returns everything except its last element.

```sh
ghci> init [5,4,3,2,1]  
[5,4,3,2]   
```
```sh
ghci> head []  
*** Exception: Prelude.head: empty list  
```

When using `head`, `tail`, `last` and `init`, be careful not to use them on empty lists. 

**This error cannot be caught at compile time** so it's always good practice to take precautions against accidentally telling Haskell to give you some elements from an empty list.


#### `length` takes a list and returns its length

```sh
ghci> length [5,4,3,2,1]  
5  
```

#### `null` checks if a list is empty. If it is, it returns `True`, otherwise it returns `False`. 

Use this function instead of `mylist == []` (if you have a list called `mylist`)

```sh
ghci> null [1,2,3]  
False  
ghci> null []  
True  
```

#### `reverse` reverses a list.

```sh
ghci> reverse [5,4,3,2,1]  
[1,2,3,4,5]  
``` 

#### `take` takes number and a list. It extracts that many elements from the beginning of the list. Watch.

```sh
ghci> take 3 [5,4,3,2,1]  
[5,4,3]  
ghci> take 1 [3,9,3]  
[3]  
ghci> take 5 [1,2]  
[1,2]  
ghci> take 0 [6,6,6]  
[] 
```

#### `drop` works in a similar way, only it drops the number of elements from the beginning of a list.

```sh
ghci> drop 3 [8,4,2,1,5,6]  
[1,5,6]  
ghci> drop 0 [1,2,3,4]  
[1,2,3,4]  
ghci> drop 100 [1,2,3,4]  
[]   
```

#### `maximum` takes a list of stuff that can be put in some kind of order and returns the biggest element.

`minimum` returns the smallest.

```sh
ghci> minimum [8,4,2,1,5,6]  
1  
ghci> maximum [1,9,2,3,4]  
9   
```

#### `sum` takes a list of numbers and returns their sum.

#### `product` takes a list of numbers and returns their product.

```sh
ghci> sum [5,2,1,6,3,2,5,7]  
31  
ghci> product [6,2,1,2]  
24  
ghci> product [1,2,5,6,7,9,2,0]  
0
```

#### `elem` takes a thing and a list of things and tells us if that thing is an element of the list. 
It's usually called as an infix function because it's easier to read that way.

```sh
ghci> 4 `elem` [3,4,5,6]  
True  
ghci> 10 `elem` [3,4,5,6]  
False  
```

### List ranges

```sh
ghci> [1..20]  
[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]  
ghci> ['a'..'z']  
"abcdefghijklmnopqrstuvwxyz"  
ghci> ['K'..'Z']  
"KLMNOPQRSTUVWXYZ"   
```

Ranges are cool because you can also specify a step. What if we want all even numbers between 1 and 20? Or every third number between 1 and 20?

```sh
ghci> [2,4..20]  
[2,4,6,8,10,12,14,16,18,20]  
ghci> [3,6..20]  
[3,6,9,12,15,18]   
ghci> [0,10..100]
[0,10,20,30,40,50,60,70,80,90,100]

```

#### decrease a list range

```sh
ghci> [20..1]
[]
```

You need to specify the step

```sh
[20,19..1]
[20,19,18,17,16,15,14,13,12,11,10,9,8,7,6,5,4,3,2,1]
```

#### `cycle` takes a list and cycles it into an infinite list. If you just try to display the result, it will go on forever so you have to slice it off somewhere.

```sh
ghci> take 10 (cycle [1,2,3])  
[1,2,3,1,2,3,1,2,3,1]  
ghci> take 12 (cycle "LOL ")  
"LOL LOL LOL " 
```

`repeat` takes an element and produces an infinite list of just that element. It's like cycling a list with only one element.

```sh
ghci> take 10 (repeat 5)  
[5,5,5,5,5,5,5,5,5,5]  
```

Although it's simpler to just use the `replicate` function if you want some number of the same element in a list. `replicate 3 10` returns `[10,10,10]`.

### List Comprehension
> Math notation is like

```sh
S = {2*x | x E N, x <= 10}
```

If we wanted to write that in Haskell, we could do something like `take 10 [2,4..]`. 

But what if we didn't want doubles of the first 10 natural numbers but some kind of more **complex function applied** on them? 

We could use a list comprehension for that. List comprehensions are very similar to set comprehensions. 

We'll stick to getting the first 10 even numbers for now. The list comprehension we could use is `[x*2 | x <- [1..10]]`. `x` is drawn from `[1..10]` and for every element in `[1..10]` (which we have bound to `x`), we get that element, only doubled. Here's that comprehension in action.


```sh
ghci> [x*2 | x <- [1..10]]  
[2,4,6,8,10,12,14,16,18,20]  

ghci> [(x/2)*27 | x <- [45..56]]
[607.5, 621.0, 634.5, 648.0, 661.5, 675.0, 688.5, 702.0, 715.5, 729.0, 742.5, 756.0]
```

Now let's add a condition (or a predicate) to that comprehension. 

```sh
ghci> [x*2 | x <- [1..10]]  
[2,4,6,8,10,12,14,16,18,20]

ghci> [x*2 | x <- [1..10], x*2 >= 12]  
[12,14,16,18,20]  
```

How about if we wanted all numbers from 50 to 100 whose remainder when divided with the number 7 is 3? Easy.

```sh
ghci> [ x | x <- [50..100], x `mod` 7 == 3]  
[52,59,66,73,80,87,94]   
```

Let's say we want a comprehension that replaces each odd number greater than 10 with "BANG!" and each odd number that's less than 10 with "BOOM!". If a number isn't odd, we throw it out of our list. For convenience, we'll put that comprehension inside a function so we can easily reuse it.

```haskell
boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x]  
```
The last part of the comprehension is the predicate. The function `odd` returns `True` on an odd number and `False` on an even one. The element is included in the list only if all the predicates evaluate to `True`

We can include several predicates. If we wanted all numbers from 10 to 20 that are not 13, 15 or 19, we'd do:

```sh
ghci> [ x | x <- [10..20], x /= 13, x /= 15, x /= 19]  
[10,11,12,14,16,17,18,20] 
```

If we have two lists, `[2,5,10]` and `[8,10,11]` and we want to get the products of all the possible combinations between numbers in those lists, here's what we'd do.

```sh
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11]]  
[16,20,22,40,50,55,80,100,110]  
```

As expected, the length of the new list is 9. What if we wanted all possible products that are more than 50?

```sh
ghci> [ x*y | x <- [2,5,10], y <- [8,10,11], x*y > 50]  
[55,80,100,110] 
```

```sh
ghci> let nouns = ["hobo","frog","pope"]  
ghci> let adjectives = ["lazy","grouchy","scheming"]  
ghci> [adjective ++ " " ++ noun | adjective <- adjectives, noun <- nouns]  
["lazy hobo","lazy frog","lazy pope","grouchy hobo","grouchy frog",  
"grouchy pope","scheming hobo","scheming frog","scheming pope"]   
```


```sh
ghci> removeNonUppercase st = [ c | c <- st, c `elem` ['A'..'Z']]   
ghci> removeNonUppercase "Hahaha! Ahahaha!"  
"HA"  
ghci> removeNonUppercase "IdontLIKEFROGS"  
"ILIKEFROGS"   
```

Nested list comprehensions are also possible if you're operating on lists that contain lists. A list contains several lists of numbers. Let's remove all odd numbers without flattening the list.

```sh
ghci> let xxs = [[1,3,5,2,3,1,2,4,5],[1,2,3,4,5,6,7,8,9],[1,2,4,2,1,6,3,1,3,2,3,6]]  
ghci> [ [ x | x <- xs, even x ] | xs <- xxs]  
[[2,2,4],[2,4,6,8],[2,4,2,6,2,6]]  
```

## Tuples

Another key difference is that they don't have to be homogenous. Unlike a list, a tuple can contain a combination of several types.

we use parentheses: `[(1,2),(8,11),(4,5)]`. What if we tried to make a shape like `[(1,2),(8,11,5),(4,5)]`? Well, we'd get error


```sh
ghci> [(1,2),("One",2)]
<interactive>:14:3: error:

ghci> [("one",1),("two",2)]
[("one",1),("two",2)]
```
**Use tuples when you know in advance how many components some piece of data should have.** Tuples are much more rigid because each different size of tuple is its own type,

#### `fst` takes a pair and returns its first component.
```sh
ghci> fst (8,11)  
8  
ghci> fst ("Wow", False)  
"Wow"  
```

#### `snd` takes a pair and returns its second component. Surprise!

```sh
ghci> snd (8,11)  
11  
ghci> snd ("Wow", False)  
False  
```
> **Note: these functions operate only on pairs. They won't work on triples, 4-tuples, 5-tuples, etc. We'll go over extracting data from tuples in different ways a bit later.**

A cool function that produces a list of pairs: `zip`. It takes two lists and then zips them together into one list by joining the matching elements into pairs. 

It's a really simple function but it has loads of uses. 

It's especially useful for when you want to combine two lists in a way or traverse two lists simultaneously. Here's a demonstration.

```sh
ghci> zip [1,2,3,4,5] [5,5,5,5,5]  
[(1,5),(2,5),(3,5),(4,5),(5,5)]  
ghci> zip [1 .. 5] ["one", "two", "three", "four", "five"]  
[(1,"one"),(2,"two"),(3,"three"),(4,"four"),(5,"five")] 
```

The longer list simply gets cut off to match the length of the shorter one. Because Haskell is lazy, we can zip finite lists with infinite lists:

```sh
ghci> zip [1..] ["apple", "orange", "cherry", "mango"]  
[(1,"apple"),(2,"orange"),(3,"cherry"),(4,"mango")]  
```

### Example using `a^2 + b^2 = c^2`
```sh
ghci> let triangles = [ (a,b,c) | c <- [1..3], b <- [1..3], a <- [1..3] ] 
[
(1,1,1),(2,1,1),(3,1,1),
(1,2,1),(2,2,1),(3,2,1),
(1,3,1),(2,3,1),(3,3,1),
(1,1,2),(2,1,2),(3,1,2),
(1,2,2),(2,2,2),(3,2,2),
(1,3,2),(2,3,2),(3,3,2),
(1,1,3),(2,1,3),(3,1,3),
(1,2,3),(2,2,3),(3,2,3),
(1,3,3),(2,3,3),(3,3,3)]
```
We're just drawing from three lists and our output function is combining them into a triple. If you evaluate that by typing out `triangles` in GHCI, you'll get a list of all possible `triangles` with sides under or equal to 10. Next, we'll add a condition that they all have to be right triangles. We'll also modify this function by taking into consideration that side b isn't larger than the hypothenuse and that side a isn't larger than side b.

```sh
ghci> let rightTriangles = [ (a,b,c) | c <- [1..10], b <- [1..c], a <- [1..b], a^2 + b^2 == c^2]   
```

We're almost done. Now, we just modify the function by saying that we want the ones where the perimeter is 24.

```
ghci> let rightTriangles' = [ (a,b,c) | c <- [1..10], b <- [1..c], a <- [1..b], a^2 + b^2 == c^2, a+b+c == 24]  
ghci> rightTriangles'  
[(6,8,10)]  
```











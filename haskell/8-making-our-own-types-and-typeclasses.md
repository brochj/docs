# Making Our Own Types and Typeclasses

So far, we've run into a lot of data types. `Bool`, `Int`, `Char`, `Maybe`, etc. But how do we make our own? Well, one way is to use the `data` keyword to define a type. 

Let's see how the `Bool` type is defined in the standard library.

```haskell
data Bool = False | True 
```

`data` means that we're defining a new data type. The part before the `=` denotes the type, which is Bool. 

The parts after the `=` are `value constructors`. They specify the different values that this type can have. 

The `|` is read as _or_. So we can read this as: the `Bool` type can have a value of `True` or `False`. 

> Both the type name and the value constructors have to be capital cased.

Now, let's think about how we would represent a shape in Haskell. One way would be to use tuples. A circle could be denoted as `(43.1, 55.0, 10.4)` where the first and second fields are the coordinates of the circle's center and the third field is the radius. Sounds OK, but those could also represent a 3D vector or anything else. A better solution would be to make our own type to represent a shape. Let's say that a shape can be a circle or a rectangle. Here it is:

```haskell
data Shape = Circle Float Float Float | Rectangle Float Float Float Float   

-- Circle is (x, y, radius)  Rectangle  is (x1, y1, x2, y2)
```

The `Circle` value constructor has three fields, which take floats. 

So when we write a value constructor, we can optionally add some types after it and those types define the values it will contain. 

Now when I say fields, I actually mean parameters. Value constructors are actually functions that ultimately return a value of a data type. Let's take a look at the type signatures for these two value constructors.

```sh
ghci> :t Circle  
Circle :: Float -> Float -> Float -> Shape  

ghci> :t Rectangle  
Rectangle :: Float -> Float -> Float -> Float -> Shape  
```
Cool, so **value constructors are functions like everything else**. Who would have thought? 

Let's make a function that takes a shape and returns its surface.

```haskell
surface :: Shape -> Float  
surface (Circle _ _ r) = pi * r ^ 2  
surface (Rectangle x1 y1 x2 y2) = (abs $ x2 - x1) * (abs $ y2 - y1)  
```

The first notable thing here is the type declaration. It says that the function takes a shape and returns a float. 

**We couldn't write a type declaration** of` Circle -> Float` because **`Circle` is not a type**, `Shape` is. Just like we can't write a function with a type declaration of `True -> Int`. 

The next thing we notice here is that **we can pattern match against constructors**. 

We pattern matched against constructors before (all the time actually) when we pattern matched against values like `[]` or `False` or `5`, only those values didn't have any fields. We just write a constructor and then bind its fields to names. Because we're interested in the radius, we don't actually care about the first two fields, which tell us where the circle is.

```sh
ghci> surface $ Circle 10 20 10  
314.15927  

ghci> surface $ Rectangle 0 0 100 100  
10000.0 
```

## Printing custom type

Yay, it works! But if we try to just print out `Circle 10 20 5` in the prompt, we'll get an error. That's because Haskell doesn't know how to display our data type as a string (yet). 

Remember, when we try to print a value out in the prompt, Haskell first runs the show function to get the string representation of our value and then it prints that out to the terminal. To make our Shape type part of the Show typeclass, we modify it like this:

```haskell
data Shape = Circle Float Float Float | Rectangle Float Float Float Float deriving (Show) 
```

We won't concern ourselves with deriving too much for now. Let's just say that if we add `deriving (Show)` at the end of a data declaration, Haskell automagically makes that type part of the `Show` typeclass. So now, we can do this:

```sh
ghci> Circle 10 20 5  
Circle 10.0 20.0 5.0  

ghci> Rectangle 50 230 60 90  
Rectangle 50.0 230.0 60.0 90.0  
```

## Partially application

Value constructors are functions, so we can map them and partially apply them and everything. If we want a list of concentric circles with different radii, we can do this.

```sh
ghci> map (Circle 10 20) [4,5,6,6]  
[Circle 10.0 20.0 4.0,Circle 10.0 20.0 5.0,Circle 10.0 20.0 6.0,Circle 10.0 20.0 6.0]  
```

## Dependent Types

Our data type is good, although it could be better. Let's make an intermediate data type that defines a point in two-dimensional space. Then we can use that to make our shapes more understandable.

```haskell
data Point = Point Float Float deriving (Show)  
data Shape = Circle Point Float | Rectangle Point Point deriving (Show)  
```

Notice that when defining a point, we used the same name for the data type and the value constructor. **This has no special meaning**, although it's common to use the same name as the type if **there's only one value constructor**.

So now the `Circle` has two fields, one is of type `Point` and the other of type `Float`. This makes it easier to understand what's what. Same goes for the rectangle. We have to adjust our `surface` function to reflect these changes.

```haskell
-- before
surface :: Shape -> Float  
surface (Circle _ _ r) = pi * r ^ 2  
surface (Rectangle x1 y1 x2 y2) = (abs $ x2 - x1) * (abs $ y2 - y1) 

--after
surface :: Shape -> Float  
surface (Circle _ r) = pi * r ^ 2  
surface (Rectangle (Point x1 y1) (Point x2 y2)) = (abs $ x2 - x1) * (abs $ y2 - y1)  
```

Using

```sh
ghci> surface (Rectangle (Point 0 0) (Point 100 100))  
10000.0  
ghci> surface (Circle (Point 0 0) 24)  
1809.5574  
```
---

How about a function that nudges a shape? It takes a shape, the amount to move it on the x axis and the amount to move it on the y axis and then returns a new shape that has the same dimensions, only it's located somewhere else.

```haskell
nudge :: Shape -> Float -> Float -> Shape  
nudge (Circle (Point x y) r) a b = Circle (Point (x+a) (y+b)) r  
nudge (Rectangle (Point x1 y1) (Point x2 y2)) a b = Rectangle (Point (x1+a) (y1+b)) (Point (x2+a) (y2+b))
```

```sh
ghci> nudge (Circle (Point 34 34) 10) 5 10  
Circle (Point 39.0 44.0) 10.0  
```
If we don't want to deal directly with points, we can make some auxilliary functions that create shapes of some size at the zero coordinates and then nudge those.

```haskell
baseCircle :: Float -> Shape  
baseCircle r = Circle (Point 0 0) r  
  
baseRect :: Float -> Float -> Shape  
baseRect width height = Rectangle (Point 0 0) (Point width height)  
```

```sh
ghci> nudge (baseRect 40 100) 60 23  
Rectangle (Point 60.0 23.0) (Point 100.0 123.0)  
```

## Exporting custom types

You can, of course, export your data types in your modules. To do that, just write your type along with the functions you are exporting and then **add some parentheses and in them specify the value constructors that you want to export for it**, separated by commas. If you want to export all the value constructors for a given type, just write `..`.

If we wanted to export the functions and types that we defined here in a module, we could start it off like this:

```haskell
module Shapes   
( Point(..)  
, Shape(..)  
, surface  
, nudge  
, baseCircle  
, baseRect  
) where  
```

By doing `Shape(..)`, we exported all the value constructors for `Shape`, so that means that whoever imports our module can make shapes by using the `Rectangle` and `Circle` value constructors. It's the same as writing `Shape (Rectangle, Circle)`.


TODO



















































































































































































































































































# Modules

[Haskell Hierarchical Libraries](https://downloads.haskell.org/~ghc/latest/docs/html/libraries/)

## Loading Modules

A Haskell module is a collection of related functions, types and typeclasses.

A Haskell program is a collection of modules where the main module loads up the other modules and then uses the functions defined in them to do something. Having

The syntax for importing modules in a Haskell script is `import <module name>`

This must be done before defining any functions, so imports are usually done at the top of the file. One script can, of course, import several modules.

---

### Loading Modules fom GHCI

You can also put the functions of modules into the global namespace when using GHCI. If you're in GHCI and you want to be able to call the functions exported by Data.List, do this:

```sh
ghci> :m + Data.List
```

If we want to load up the names from several modules inside GHCI, we don't have to do :m + several times, we can just load up several modules at once.

```sh
ghci> :m + Data.List Data.Map Data.Set
```

---

```haskell
import Data.List

numUniques :: (Eq a) => [a] -> Int
numUniques = length . nub
```

When you do `import Data.List`, all the functions that `Data.List` exports become available in the global namespace,

- `nub` is a function defined in `Data.List` that takes a list and weeds out duplicate elements

### Loading specific functions from modules

If you just need a couple of functions from a module, you can selectively import just those functions. If we wanted to import only the `nub` and `sort` functions from `Data.List`, we'd do this:

```haskell
import Data.List (nub, sort)
```

### Loading all functions from module except ones

You can also choose to import all of the functions of a module except a few select ones. That's often useful when we already have our own function that's called `nub` and we want to import all the functions from `Data.List` except the `nub` function:

```haskell
import Data.List hiding (nub)
```

### `qualified`

Another way of dealing with name clashes is to do qualified imports. The `Data.Map` module, which offers a data structure for looking up values by key, exports a bunch of functions with the same name as `Prelude` functions, like `filter` or `null`. So when we import `Data.Map` and then call `filter`, Haskell won't know which function to use. Here's how we solve this:

```haskell
import qualified Data.Map
```

This makes it so that if we want to reference `Data.Map`'s `filter` function, we have to do `Data.Map.filter`, whereas just `filter` still refers to the normal `filter` we all know and love.

But typing out `Data.Map` in front of every function from that module is kind of tedious. That's why we can rename the qualified import to something shorter:

```haskell
import qualified Data.Map as M
```

Now, to reference` Data.Map`'s `filter` function, we just use `M.filter`.

## Making our own modules

When making programs, it's good practice to take functions and types that work towards a similar purpose and put them in a module. That way, you can easily reuse those functions in other programs by just importing your module.

We'll start by creating a file called `Geometry.hs`

At the beginning of a module, we specify the module name. If we have a file called `Geometry.hs`, then we should name our module `Geometry`.

Then, we specify the functions that it exports and after that, we can start writing the functions. So we'll start with this.

```haskell
module Geometry
( sphereVolume
, sphereArea
, cubeVolume
, cubeArea
, cuboidArea
, cuboidVolume
) where

sphereVolume :: Float -> Float
sphereVolume radius = (4.0 / 3.0) * pi * (radius ^ 3)

sphereArea :: Float -> Float
sphereArea radius = 4 * pi * (radius ^ 2)

cubeVolume :: Float -> Float
cubeVolume side = cuboidVolume side side side

cubeArea :: Float -> Float
cubeArea side = cuboidArea side side side

cuboidVolume :: Float -> Float -> Float -> Float
cuboidVolume a b c = rectangleArea a b * c

cuboidArea :: Float -> Float -> Float -> Float
cuboidArea a b c = rectangleArea a b * 2 + rectangleArea a c * 2 + rectangleArea c b * 2

rectangleArea :: Float -> Float -> Float
rectangleArea a b = a * b
```

We want our module to just present functions for dealing with three dimensional objects, we used `rectangleArea` but we didn't export it.

### hierarchical structures

Modules can also be given a hierarchical structures. Each module can have a number of sub-modules and they can have sub-modules of their own. Let's section these functions off so that `Geometry` is a module that has three sub-modules, one for each type of object.

First, we'll make a folder called `Geometry`. **Mind the capital G**. In it, we'll place three files: `Sphere.hs`, `Cuboid.hs`, and `Cube.hs`. Here's what the files will contain:

```sh
Geometry
 ├── Sphere.hs
 ├── Cuboid.hs
 └── Cube.hs
```

- `Sphere.hs`

```haskell
module Geometry.Sphere
( volume
, area
) where

volume :: Float -> Float
volume radius = (4.0 / 3.0) * pi * (radius ^ 3)

area :: Float -> Float
area radius = 4 * pi * (radius ^ 2)
```

- `Cuboid.hs`

```haskell
module Geometry.Cuboid
( volume
, area
) where

volume :: Float -> Float -> Float -> Float
volume a b c = rectangleArea a b * c

area :: Float -> Float -> Float -> Float
area a b c = rectangleArea a b * 2 + rectangleArea a c * 2 + rectangleArea c b * 2

rectangleArea :: Float -> Float -> Float
rectangleArea a b = a * b
```

- `Cube.hs`

```haskell
module Geometry.Cube
( volume
, area
) where

import qualified Geometry.Cuboid as Cuboid

volume :: Float -> Float
volume side = Cuboid.volume side side side

area :: Float -> Float
area side = Cuboid.area side side side
```

Alright! So first is `Geometry.Sphere`. Notice how we placed it in a folder called `Geometry` and then defined the module name as `Geometry.Sphere`.

Also notice how in all three sub-modules, we defined functions with the same names. We can do this because they're separate modules.

So now if we're in a file that's on the same level as the Geometry folder, we can do, say:

```haskell
import Geometry.Sphere
```

And if we want to juggle two or more of these modules, we have to do qualified imports because they export functions with the same names.

```haskell
import qualified Geometry.Sphere as Sphere
import qualified Geometry.Cuboid as Cuboid
import qualified Geometry.Cube as Cube
```

And then we can call `Sphere.area`, `Sphere.volume`, `Cuboid.area`, etc. and each will calculate the area or volume for their corresponding object.

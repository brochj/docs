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






































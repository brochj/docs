# Data.List

The `Data.List` module is all about lists, obviously. It provides some very useful functions for dealing with them.

<!-- vscode-markdown-toc -->
* [intersperse](#intersperse)
* [intercalate](#intercalate)
* [transpose](#transpose)
* [foldl' and foldl'](#foldlandfoldl)
* [concat](#concat)
* [concatMap](#concatMap)
* [and](#and)
* [or](#or)
* [any and all](#anyandall)
* [iterate](#iterate)
* [splitAt](#splitAt)
* [takeWhile](#takeWhile)
* [dropWhile](#dropWhile)
	* [Example](#Example)
* [span and break](#spanandbreak)
* [partition](#partition)
* [sort](#sort)
* [group](#group)
* [inits an tails](#initsantails)
* [isInfixOf](#isInfixOf)
* [isPrefixOf and isSuffixOf](#isPrefixOfandisSuffixOf)
* [elem and notElem](#elemandnotElem)
* [find](#find)
* [elemIndex](#elemIndex)
* [elemIndices](#elemIndices)
* [findIndex and findIndices](#findIndexandfindIndices)
* [zip3, zip4, zipWith3, zipWith4 ...until 7](#zip3zip4zipWith3zipWith4...until7)
* [lines](#lines)
* [unlines](#unlines)
* [words and unwords](#wordsandunwords)
* [nub](#nub)
* [delete](#delete)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->


## <a name='intersperse'></a>intersperse 

takes **an element** and a list and then puts that element in between each pair of elements in the list. Here's a demonstration:

```sh
ghci> intersperse '.' "MONKEY"  
"M.O.N.K.E.Y"  

ghci> intersperse "." "MONKEY" 
<interactive>:24:17: error:
# returns error "" double quotes means character array (String)

ghci> intersperse 0 [1,2,3,4,5,6]  
[1,0,2,0,3,0,4,0,5,0,6]  
```

## <a name='intercalate'></a>intercalate

takes a list of lists and a list. It then inserts that list in between all those lists and then flattens the result.

```sh
ghci> intercalate " " ["hey","there","guys"]  
"hey there guys"  

ghci> intercalate ' ' ["hey","there","guys"]  
<interactive>:29:13: error:
# returns error ' ' single quotes means single character (Char)


ghci> intercalate [0,0,0] [[1,2,3],[4,5,6],[7,8,9]]  
[1,2,3,0,0,0,4,5,6,0,0,0,7,8,9] 
```

## <a name='transpose'></a>transpose

transposes a list of lists. If you look at a list of lists as a 2D matrix, the columns become the rows and vice versa.

```sh
ghci> transpose [[1,2,3],[4,5,6],[7,8,9]]  
[[1,4,7],[2,5,8],[3,6,9]]  

ghci> transpose ["hey","there","guys"]  
["htg","ehu","yey","rs","e"]
```

## <a name='foldlandfoldl'></a>foldl' and foldl'

`foldl'` and `'foldl1'` are stricter versions of their respective lazy incarnations. When using lazy folds on really big lists, you might often get a stack overflow error. The culprit for that is that due to the lazy nature of the folds, the accumulator value isn't actually updated as the folding happens. 

What actually happens is that the accumulator kind of makes a promise that it will compute its value when asked to actually produce the result (also called a thunk). That happens for every intermediate accumulator and all those thunks overflow your stack. 

The strict folds aren't lazy buggers and actually compute the intermediate values as they go along instead of filling up your stack with thunks. So if you ever get stack overflow errors when doing lazy folds, try switching to their strict versions.

## <a name='concat'></a>concat

flattens a list of lists into just a list of elements.

```sh
ghci> concat ["foo","bar","car"]  
"foobarcar" 

# 1 level
ghci> concat ["first", "first", "first", "first"] 
"firstfirstfirstfirst"

# 2 levels deep
ghci> concat [ [ "second"], ["second"] , ["second"], ["second"] ] 
["second","second","second","second"]

# 3 levels deep
concat [ [ ["third"],["third"] ] , [ ["third"],["third"] ] ]
[["third"],["third"],["third"],["third"]]

ghci> concat [[3,4,5],[2,3,4],[2,1,1]]  
[3,4,5,2,3,4,2,1,1]  
```

It will just remove one level of nesting. So if you want to completely flatten `[[[2,3],[3,4,5],[2]],[[2,3],[3,4]]]`, which is a list of lists of lists, you have to concatenate it twice.

```sh
ghci> concat [[[2,3],[3,4,5],[2]],[[2,3],[3,4]]]
[[2,3],[3,4,5],[2],[2,3],[3,4]]

ghci> concat $ concat [[[2,3],[3,4,5],[2]],[[2,3],[3,4]]]
[2,3,3,4,5,2,2,3,3,4]
```

## <a name='concatMap'></a>concatMap

Doing `concatMap` is the same as first mapping a function to a list and then concatenating the list with `concat`.

```sh
ghci> concatMap (replicate 4) [1..3]  
[1,1,1,1,2,2,2,2,3,3,3,3]  

ghci> concat $ map (replicate 4) [1..3]
[1,1,1,1,2,2,2,2,3,3,3,3]
```

## <a name='and'></a>and 

`and` takes a list of boolean values and returns `True` only if all the values in the list are `True`.

```sh
ghci> and $ map (>4) [5,6,7,8]  
True  
ghci> and $ map (==4) [4,4,4,3,4]  
False
```

## <a name='or'></a>or

`or` is like `and`, only it returns `True` if **any** of the boolean values in a list is `True`.

```sh
ghci> or $ map (==4) [2,3,4,5,6,1]  
True  
ghci> or $ map (>4) [1,2,3]  
False  
```

## <a name='anyandall'></a>any and all

`any` and `all` take a predicate and then check if any or all the elements in a list satisfy the predicate, respectively. Usually we use these two functions instead of mapping over a list and then doing and or or.

```sh
ghci> any (==4) [2,3,5,6,1,4]  
True  
ghci> all (>4) [6,9,10]  
True  
ghci> all (`elem` ['A'..'Z']) "HEYGUYSwhatsup"  
False  
ghci> any (`elem` ['A'..'Z']) "HEYGUYSwhatsup"  
True  
```

## <a name='iterate'></a>iterate

takes a function and a starting value. It applies the function to the starting value, then it applies that function to the result, then it applies the function to that result again, etc. It returns all the results in the form of an infinite list.

```sh
ghci> take 10 $ iterate (*2) 1  
[1,2,4,8,16,32,64,128,256,512]  

ghci> take 3 $ iterate (++ "haha") "haha"  
["haha","hahahaha","hahahahahaha"] 
```

## <a name='splitAt'></a>splitAt

takes a number and a list. It then splits the list at that many elements, returning the resulting two lists in a tuple.

```sh
ghci> splitAt 3 "heyman"  
("hey","man")  

ghci> splitAt 100 "heyman"  
("heyman","")  

ghci> splitAt (-3) "heyman"  
("","heyman")  

ghci> let (a,b) = splitAt 3 "foobar" in b ++ a  
"barfoo"  
```

## <a name='takeWhile'></a>takeWhile

It takes elements from a list while the predicate holds and then when an element is encountered that doesn't satisfy the predicate, it's cut off.

```sh
ghci> takeWhile (>3) [6,5,4,3,2,1,2,3,4,5,4,3,2,1]  
[6,5,4]  
ghci> takeWhile (/=' ') "This is a sentence"  
"This" 
```

Say we wanted to know the sum of all third powers that are under 10,000. 

**We can't** `map (^3)` to `[1..]`, apply a filter and then try to sum that up **because filtering an infinite list never finishes**. You may know that all the elements here are ascending but Haskell doesn't. That's why we can do this:

```sh
ghci> sum . takeWhile (<10000) $ map (^3) [1..]  
53361  
```

## <a name='dropWhile'></a>dropWhile

only it drops all the elements while the predicate is true. Once predicate equates to `False`, it returns the rest of the list.

```sh
ghci> dropWhile (<3) [1,2,2,2,3,4,5,4,3,2,1]  
[3,4,5,4,3,2,1]  

ghci> dropWhile (/=' ') "This is a sentence"  
" is a sentence"  
```

### <a name='Example'></a>Example
The list is made of tuples whose first component is the stock value, the second is the year, the third is the month and the fourth is the date. **We want to know when the stock value first exceeded one thousand dollars**!

```sh
ghci> let stock = [(994.4,2008,9,1),(995.2,2008,9,2),(999.2,2008,9,3),(1001.4,2008,9,4),(998.3,2008,9,5)]  
ghci> head (dropWhile (\(val,y,m,d) -> val < 1000) stock)  
(1001.4,2008,9,4)  
```

## <a name='spanandbreak'></a>span and break

`span` is kind of like `takeWhile`, only it returns a pair of lists. The first list contains everything the resulting list from `takeWhile` would contain if it were called with the same predicate and the same list. The second list contains the part of the list that would have been dropped.

Whereas `span` spans the list while the predicate is true, 

- `break` breaks it when the predicate is first true

```sh
ghci> span (/=4) [1,2,3,4,5,6,7]  
([1,2,3],[4,5,6,7])  

ghci> break (==4) [1,2,3,4,5,6,7]  
([1,2,3],[4,5,6,7])  
```

## <a name='partition'></a>partition

takes a list and a predicate and returns a pair of lists. The first list in the result contains all the elements that satisfy the predicate, the second contains all the ones that don't.

```sh
ghci> partition (`elem` ['A'..'Z']) "BOBsidneyMORGANeddy"  
("BOBMORGAN","sidneyeddy")  

ghci> partition (>3) [1,3,5,6,3,2,1,0,3,7]  
([5,6,7],[1,3,3,2,1,0,3])  
```

It's important to understand how this is different from `span` and `break`:

```sh
ghci> span (`elem` ['A'..'Z']) "BOBsidneyMORGANeddy"  
("BOB","sidneyMORGANeddy")  

ghci> partition (`elem` ['A'..'Z']) "BOBsidneyMORGANeddy"  
("BOBMORGAN","sidneyeddy") 
```

While `span` and `break` are done once they encounter the first element that doesn't and does satisfy the predicate, `partition` goes through the whole list and splits it up according to the predicate.


## <a name='sort'></a>sort  

`sort` simply sorts a list. The type of the elements in the list has to be part of the `Ord` typeclass, because if the elements of a list can't be put in some kind of order, then the list can't be sorted.

```sh
ghci> sort [8,5,3,2,1,6,4,2]  
[1,2,2,3,4,5,6,8]  

ghci> sort "This will be sorted soon"  
"    Tbdeehiillnooorssstw"  
```

## <a name='group'></a>group

takes a list and groups adjacent elements into sublists if they are equal.

```sh
ghci> group [1,1,1,1,2,2,2,2,3,3,2,2,2,5,6,7]  
[[1,1,1,1],[2,2,2,2],[3,3],[2,2,2],[5],[6],[7]]  

ghci> group [1,1,1,1,99,2,2,2,2,3,3,2,2,2,5,6,7] 
[[1,1,1,1],[99],[2,2,2,2],[3,3],[2,2,2],[5],[6],[7]]
```

If we sort a list before grouping it, we can find out how many times each element appears in the list.

```sh
ghci> map (\l@(x:xs) -> (x,length l)) . group . sort $ [1,1,1,1,2,2,2,2,3,3,2,2,2,5,6,7]  
[(1,4),(2,7),(3,2),(5,1),(6,1),(7,1)]  
```

## <a name='initsantails'></a>inits an tails

`inits` and `tails` are like `init` and `tail`, only they recursively apply that to a list until there's nothing left. Observe.

```sh
ghci> inits "w00t"  
["","w","w0","w00","w00t"]  
ghci> tails "w00t"  
["w00t","00t","0t","t",""]  
ghci> let w = "w00t" in zip (inits w) (tails w)  
[("","w00t"),("w","00t"),("w0","0t"),("w00","t"),("w00t","")]  
```


## <a name='isInfixOf'></a>isInfixOf

`isInfixOf` searches for a sublist within a list and returns `True` if the sublist we're looking for is somewhere inside the target list.

```sh
ghci> "cat" `isInfixOf` "im a cat burglar"  
True  

ghci> "cat" `isInfixOf` "cat im a burglar"
True

ghci> "Cat" `isInfixOf` "im a cat burglar"  
False  

ghci> "cats" `isInfixOf` "im a cat burglar"  
False  
```

## <a name='isPrefixOfandisSuffixOf'></a>isPrefixOf and isSuffixOf

`isPrefixOf` and `isSuffixOf` search for a sublist at the beginning and at the end of a list, respectively.

```sh
ghci> "hey" `isPrefixOf` "hey there!"  
True  

ghci> "hey" `isPrefixOf` "oh hey there!"  
False  

ghci> "there!" `isSuffixOf` "oh hey there!"  
True  

ghci> "there!" `isSuffixOf` "oh hey there"  
False  
```

## <a name='elemandnotElem'></a>elem and notElem 

check if an element is or isn't inside a list.



## <a name='find'></a>find

 takes a list and a predicate and returns the first element that satisfies the predicate.

 But it returns that element wrapped in a `Maybe` value

 a `Maybe` value can either be Just something or Nothing. Much like a list can be either an empty list or a list with some elements, a `Maybe` value can be either no elements or a single element. 


```sh
ghci> find (>4) [1,2,3,4,5,6]  
Just 5  

ghci> find (>4) [1,2,3,4,6,5,4,3,2]
Just 6

ghci> find (>9) [1,2,3,4,5,6]  
Nothing  

ghci> :t find  
find :: (a -> Bool) -> [a] -> Maybe a  
```

Remember when we were searching for the first time our stock went over $1000. We did `head (dropWhile (\(val,y,m,d) -> val < 1000) stock)`. Remember that `head` is not really safe. What would happen if our stock never went over $1000? 

Our application of `dropWhile` would return an empty list and getting the head of an empty list would result in an error. However, if we rewrote that as `find (\(val,y,m,d) -> val > 1000)` stock, we'd be much safer. If our stock never went over $1000 (so if no element satisfied the predicate), we'd get back a `Nothing`. But there was a valid answer in that list, we'd get, say, `Just (1001.4,2008,9,4)`.

## <a name='elemIndex'></a>elemIndex

`elemIndex` is kind of like `elem`, only it doesn't return a boolean value. It maybe returns the index of the element we're looking for. If that element isn't in our list, it returns a `Nothing`.

```sh
ghci> :t elemIndex  
elemIndex :: (Eq a) => a -> [a] -> Maybe Int  

ghci> 4 `elemIndex` [1,2,3,4,5,6]  
Just 3  

ghci> 10 `elemIndex` [1,2,3,4,5,6]  
Nothing  
```

## <a name='elemIndices'></a>elemIndices

`elemIndices` is like `elemIndex`, only it returns a list of indices, in case the element we're looking for crops up in our list several times. 

Because we're using a list to represent the indices, we don't need a `Maybe` type, because failure can be represented as the empty list, which is very much synonymous to `Nothing`.

```sh
ghci> ' ' `elemIndices` "Where are the spaces?"  
[5,9,13]  

ghci> ' ' `elemIndices` "Wherearethespaces" 
[]
```

## <a name='findIndexandfindIndices'></a>findIndex and findIndices

`findIndex` is like find, but it maybe returns the index of the first element that satisfies the predicate. 

`findIndices` returns the indices of all elements that satisfy the predicate in the form of a list.

```sh
ghci> findIndex (==4) [5,3,2,1,6,4]  
Just 5  

ghci> findIndex (==7) [5,3,2,1,6,4]  
Nothing  

ghci> findIndices (`elem` ['A'..'Z']) "Where Are The Caps?"  
[0,6,10,14]  
```

## <a name='zip3zip4zipWith3zipWith4...until7'></a>zip3, zip4, zipWith3, zipWith4 ...until 7

```sh
ghci> zipWith3 (\x y z -> x + y + z) [1,2,3] [4,5,2,2] [2,2,3]  
[7,9,8] 

ghci> zip4 [2,3,3] [2,2,2] [5,5,3] [2,2,2]  
[(2,2,5,2),(3,2,5,2),(3,2,3,2)] 

ghci> zip4 ['a','b','c'] [1,2,3] ['d','e','f'] [4,6,6]
[('a',1,'d',4),('b',2,'e',6),('c',3,'f',6)]
```



zip4 ['a','b','c'] [1,2,3] ['d','e','f'] [4,6,6]

## <a name='lines'></a>lines

`lines` is a useful function when dealing with files or input from somewhere. It takes a string and returns every line of that string in a separate list.

```sh
ghci> lines "first line\nsecond line\nthird line"  
["first line","second line","third line"]  
```

## <a name='unlines'></a>unlines

`unlines` is the inverse function of lines. It takes a list of strings and joins them together using a `'\n'`

```sh
ghci> unlines ["first line", "second line", "third line"]  
"first line\nsecond line\nthird line\n"  
```
- Using `intercalate` we don't have the `\n` after the last element.

```sh
ghci> intercalate "\n" ["first line", "second line", "third line"]  
"first line\nsecond line\nthird line"
```

## <a name='wordsandunwords'></a>words and unwords

`words` and `unwords` are for splitting a line of text into words or joining a list of words into a text. Very useful.

```sh
ghci> words "hey these are the words in this sentence"  
["hey","these","are","the","words","in","this","sentence"]  

ghci> words "\t\they these           are    the words in this\nsentence\n"  
["hey","these","are","the","words","in","this","sentence"]  

ghci> unwords ["hey","there","mate"]  
"hey there mate"  

ghci> unwords ["hey","there","ma te"] 
"hey there ma te"
```

## <a name='nub'></a>nub
It takes a list and **weeds out the duplicate elements**, returning a list whose every element is a unique snowflake! 

The function does have a kind of strange name. It turns out that "nub" means a small lump or essential part of something.

```sh
ghci> nub [1,2,3,4,3,2,1,2,3,4,3,2,1]  
[1,2,3,4]  

ghci> nub "Lots of words and stuff"  
"Lots fwrdanu" 
```

## <a name='delete'></a>delete

`delete` takes an element and a list and **deletes the first occurence** of that element in the list.

```sh
ghci> delete 'h' "hey there ghang!"  
"ey there ghang!"  

ghci> delete 'h' . delete 'h' $ "hey there ghang!"  
"ey tere ghang!"  

ghci> delete 'h' . delete 'h' . delete 'h' $ "hey there ghang!"  
"ey tere gang!"  
```






















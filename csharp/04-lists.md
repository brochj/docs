# 04 Lists

## Lists

```csharp
var names = new List<string> {"Oscar", "Broch", "Junior"};

foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

### Adding elements

```csharp
var names = new List<string> {"Oscar", "Broch", "Junior"};

foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}

Console.WriteLine();
names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");
foreach (var name in names)
{
  Console.WriteLine($"Hello {name.ToUpper()}!");
}
// Hello OSCAR!
// Hello BROCH!
// Hello JUNIOR!

// Hello OSCAR!
// Hello BROCH!
// Hello JUNIOR!
// Hello MARIA!
// Hello BILL!
```

## Picking an element

```csharp
var names = new List<string> {"Oscar", "Broch", "Junior"};

Console.WriteLine($"My name is {names[0]}.");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list.");

// My name is Oscar.
// I've added Junior and Maria to the list.
```

## Counting elements List.Count

```csharp
Console.WriteLine($"The list has {names.Count} people in it");
```

## Searching for an element List.IndexOf()

he IndexOf method searches for an item and returns the index of the item. If the item isn't in the list, `IndexOf` returns `-1`.

```csharp
var names = new List<string> {"Oscar", "Broch", "Felipe"};

var index = names.IndexOf("Felipe");
if (index != -1)
  Console.WriteLine($"The name {names[index]} is at index {index}");

var notFound = names.IndexOf("Not Found");
Console.WriteLine($"When an item is not found, IndexOf returns {notFound}");

// The name Felipe is at index 2
// When an item is not found, IndexOf returns -1
```

## Sorting a List List.Sort()

```csharp
names.Sort();
foreach (var name in names)
{
  Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

## Fibonacci

```csharp
var fibonacciNumbers = new List<int> {1, 1};

while (fibonacciNumbers.Count < 20)
{
    var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
    var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

    fibonacciNumbers.Add(previous + previous2);
}
foreach(var item in fibonacciNumbers)
    Console.WriteLine(item);
```
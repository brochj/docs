# Arrays

- Array sao reference types

## Criando um Arrays

```csharp
var myArray = new int[5];  // [0,0,0,0,0]

int[] myArray = new int[5]; // [0,0,0,0,0]

var myArray = new int[5]{1,2,3,4,5};  // [1,2,3,4,5]

myArray[0] = 12; // [12,0,0,0,0]

```
## Percorrendo Arrays

```csharp
var myArray = new int[5];  // [0,0,0,0,0]

for (int i = 0; i < myArray.Length; i++)
{
  Console.WriteLine(myArray[i]);
  
}

foreach (var item in myArray)
{
  Console.WriteLine(item);
  
}
```
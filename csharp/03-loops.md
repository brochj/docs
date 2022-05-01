# 03 - Loops

## if statement

```c#
int a = 5;
int b = 5;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10.");
```

> The indentation under the if and else statements is for human readers. The C# language doesn't treat indentation or white space as significant.

```c#
int a = 5;
int b = 3;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10");
else
    Console.WriteLine("The answer is not greater than 10");
```

> Because indentation isn't significant, you need to use { and } to indicate when you want more than one statement to be part of the block that executes conditionally.

```c#
int a = 5;
int b = 3;
if (a + b > 10)
{
    Console.WriteLine("The answer is greater than 10");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
}
```

```csharp
int a = 5;
int b = 3;
int c = 4;
if ((a + b + c > 10) && (a == b) || (a == c))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("And the first number is equal to the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("Or the first number is not equal to the second");
}
```

## While Loop

```csharp
int counter = 0;
while (counter < 10)
{
  Console.WriteLine($"Hello World! The counter is {counter}");
  counter++;
}
```

## Do While Loop

```csharp
int counter = 0;
do
{
  Console.WriteLine($"Hello World! The counter is {counter}");
  counter++;
} while (counter < 10);
```

## For Loop

```csharp
for(int counter = 0; counter < 10; counter++)
{
  Console.WriteLine($"Hello World! The counter is {counter}");
}
```

The first part is the **for initializer**: `int counter = 0`; declares that counter is the loop variable, and sets its initial value to 0.

The middle part is the **for condition**: `counter < 10` declares that this for loop continues to execute as long as the value of counter is less than 10.

The final part is the **for iterator**: `counter++` specifies how to modify the loop variable after executing the block following the for statement. Here, it specifies that counter should be incremented by 1 each time the block executes.

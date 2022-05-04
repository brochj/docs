# Exceptions

## Try Catch

```csharp
try {
// Code
}
catch (IndexOutOfRangeException ex)
{
  Console.WriteLine(ex.InnerException);
  Console.WriteLinel(ex.Message);
  Console.WriteLine("Nai encontrei o indice na lista");
} 
catch (Exception ex) {
  Console.WriteLine(ex.InnerException);
  Console.WriteLinel(ex.Message);
  Console.WriteLine("Ops, algo deu errado!");
}
finally 
{
  // SEMPRE PASSA NO FINALLY, MESMO QUE NAO OCORRA UMA EXCEPTION

  // Usos: Fechar arquivo, conexao com banco de dados,...
}
```

## Throw Exception

```csharp
if (string.IsNullOrEmpty(texto)){
  throw new Exception("O texto nao pode ser nulo")
}
```

## Custom Exceptions

```csharp
public static class MyException : Exception
{
    public MyException(DateTime date)
    {
      QuandoAconteceu = date;
    }

    public DateTime QuandoAconteceu { get; set; }
}
```
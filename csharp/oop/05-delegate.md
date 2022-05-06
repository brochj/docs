# Delegate


```csharp

class Program
{
  static void Main()
  {
    var pagar = new Pagamento.Pagar(RealizarPagamento);
    pagar(45)
  }

  static void RealizarPagamento(double valor) // A signature deve ser igual do método Pagar()
  {

  }
}


class Pagamento
{
  public delegate void Pagar(double valor); // Não tem implementação
}
```
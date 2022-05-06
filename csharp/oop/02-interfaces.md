# interfaces


A interface define tudo que a classa tem que ter.

Não se define os modificadores (public,...) na interface

```csharp
public class Payment : IPayment
{
    
}

interface IPayment
{
  DateTime Vencimento { get; set; }

  void Pagar(double valor);
}

```

# Classe Abstratas

Classes Abstratas não podem ser instanciadas, só podem ser herdadas.

Classes Abstratas podem ter implementações, exemplo alguma validação, algo que sempre precise ser feito pelas classes que vão herdar.


```csharp
public abstract class Pagamento : IPagamento {} // implementa a interface, com métodos virtuais

public class PagamentoCartao : Pagamento {} // Faz o override dos métodos de Pagamento
public class PagamentoBoleto : Pagamento {} // Faz o override dos métodos de Pagamento
public class PagamentoAppleP : Pagamento {} // Faz o override dos métodos de Pagamento
public class PagamentoSamsun : Pagamento {} // Faz o override dos métodos de Pagamento

interface IPayment {}
```
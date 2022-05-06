## Objetos

Objetos possuem

- Propriedades
- Métodos
- Eventos

Objetos são sempre um Tipo de Referência

## Classes

## Encapsulamento

Encapsulamento é agrupar dentro de uma classe os Métodos, Propriedades e Eventos, que fazem sentido estarem juntos.

## Abstração

Esconder os detalhes, ou seja, deixar como privado métodos e propriedades que não fazem sentido serem expostas para outras classes.

**Quanto mais esconder melhor**, pois caso precise alterar a classe, não vai quebrar outra parte do código que estão usando os métodos e Propriedades

## Herança

## Polimorfismo

No C# usamos a keyword `virtual` na classe pai, no método/propriedade que queremos sobrescrever nas classes filhas.

```csharp
class Pagamento {
  public virtual void Pagar(){

  }
}

class PagamentoBoleto : Pagamento {
  public override void Pagar(){

  }
}
```

## Modificadores de Acesso

- private: visível só dentro da classe
- protected: visível só para os FILHOS que herdam da classe
- internal:
- public:

## Tipos Complexo

Classes e structs são tipos complexos.

Evitar criar classes com muitas propriedades primitivas, 


## Propriedades

Propriedades possuem diferentes de variáveis, pois as propriedades possuem acessores `get` e `set`

```csharp
class Pagamento {
  
  public DateTime Vencimento {get; set};


  private DateTime _dataPagamento;

  public DateTime DataPagamento 
  {
    get {return _dataPagamento;}
    set {_dataPagamento = value;}
  }

}
```

## Métodos

### Sobrecargas de método

É quando utilizamos o mesmo NOME de um métodos, mas mudamos apenas sua assinatura,

- Signature de um Método: é composta pelo Retorno, Nome, e Parâmetros do Método

```csharp
class Pagamento {
  
public static void Pagar(string numero) { }
public static void Pagar(string numero, DateTime vencimento) { }

}
```

### Sobreescrita de método

Ver no Polimorfismo

Usa-se as keyword `virtual` e `override`

### Método Construtor

É sempre chamado no momento que que um objeto é instanciado.

É possível criar sobrecargas do método Construtor
```csharp
var pagar = new Pagamento();

class Pagamento
{
  public Pagamento (DateTime vencimento) {  }
  public Pagamento () {  }
}

class NoBoleto : Pagamento
{
  public NoBoleto(DateTime vencimento) : base(vencimento) { }
}
```

### Using e Dispose

O disposable é como se fosse um método "desconstrutor". Para usá-lo perecisamos implementar a interface `IDisposable`, que nada mais é do que criar um método chamado `Dispose`

Para garantir que o `Dispose` será chamado, vamos usar o `using`

Detalhe: Para usar o `using`, a classe necessariamente deve implementar `IDisposable`

```csharp
class Main
{
  using(var pagamento = new Pagamento()){
    Console.WriteLine("Processando o pagamento");
  }
}


public class Pagamento : IDisposable
{
  // Construtor
  public Pagamento() 
  {
      Console.WriteLine("Iniciando o pagamento");
  }

  // "Destruidor"
  public void Dispose()
  {
      Console.WriteLine("Finalizando o pagamento");
  }
}
// No Console vai aparecer

// Iniciando o pagamento
// Processando o pagamento
// Finalizando o pagamento

```

## Classes Estáticas

- Quando a classe é do tipo `static` siginifica que ela não pode ser instanciada.

- A classe sempre vai estar disponível a partir do start da aplicação.

- Se a classe for `static` seus métodos e propriedades também devem ser do tipo `static`

```csharp
public static class Main
{
    // var pagamento = new Pagamento(); // Não consigo instaciar Pagamento()
    Pagamento.Vencimento = DateTime.Now
}
public static class Pagamento
{
  public static DateTime Vencimento { get; set; }
}
```

Um bom lugar para usar classe static é nas config, pois assim toda a aplicação vai ter acesso.

```csharp
public static class Settings
{
    public static string API_URL { get; set; }
    public static string API_HOME { get; set; }
}
```

## Classe Seladas

selead: Não permite que a classe seja herdada

Usada quando você precisa garantir que classe só tenha uma forma.

```csharp
public sealed class Pagamento
{
  
}
```

## Classes Parciais (partial)

Usanda quando queremos dividir a classe e várias partes.

Para isso, elas devem estar no mesmo `namespace` e possuir mesmo nome.

```csharp
class Main
{
  
}

// Payments.cs
namespace Payments
{
  public class Payment
  {
    
  }
}

// CreditCard.cs
namespace Payments
{
  public class partial Payment
  {
    
  }
}



```


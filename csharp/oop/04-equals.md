# Comparando Objetos

## Equals

```csharp
var pessoaA = new Pessoa("andré", id: 1);
var pessoaB = new Pessoa("andré", id: 1);

// pessoaA == pessoaB -> False 
// (é falso porque são tipos de referência, 
//só armazenam os endereços na memória, e eles são difernetes)



```

A melhor forma para comparar é implementar uma interface `IEquatable`, 
que vai pedir que implemente um método `Equals()` que retora
um `bool` e recebe um Objeto do mesmo tipo da classe.




```csharp
public class Pessoa : IEquatable<Pessoa>
{

  public strin Id { get; set; }

  public bool Equals(Pessoa other) 
  {
    return Id == other.Id;
  }

}
```

Agora se fizer

```csharp
pessoaA.Equals(pessoaB); // -> True
// Pois ele vai comparar os Id dos dois objetos.
```
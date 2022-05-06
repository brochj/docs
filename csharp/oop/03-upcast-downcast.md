# Upcast Downcast


Uma pessoa física tambm é uma pessoa,

e uma pessoa, pode ser pessoa física.

Quando é feita da classe filha para pai, 
é chamado de `upcast`
Quando é feita da classe pai para filha, 
é chamado de `downcast`


```csharp

class Payments
{
  static void Main(string[] args)
  {
    var pessoa = new Pessoa();
    var pessoaFisica = new PessoaFisica()
    // Consigo mudar o TIPO de pessoa (downcast)

    pessoaFisica = (PessoaFisica)pessoa; // Convertendo pessoa -> PessoaFisica, usando conversão explícita (cast)

    // O inverso também é possível (upcast)

    var PessoaJuridica = new PessoaJuridica{} // classe filha, objeto filho
    pessoa = PessoaJuridica; // objeto filho, sendo passado para um da classe pai.

  }
}

class Pessoa
{
  public string Name { get; set; }
}

class PessoaFisica : Pessoa
{
  public string Cpf { get; set; }
}

class PessoaJuridica : Pessoa 
{
  public string Cnpj { get; set; }
}
```
# struct

Definições

- Tipos de dado estruturado
- Apenas a estrutura, o esqueleto
- Tipo de valor (value type)
- Armazenam apenas outros tipos de dados
- Definido pela palavra struct
- Composto de propriedades e métodos
- Nome sempre com maiúsculo
  - O mesmo para propriedades e métodos
- Criado a partir da palavra `new`
  - Neste momento sim temos os valores

```csharp
struct Product
{
// propriedades
  public int Id;
  public float Price;
  public string Title;

// metodos
  public float PriceInDolar(float dolar)
  {
    return Price * dolar;
  }
}
```
Instanciando um `struct`
```csharp
var product = new Product();
```

```csharp
var product = new Product(); 
product.Id = 1;
product.Title = "Mouse gamer"; 
product.Price = 197.23f;

Console .WriteLine(product.Id);
Console .WriteLine(product.Title);
Console .WriteLine(product.Price);
```

## struct podem possuir método construtor

```csharp
struct Product
{
  // Não precisa especificar o retorno, quando é o método construtor.
  public Product(int id, string title, float price)
  {
    Id = id;
    Title = title;
    Price = price;
  }

  public int Id;
  public string Title;
  public float Price;
}
```

```csharp
var product = new Product(1, "Mouse Gamer", 128.75f); 

Console .Writeline(product.Id);
Console .WriteLline(product.Title);
Console .WriteLine(product.Price);
Console .WriteLine(product.PriceInDolar(5.70f));
```
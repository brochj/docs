# Enums

Definições 

- Usado para fornecer uma melhor visualização do código
- Substituem o uso de inteiros
- Usados em listas curtas
- Usados em dados fixos
-   Hard Coded
- Sempre em maiúsculo
-   Começar com a letra E

```csharp
enum EEstadoCivil
{
  Solteiro = 1,
  Casado = 2, 
  Divorciado = 3
}
```

Formas de usar

```csharp
struct Cliente
{
  public string Nome; 
  public EEstadoCivil EstadoCivil;
}
```

```csharp
var cliente = new Cliente("João Silva", EEstadoCivil.Casado);
```

## Exibindo dados de um enumerador

```csharp
Console .WriteLine(cliente.Nome);
Console .WriteLine(cliente.EstadoCivil); // Escreve Casado
Console .WriteLine((int)cliente.EstadoCivil); // Escreve 2
```
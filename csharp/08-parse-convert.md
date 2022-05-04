# Parse

- Método presente em todo tipo primitivo
- Usado para converter um **caractere ou string** para um tipo qualquer 
- Caso haja alguma incompatibilidade, gera um erro

```csharp
int inteiro = int.Parse("100");
```

# Convert


- Similar ao parse visto anteriormente
- Porém permite converter vários tipos de valor
- Não apenas string
- Devemos Informar o tipo na chamada da conversão

```csharp
int inteiro = Convert.ToInt32("100");
```
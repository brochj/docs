
## Heap and Stack
Definições

- A memória é dividida em duas partes, Heap e Stack 

- `Heap` armazena os dados

- `Stack` armazena as referências para os dados

Definições
- Qualquer tipo no .NET é tratado como
- Tipo de Referência (Reference Type)
- Tipo de Valor (Value Type)
- Tipos de valor armazenam dados
- São armazenados em um local da memória chamada Stack

## Value Types (Stack)

- Quando armazenamos um valor, a memória é alocada
- Este espaço armazena o dado criado
- Nossa variável acessa este dado diretamente
- Se assimilarmos uma variável do tipo de valor a outra
  - O valor será COPIADO
  - Ambas serão independents
- Exemplos: `Built-in`, `Structs`, `Enums`
- Garbage Collector não acessa o Stack

```csharp
int x = 25;
int y = x; // Y é um cópia de X
Console.Writeline(x); // 25
Console.Writeline(y); // 25
x = 32; // Somente x foi alterado
Console.Writeline(x); // 32
Console.Writeline(y); // 25
```
## Reference Types (Heap)
Definições 
- Armazenam o endereço do objeto que contém os dados
- Não armazena os dados em si
- São armazenados em um local da memória chamado de Heap
- Ao assimilar uma variável
  - Criará uma referência
  - Aponta para a mesma informação
  - Nãosãoindependentes
- Quando não mais utilizados são marcados para exclusão
- **Garbage Collector** passa removendo todos eles
- Exemplos: `Classes`, `Objects`, `Arrays`...

```csharp
var arr = new string[2]; 
arr[0] = "Item 1"; 
var arr2 = arr; // Não cria uma cópia

Console .WriteLine(arr[0]); 
Console .Writeline(arr2[0]);

// Altera as duas listas
arr[0] = "Item Alterado"; 
Console .WriteLine(arr[0]); 
Console .WriteLine(arr2[0]);
```
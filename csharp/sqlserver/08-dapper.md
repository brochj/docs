# Dapper

```sh
dotnet add package Dapper
```

Criar ua pasta `Models` e nessa pasta criar um classe (na maioria das vezes) para cada tabela do banco

```csharp
// Models/Category.cs
namespace BrochDataAccess.Models
{
    public class Category
    {
        public Guid Id { get; set; } // O nome da propriedade tem que ser o mesmo nome da coluna da tabela
        public string Title { get; set; }
    }
}
```

## Conectando no banco e fazendo um SELECT

```csharp
using BrochDataAccess.Models;
using Dapper;
using Microsoft.Data.SqlClient;

const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";


using (var connection = new SqlConnection(connectionString))
{
    var categories = connection.Query<Category>("SELECT [Id], [Title] FROM [Category]");

    foreach (var category in categories)
    {
        Console.WriteLine($"{category.Id} - {category.Title}");
    }
}
```

## Fazendo um Insert

```csharp
using BrochDataAccess.Models;
using Dapper;
using Microsoft.Data.SqlClient;

const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";

// Crio um objeto 
var category = new Category();

category.Id = Guid.NewGuid();
category.Title = "Amazon AWS";
category.Url = "amazon-aws";
category.Summary = "AWS Cloud";
category.Order = 1;
category.Description = "Categoria destinada ao servicos do AWS";
category.Featured = true;

// NUNCA CONCATENE STRING, POIS FACILITA SQL INJECTION
// Nunca faça algo do tipo, $"... VALUES({category.Id}, {category.Title}...)
var insertSql = @"INSERT INTO 
    [Category] 
VALUES(
    @abacate, 
    @Title, 
    @Url, 
    @Summary, 
    @Order, 
    @Description, 
    @Featured
    )";

using (var connection = new SqlConnection(connectionString))
{
    var rows = connection.Execute(insertSql, new
    {
        abacate = category.Id, // abacate é só para exemplificar que pode ser qualquer nome
        category.Title, // mas se o nome for igual, não precisa atribuir.
        category.Url,
        category.Summary,
        category.Order,
        category.Description,
        category.Featured,
    });

    Console.WriteLine($"{rows} linha(s) inserida(s)");
}
```

## Fazendo um Update/Delete

```csharp
using BrochDataAccess.Models;
using Dapper;
using Microsoft.Data.SqlClient;

const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";

using (var connection = new SqlConnection(connectionString))
{
    UpdateCategory(connection);
    ListCategories(connection);
}

static void ListCategories(SqlConnection connection)
{
    var categories = connection.Query<Category>("SELECT [Id], [Title] FROM [Category]");

    foreach (var category in categories)
    {
        Console.WriteLine($"{category.Id} - {category.Title}");
    }
}

static void CreateCategory(SqlConnection connection)
{
    var category = new Category();

    category.Id = Guid.NewGuid();
    category.Title = "Amazon AWS";
    category.Url = "amazon-aws";
    category.Summary = "AWS Cloud";
    category.Order = 1;
    category.Description = "Categoria destinada ao servicos do AWS";
    category.Featured = true;

    // NUNCA CONCATENE STRING, POIS FACILITA SQL INJECTION
    var insertSql = @"INSERT INTO 
    [Category] 
VALUES(
    @abacate, 
    @Title, 
    @Url, 
    @Summary, 
    @Order, 
    @Description, 
    @Featured
    )";

    var rows = connection.Execute(insertSql, new
    {
        abacate = category.Id, // abacate é só para exemplificar que pode ser qualquer nome
        category.Title, // mas se o nome for igual, não precisa atribuir.
        category.Url,
        category.Summary,
        category.Order,
        category.Description,
        category.Featured,
    });

    Console.WriteLine($"{rows} linha(s) inserida(s)");
}

static void UpdateCategory(SqlConnection connection)
{
    var updateQuery = "UPDATE [Category] SET [Title]=@title WHERE [Id]=@id";
    int rows = connection.Execute(updateQuery, new
    {
        id = new Guid("06d73e6b-315f-4cfc-b462-f643e1a50e97"),
        title = "Mobile 2022"
    });

    // Se nao encontrar o id no banco, rows vai retornar 0 (ZERO)
    Console.WriteLine($"{rows} registros atualizados");
}

```

## Execute Many

Só passar um array de objetos para o método `Execute()`

```csharp
new[] { new{}, new{}, new{} }
```
```csharp
static void CreateManyCategory(SqlConnection connection)
{
    var category = new Category();

    category.Id = Guid.NewGuid();
    category.Title = "Amazon AWS";
    category.Url = "amazon-aws";
    category.Summary = "AWS Cloud";
    category.Order = 1;
    category.Description = "Categoria destinada ao servicos do AWS";
    category.Featured = true;

    var category2 = new Category();

    category2.Id = Guid.NewGuid();
    category2.Title = "Categoria Nova";
    category2.Url = "categoria-nova";
    category2.Summary = "categoria nova";
    category2.Order = 2;
    category2.Description = "Categoria destinada ao servicos do AWS";
    category2.Featured = true;

    // NUNCA CONCATENE STRING, POIS FACILITA SQL INJECTION
    var insertSql = @"INSERT INTO 
    [Category] 
VALUES(
    @abacate, 
    @Title, 
    @Url, 
    @Summary, 
    @Order, 
    @Description, 
    @Featured
    )";

    var rows = connection.Execute(insertSql, new[]{ // ARRAY DE OBJETOS
        new {
            abacate = category.Id,
            category.Title,
            category.Url,
            category.Summary,
            category.Order,
            category.Description,
            category.Featured,

        },
        new {
            abacate = category2.Id,
            category2.Title,
            category2.Url,
            category2.Summary,
            category2.Order,
            category2.Description,
            category2.Featured,

        }
    });

    Console.WriteLine($"{rows} linha(s) inserida(s)");
}


```

## Execuntado Stored Procedures

### procedure que não retorna nada (ex: delete, update, create)
```csharp
static void ExecuteStoredProcedure(SqlConnection connection)
{
    var procedure = "spDeleteStudent";

    var param = new { StudentId = "79b82071-80a8-4e78-a79c-92c8cd1fd052" };

    var affectedRows = connection.Execute(procedure, param, commandType: System.Data.CommandType.StoredProcedure);

    Console.WriteLine($"{affectedRows} linha(s) inserida(s)");
}
```

### procedure que retorna algo (ex: select)

```sql
CREATE OR ALTER PROCEDURE [spGetCoursesByCategory]
    @CategoryId UNIQUEIDENTIFIER
AS
    SELECT * FROM [Course] WHERE [CategoryId] = @CategoryId
```

```csharp
static void ExecuteReadStoredProcedure(SqlConnection connection)
{
    var procedure = "spGetCoursesByCategory";

    var param = new { CategoryId = "af3407aa-11ae-4621-a2ef-2028b85507c4" };

    var courses = connection.Query(procedure, param, commandType: System.Data.CommandType.StoredProcedure);
    
    // IEnumerable<Courses> courses = connection.Query<Courses>(); // O IDEAL é Criar um Tipo Courses para receber os dados da Query

    foreach (var item in courses)
    {
        Console.WriteLine(item.Title);
    }
}

```


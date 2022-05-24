# Conectando no banco usando ADONET

```csharp
const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";

```

## Instalando

Instalar o pacote `Microsoft.Data.SqlClient`

```sh
dotnet add package Microsoft.Data.SqlClient
```
Se precisar especificar a versão

```sh
dotnet add package Microsoft.Data.SqlClient --version 2.1.3
```

## Usando 

Não tão recomendado

```csharp
using Microsoft.Data.SqlClient;

const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";

var connection = new SqlConnection(connectionString);
connection.Open();

// DO things
// Insert
// Update

connection.Close();

connection.Dispose(); // O Dispose DESTRÓI o objeto connection

```

Prefira usar o `using`

```csharp
using Microsoft.Data.SqlClient;

const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";

using (var connection = new SqlConnection(connectionString))
{
    // DO things

}
```

```csharp
using Microsoft.Data.SqlClient;

const string connectionString = "Server=localhost,1433;Database=broch;User ID=sa;Password=1q2w3e4r@#$;TrustServerCertificate=True";

using (var connection = new SqlConnection(connectionString))
{
    Console.WriteLine("Conectado");

    connection.Open();

    using (var command = new SqlCommand())
    {
        command.Connection = connection;
        command.CommandType = System.Data.CommandType.Text;
        command.CommandText = "SELECT [Id], [Title] FROM [Category]";

        var reader = command.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine($"{reader.GetGuid(0)} - {reader.GetString(1)}");

        }
    }

}

```

Se estiver no linux, e der erro de plataforma, usar a flag

```sh
dotnet run -r linux-x64
```
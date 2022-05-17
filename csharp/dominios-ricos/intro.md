
## Criando a estrutura
<!-- 1975 006 -->
Criar pastas

```sh
PaymentContext
- PaymentContext.Domain
- PaymentContext.Shared
- PaymentContext.Tests
```

### dentro de `PaymentContext`

```sh
dotnet new sln
```
### dentro de `PaymentContext.Domain`

```sh
dotnet new classlib
```
depois de compilado, a class library vira uma dll

### dentro de `PaymentContext.Shared`

```sh
dotnet new classlib
```
depois de compilado, a class library vira uma dll

### dentro de `PaymentContext.Tests`

```sh
dotnet new mstest
```

### dentro de `PaymentContext`

```sh
dotnet sln add PaymentContext.Domain/PaymentContext.Domain.csproj
dotnet sln add PaymentContext.Shared/PaymentContext.Shared.csproj
dotnet sln add PaymentContext.Tests/PaymentContext.Tests.csproj
dotnet restore
dotnet build
```

### dentro de `PaymentContext.Domain`

```sh
dotnet add reference ../PaymentContext.Shared/PaymentContext.Shared.csproj
```

### dentro de `PaymentContext.Tests`

```sh
dotnet add reference ../PaymentContext.Domain/PaymentContext.Domain.csproj
dotnet add reference ../PaymentContext.Shared/PaymentContext.Shared.csproj
```

## 

## Installing 

### Manjaro

`sudo snap remove dotnet-sdk`

`sudo pacman -S dotnet-sdk`

`sudo pacman -Sy aspnet-runtime`

`sudo ln -sf /usr/share/dotnet/dotnet /usr/bin/dotnet`



## Starting projects
- `dotnet new console` -> Novo Cosole Application
- `dotnet new classlib` -> Nova class Library
- `dotnet new web` -> Novo projeto ASP.NET Core
- `dotnet new mvc` -> Novo projeto ASP.NET Core
- `dotnet new webapi` -> Novo projeto ASP.NET Core
- `dotnet new mstest` -> Novo projeto Microsoft Teste

## Basic Commands

Definições
- `dotnet restore`
- Restaura todos os pacotes que a aplicação precisa para ser executada

- `dotnet build`
- Compila a aplicação

- `dotnet clean`
- Limpa as compilações anteriores

- `dotnet run`
- Compila e executa a aplicação

## Dotnet RUN 

## Environment Variables

Definições
- Desta forma, podemos dizer ao .NET qual ambiente estamos utilizando
- `dotnet run --environment=$SEU AMBIENTE`
- `dotnet run --environment=development`
- `dotnet run --environment=production`
- O comando run não executa depuração (Debug)
- Neste modo sua aplicação não vai parar nos Break Points (Explicado adiante)

## Namespaces

Definições
- Enquanto as pastas são as divisões físicas
- Os namespaces são as divisões lógicas
- Assim como não podemos ter dois arquivos com mesmo nome nas pastas
- Não podemos ter duas classes com mesmo nome em um namespace
- O ideal é ter apenas um namespace e uma classe por arquivo
- O escopo de um namespace é definido entre CHAVES
  - Classes e métodos também
- Um namespace pode ser reutilizado
  - Pode estar presente em diversos arquivos
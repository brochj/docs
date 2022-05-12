
Baixar o sqlserver do docker.

Baixar o Azure Data studio

Subir o container

```sh
docker run --name sqlserver -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=1q2w3e4r@#$" -p 1433:1433 -d mcr.microsoft.com/mssql/server
```

Abrir o Azure e Conectar

```sh
Server: localhost,1433
user: sa 
password:

```

## Criando e removendo uma base de dados

```sql
CREATE DATABASE [Curso]

DROP DATABASE [Curso]
```

Caso de erro dizendo que o banco está em uso, usar o seguinte script

```sql
USE [master];

DECLARE @kill varchar(8000) = '';
SELECT @kill = @kill + 'kill ' + CONVERT(varchar(5), session_id)
FROM sys.dm_exec_sessions
WHERE database_id = db_id('Curso') -- MUDAR NOME 

EXEC(@kill);

DROP DATABASE [Curso] -- MUDAR NOME 
```

## Criando uma tabela

```sh
USE [Curso]

CREATE TABLE [Aluno](
    [Id] INT,
    [Name] NVARCHAR(80),
    [Nascimento] DATETIME,
    [Active] BIT,
)
GO
```

## Alterando tabela (adicionar coluna)

```sql 
USE [Curso]

ALTER TABLE [Aluno]
    ADD [Document] NVARCHAR(11)
```

## Removendo coluna

```sql 
ALTER TABLE [Aluno]
    DROP COLUMN [Document]
```

## Alterando tipo de dado da coluna

```sql
ALTER TABLE [Aluno]
    ALTER COLUMN [Document] CHAR(11)
```

## Constraits

```sql 
USE [Curso]

CREATE TABLE [Aluno](
    [Id] INT NOT NULL,
    [Name] NVARCHAR(80) NOT NULL,
    [Nascimento] DATETIME NOT NULL,
    [Active] BIT DEFAULT(0),
)
GO

```

Adicionando Constraints

```sql 
ALTER TABLE [Aluno]
    ALTER COLUMN [Active] BIT NOT NULL

```
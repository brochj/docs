
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

### Adicionando Constraints

```sql 
ALTER TABLE [Aluno]
    ALTER COLUMN [Active] BIT NOT NULL

```

### Unique

```sql
CREATE TABLE [Aluno](
    [Id] INT NOT NULL UNIQUE,
    [Name] NVARCHAR(80) NOT NULL,
    [Email] NVARCHAR(180) NOT NULL UNIQUE,
    [Nascimento] DATETIME NOT NULL,
    [Active] BIT,
)
GO
```

# Primary Key

```sql
CREATE TABLE [Aluno](
    [Id] INT NOT NULL,
    [Name] NVARCHAR(80) NOT NULL,
    [Email] NVARCHAR(180) NOT NULL,
    [Nascimento] DATETIME NOT NULL,
    [Active] BIT,

    PRIMARY KEY([Id]) 
    -- PRIMARY KEY([Id], [Email]) -- Chave composta
    -- CONSTRAINT [PK_Aluno] PRIMARY KEY([Id]) -- Nomeando a PK para PK_Aluno
    -- CONSTRAINT [UQ_Aluno_Email] UNIQUE([Email])


)
GO
```

### Adicionando uma PK

```sql
ALTER TABLE [Aluno]
    ADD PRIMARY KEY([Id])
```

### Removendo uma PK

```sql
ALTER TABLE [Aluno]
    DROP CONSTRAINT [PK_Aluno_]
```

## Curso

```sql
CREATE TABLE [Aluno](
    [Id] INT NOT NULL,
    [Name] NVARCHAR(80) NOT NULL,
    [Email] NVARCHAR(180) NOT NULL,
    [Nascimento] DATETIME NOT NULL,
    [Active] BIT NOT NULL DEFAULT(0),

    CONSTRAINT [PK_Aluno] PRIMARY KEY([Id]), 
    CONSTRAINT [UQ_Aluno_Email] UNIQUE([Email]), 
)
GO

CREATE TABLE [Curso] (
    [Id] INT NOT NULL IDENTITY(1,1),
    [Nome] NVARCHAR(80) NOT NULL,
    [CategoriaId] INT NOT NULL,

    CONSTRAINT [PK_Curso] PRIMARY KEY([Id]),
    CONSTRAINT [FK_Curso_Categoria] FOREIGN KEY([CategoriaId])
        REFERENCES [Categoria]([Id])
)
GO

CREATE TABLE [ProgressoCurso] (
    [AlunoId] INT NOT NULL,
    [CursoId] INT NOT NULL,
    [Progresso] INT NOT NULL,
    [UltimaAtualizacao] DATETIME NOT NULL DEFAULT(GETDATE()),

    CONSTRAINT PK_ProgressoCurso PRIMARY KEY([AlunoId], [CursoId])
)
GO

CREATE TABLE [Categoria] (
    [Id] INT NOT NULL,
    [Nome] NVARCHAR(80) NOT NULL,

    CONSTRAINT [PK_Categoria] PRIMARY KEY([Id])
)
GO

```

## Índices

Usar índices nas colunas que são feitas bastantes pesquisas

```sql
CREATE INDEX [IX_Aluno_Email] ON [Aluno]([Email])

DROP INDEX [IX_Aluno_Email] ON [Aluno]

```

## Identity

Usado para incrementar 

```sql
CREATE TABLE [Curso] (
    [Id] INT NOT NULL IDENTITY(1,1), -- Gera o Id Automaticamente incrementado de 1 em 1
    ....
```

```sql
CREATE TABLE [Curso] (
    [Id] UNIQUEIDENTIFIER NOT NULL, -- Gera o Id Automaticamente
    ....
```


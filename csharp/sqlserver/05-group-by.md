## GROUP BY

O COUNT, AVG, SUM, MAX, MIN retornam um valor. Quando queremos ter o resultado da soma de várias categorias diferentes, tem que usar o GROUP BY no final, referenciando tudo que foi pedido no SELECT.

```sql
SELECT TOP 100
    [Categoria].[Id],
    [Categoria].[Nome],
    COUNT([Curso].[CategoriaId]) AS [Cursos]
FROM
    [Categoria]
    INNER JOIN [Curso]
        ON [Curso].[CategoriaId] = [Categoria].[Id]
GROUP BY
    [Categoria].[Id],
    [Categoria].[Nome],
    [Curso].[CategoriaId]
```

| Id  |   Nome    | Cursos |
| :-: | :-------: | :----: |
|  1  |  Backend  |   2    |
|  2  | Frontend  |   1    |
|  3  | FullStack |   1    |

## HAVING

Selecionar os grupos dada uma condição

```sql
SELECT TOP 100
    [Categoria].[Id],
    [Categoria].[Nome],
    COUNT([Curso].[CategoriaId]) AS [Cursos]
FROM
    [Categoria]
    INNER JOIN [Curso]
        ON [Curso].[CategoriaId] = [Categoria].[Id]
GROUP BY
    [Categoria].[Id],
    [Categoria].[Nome],
    [Curso].[CategoriaId]
HAVING
    COUNT([Curso].[CategoriaId]) > 1
```

| Id  |  Nome   | Cursos |
| :-: | :-----: | :----: |
|  1  | Backend |   2    |

## VIEW

Uma VIEW é uma forma de abstrair um SELECT.

Isso é legal pois posso aplicar um SELECT em uma VIEW.

- As VIEWS Não podem ter ORDER BY dentro delas.

```sql
CREATE OR ALTER VIEW vwContagemCursosPorCategoria AS

    SELECT TOP 100
        [Categoria].[Id],
        [Categoria].[Nome],
        COUNT([Curso].[CategoriaId]) AS [Cursos]
    FROM
        [Categoria]
        INNER JOIN [Curso]
            ON [Curso].[CategoriaId] = [Categoria].[Id]
    GROUP BY
        [Categoria].[Id],
        [Categoria].[Nome],
        [Curso].[CategoriaId]
    HAVING
        COUNT([Curso].[CategoriaId]) > 1
```

Usando uma VIEW

```sql
SELECT * FROM vwContagemCursosPorCategoria
```

Vai retornar

| Id  |  Nome   | Cursos |
| :-: | :-----: | :----: |
|  1  | Backend |   2    |

```sql
SELECT * FROM vwContagemCursosPorCategoria
WHERE Id = 1
```

## Stored Procedures


```sql
CREATE OR ALTER PROCEDURE [spListCourse] AS
    SELECT * FROM [Curso]
```
Usando Stored Procedures

```sql
EXEC [spListCourse]
```
## Variáveis


```sql
CREATE OR ALTER PROCEDURE [spListCourse] AS
    DECLARE @Id INT
    SET @Id = 9
    SELECT * FROM [Curso] WHERE [Id] = @Id
```

```sql
CREATE OR ALTER PROCEDURE [spListCourse] AS
    DECLARE @CategoryId INT
    SET @CategoryId = (SELECT TOP 1 [Id] FROM [Categoria] WHERE [Nome] = 'backend')

    SELECT * FROM [Curso] WHERE [CategoriaId] = @CategoryId
```
Usando um parâmetro de entrada

```sql
CREATE OR ALTER PROCEDURE [spListCourse] 
    @Category NVARCHAR(80) -- Parametro que vou passar no EXEC
AS
    DECLARE @CategoryId INT
    SET @CategoryId = (SELECT TOP 1 [Id] FROM [Categoria] WHERE [Nome] = @Category)

    SELECT * FROM [Curso] WHERE [CategoriaId] = @CategoryId
```

```sql
EXEC [spListCourse] 'backend'
```
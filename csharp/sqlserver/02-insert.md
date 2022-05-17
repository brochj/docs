## Insert sqlserver

O id não precisa passar, pois vai ser gerado automaticamente

```sql
INSERT INTO [Categoria] ([Nome]) VALUES('Backend')
INSERT INTO [Categoria] ([Nome]) VALUES('Frontend')
INSERT INTO [Categoria] ([Nome]) VALUES('Mobile')

INSERT INTO [Curso] ([Nome],[CategoriaId]) VALUES('Fundamentos de C#', 1)
INSERT INTO [Curso] ([Nome],[CategoriaId]) VALUES('Fundamentos de OOP', 1)
INSERT INTO [Curso] ([Nome],[CategoriaId]) VALUES('Angular', 2)
INSERT INTO [Curso] ([Nome],[CategoriaId]) VALUES('Flutter', 3)
INSERT INTO [Curso] VALUES('Flutter e Sqlite', 3)
```

## SELECT

```sql
SELECT * FROM [Curso] -- EVITAR USAR
SELECT TOP 2 * FROM [Curso] -- EVITAR USAR *

SELECT TOP 2
    [Id],[Nome]
FROM
    [Curso]

-- Seleciona os top 100 ÚNICOS
SELECT DISTINCT TOP 100
    [Nome]
FROM
    [Categoria]
```

## Queries (WHERE)

```sql
SELECT  TOP 100
    [Id], [Nome], [CategoriaId]
FROM
    [Curso]
WHERE
    [Id] = 1 OR
    [CategoriaId] = 1
```

```sql
SELECT  TOP 100
    [Id], [Nome], [CategoriaId]
FROM
    [Curso]
WHERE
    [Id] IS NOT NULL OR
    [CategoriaId] IS NULL

```

## Order BY

```sql
SELECT  TOP 100
    [Id], [Nome], [CategoriaId]
FROM
    [Curso]
ORDER BY
    [Nome]
```

```sql
SELECT  TOP 100
    [Id], [Nome], [CategoriaId]
FROM
    [Curso]
ORDER BY
    [Nome], [Id], [CategoriaId] -- Ordem de ordenacao
```

```sql
SELECT  TOP 100
    [Id], [Nome], [CategoriaId]
FROM
    [Curso]
ORDER BY
    [Nome] DESC -- Z para A
    [Nome] ASC -- PADRÃO - A para Z
```

## Min, Max e Count

```sql
SELECT TOP 100
    MIN([Id])
FROM
    [Categoria]
```

```sql
SELECT TOP 100
    MAX([Id])
FROM
    [Categoria]
```

```sql
SELECT TOP 100
    COUNT([Id])
FROM
    [Categoria]
```

```sql
SELECT TOP 100
    AVG([Id])
FROM
    [Categoria]
```

```sql
SELECT TOP 100
    SUM([Id])
FROM
    [Categoria]
```


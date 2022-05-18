# JOIN

```sql
SELECT TOP 100 
    [Curso].[Id],
    [Curso].[Nome],
    [Categoria].[Id] AS [Categoria],
    [Categoria].[Nome]
FROM 
    [Curso]
    INNER JOIN [Categoria] 
        ON [Curso].[CategoriaId] = [Categoria].[Id]

    -- INNER JOIN [TabelaX] 
    --     ON [Curso].[TabelaId] = [Categoria].[Id]
    
```

## LEFT JOIN

Traz todos os items da primeira tabela, `[Cursos]`, e caso o curso não tenhas categoria, e coloca como `null`

```sql
SELECT TOP 100 
    [Curso].[Id],
    [Curso].[Nome],
    [Categoria].[Id] AS [Categoria],
    [Categoria].[Nome]
FROM 
    [Curso]
    LEFT JOIN [Categoria] 
        ON [Curso].[CategoriaId] = [Categoria].[Id]
```

## RIGHT JOIN

Traz todos os items da Segunda tabela, `[Categoria]`, e caso o curso não tenha Curso, e coloca como `null`

```sql
SELECT TOP 100 
    [Curso].[Id],
    [Curso].[Nome],
    [Categoria].[Id] AS [Categoria],
    [Categoria].[Nome]
FROM 
    [Curso]
    RIGHT JOIN [Categoria] 
        ON [Curso].[CategoriaId] = [Categoria].[Id]
```

## FULL OUTER JOIN

Traz tudo das tabelas

## UNION

Junta tudo caso apresentem as mesma colunas

TabelaX -> 3 Nomes
TabelaY -> 4 Nomes

O Union vai retornar uma coluna `[Nome]` com 7 linhas.

```sql
    SELECT TOP 100 
        [Id], [Nome]
    FROM 
        [Curso]
UNION
    SELECT TOP 100 
        [Id], [Nome]
    FROM 
        [Categoria]
```

## UNION ALL

Mesma coisa do UNION, porém ele vai remover as duplicatas

##
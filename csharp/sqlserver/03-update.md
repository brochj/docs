# Update

```sql
UPDATE
    [Categoria]
SET
    [Nome]=''
WHERE -- NAO PODE ESQUECER DO WHERE !!!!!! SEnÃO Atualiza a tabela inteira
    [Id] = 3
```

## Forma Recomendada

```sql
BEGIN TRANSACTION -- USAR QUANDO É POUCO DADOS

    UPDATE
        [Categoria]
    SET  -- o UPDATE Sempre precisa do SET!
        [Nome] = 'FullStack'
    WHERE -- NAO PODE ESQUECER DO WHERE
        [Id] = 3

-- ROLLBACK -- Desfaz as alterações, é bom usar, para ver quantas linhas de fato foram alteradas.
-- caso esteja ok, Trocar RollBack por Commit
COMMIT
```

## Delete

Tambem usar o `BEGIN TRANSACTION` para evitar problemas, fazer backup antes também.

```sql
DELETE FROM
    [Categoria]
WHERE
    [Id] = 3
```

Se tiver outras tabelas que usam o Categoria Id = 3, tem que excluí-las primeiro

```sql
DELETE FROM
    [Curso]
WHERE
    [CategoriaId] = 3

DELETE FROM
    [Categoria]
WHERE
    [Id] = 3
```

## LIKE

```sql
SELECT TOP 100
    [Nome]
FROM
    [Curso]
WHERE
    [Nome] LIKE 'Fundamentos%' -- Começa com com 'Fundamentos ...'
    -- [Nome] LIKE '%Fundamentos' -- Termina com com '... Fundamentos'
    -- [Nome] LIKE '%Fundamentos%' -- Todos que contém 'Fundamentos'
```

## IN, BETWEEN

```sql
SELECT TOP 100
    [Nome]
FROM
    [Curso]
WHERE
    [Id] IN (1, 3) -- Tras todos com Id = 1 e 3
```

```sql
SELECT TOP 100
    [Nome]
FROM
    [Curso]
WHERE
    [Id] BETWEEN 2 AND 21 -- Traz todos com Id entre 2 e 21
```

## Alias

```sql
SELECT TOP 100
    [Id] AS [Codigo],
    [Nome]
FROM
    [Curso]
```

```sql
SELECT TOP 100
    COUNT([Id]) AS [Total],
FROM
    [Curso]
```

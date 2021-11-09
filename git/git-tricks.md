Com o `-am` não precisa dar o `git add .` antes

```git
git commit -am "that was easy"
```

## Configurar alias (para encurtar comandos)

```git
git config --global alias.ac "commit -am"
```

`ac` é novo alias para `commit -am`

```git
git ac "that was easy"
```

## Change message of last commit

```git
git commit --amend -m "nice"
```

## Commitou mas esqueceu de adicionar alguns arquivos

```git
git add .
git commit --amend --no-edit
```

## Git Stash

Para salvar alterações sem comitá-las

```git
git stash
```

Salvando com um nove especifico

```git
git stash save coolstuff
```

Trazer as alterações de volta

```git
git pop
```

```git
git stash list
git stash apply <index>
git stash apply 0
```

## Git bisect

```git

```

## Git squash

```git

```

```git

```

```git

```

```git

```

```git

```

```git

```

```git

```

```git

```

```git

```

```git

```

```git

```

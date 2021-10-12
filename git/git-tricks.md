
Com o `-am` não precisa dar o `git add .` antes

```sh
git commit -am "that was easy"
```
## Configurar alias (para encurtar comandos)

```sh
git config --global alias.ac "commit -am"
```
`ac` é novo alias para `commit -am`

```sh
git ac "that was easy"
```

## Change message of last commit

```sh
git commit --amend -m "nice"
```
## Commitou mas esqueceu de adicionar alguns arquivos

```sh
git add .
git commit --amend --no-edit
```

## Git Stash

Para salvar alterações sem comitá-las
```sh
git stash
```

Salvando com um nove especifico

```sh
git stash save coolstuff
```

Trazer as alterações de volta

```sh
git pop
```

```sh
git stash list
git stash apply <index>
git stash apply 0
```

## Git bisect

```sh

```
## Git squash

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```

```sh

```
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

## Desfazer erro que foi comitado e foi para produção

Antes faça um backup para outra branch, só para garantir

```sh
git branch backup
``` 

Depois, **Certifique-se que você está na `main`**

`git log --oneline` para escolher para qual commit vai voltar

```sh
git log --oneline
```

`git reset --hard <commit-hash-escolhido>` Para voltar a branch main (LOCALMENTE)

```sh
git reset --hard <commit-hash>
```

`git push -f origin main` atualizar a `main` no repositório

- `-f` para forçar

```sh
git push -f origin main

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

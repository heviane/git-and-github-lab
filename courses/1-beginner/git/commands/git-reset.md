# Reset

## Desfazer o último commit

```bash
git reset --soft HEAD~1

git reset --mixed HEAD~1 # É o default, então pode ser omitido

git reset --hard HEAD~1

# Passando o hash do commit
git reset --hard e7c5d9e54fc42d719339add2af07c5c4c3008b14 # Nao
git reset 74d4c1997dd4c4f8da5b42f291133941b7dcbb33 # Nao


git reset --soft HEAD~1 # OK
git reset HEAD~1 # OK

# Remover um arquivo específico do commit anterior
git reset dir/file1.md
```

Evitar fazer isso após ter enviado o commit para o repositório remoto.

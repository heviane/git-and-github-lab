# Inicializa Diretório Git Local

Inicializa o diretório corrente como um diretório de controle de versão git local:

```bash
# Execute dentro do diretório desejado
git init
```

Cria o arquivo oculto `.git` dentro do diretório git.

```bash
# Visualizar diretórios e arquivos ocultos
ls -a

# Acessar o diretório do Git
cd .git

# Visualizar o conteúdo do arquivo config
cat config
```

- [core]: Refere-se ao repo local.
- [remote "origin"] e [branch "main"]: Refere-se ao repo remoto.

```bash
git remote -v # Exibe os repos remotos aos quais o repo local está vinculado

git remote add origin <URL do repositório remoto> # Vincular um repositório remoto ao repositório local
    # origin é o nome padrão para o repositório remoto, pode ser qualquer nome.
```

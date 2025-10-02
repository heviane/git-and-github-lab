# Branch (Ramo)

Branch é uma ramificação de um repositório.
É um ponteiro móvel para um commit no histórico do repositório.

Quando se cria uma nova branch a partir de outra branch existente, a nova se inicia apontando para o mesmo commit da branch que estava quando foi criada.

É uma prática comum usar a branch **main** (principal) para produção, e criar outras branches para as modificações, testes, etc.

```bash
# Cria e entra em uma nova branch chamada 'tests'
git checkout -b tests

git log
# commit e7c5d9e54fc42d719339add2af07c5c4c3008b14 (HEAD -> tests, main)

# Retorna para a branch principal (main)
git checkout main

# lista as branches e seus últimos commits
git branch -v

# mesclar branches (Mescla a branch 'tests' em 'main')
git merge tests

# Lista as branches
git branch

# Deleta a branch 'tests'
git branch -d tests # Error se eu estiver na branch 'tests'

```

## Conflitos de Merge

Acontece quando há alterações concorrentes.

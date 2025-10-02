# Desfazendo Alterações: `git revert` vs `git reset`

Quando você precisa desfazer um commit, o Git oferece duas ferramentas principais: `git reset` e `git revert`. A escolha entre elas depende de um fator crucial: **o commit já foi enviado para um repositório remoto compartilhado?**

## `git reset`: Reescrevendo o Histórico Local

O `git reset` é um comando poderoso que move a ponta de uma branch para um commit anterior, efetivamente "apagando" os commits que vieram depois dele do histórico da branch.

**Use `git reset` apenas em commits que ainda não foram enviados (`push`) para um repositório remoto.** Reescrever o histórico que já foi compartilhado com outros desenvolvedores pode causar grandes problemas de sincronização.

### Como usar

Para desfazer o último commit:

```bash
# Opção 1: Mantém as alterações no "staging area" (prontas para commitar)
# Útil para corrigir a mensagem do commit ou adicionar algo que esqueceu.
git reset --soft HEAD~1

# Opção 2 (Padrão): Mantém as alterações no "working directory" (não-staged)
# Útil para reavaliar as mudanças antes de criar um novo commit.
git reset --mixed HEAD~1 
# ou simplesmente
git reset HEAD~1

# Opção 3: Descarta completamente as alterações do commit
# CUIDADO: Esta ação não pode ser desfeita facilmente.
git reset --hard HEAD~1
```

`HEAD~1` refere-se ao commit anterior ao último.

---

## `git revert`: Criando um Novo Histórico Seguro

O `git revert` é a forma segura de desfazer alterações em um repositório compartilhado. Em vez de apagar commits, ele cria um **novo commit** que contém as alterações inversas ao commit que você quer desfazer.

Isso mantém o histórico do projeto intacto e transparente, mostrando que um commit foi feito e, depois, revertido.

**Use `git revert` para qualquer commit que já foi enviado (`push`) para o repositório remoto.**

### Como usar

Para reverter as alterações do último commit:

```bash
git revert HEAD
```

O Git abrirá seu editor de texto padrão para que você confirme a mensagem do commit de reversão. Após salvar e fechar o editor, um novo commit será criado. Depois, basta enviá-lo para o repositório remoto:

```bash
git push origin main
```

## Resumo Rápido

| Comando | Quando Usar | Efeito no Histórico | Efeito nas Alterações |
| :--- | :--- | :--- | :--- |
| `git reset` | Commits **locais** (não enviados com `push`) | Reescreve/Apaga commits | Depende do modo (`--soft`, `--mixed`, `--hard`) |
| `git revert` | Commits **compartilhados** (já enviados com `push`) | Adiciona um novo commit | Cria um commit com as alterações inversas |

---

↩️ Voltar para o Nível Intermediário
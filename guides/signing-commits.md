# Guia de Commits Assinados

Enviar commits assinados é uma prática de segurança que garante a autenticidade e a integridade das alterações enviadas para um repositório. O GitHub usa assinaturas GPG para verificar se um commit foi realmente feito por um usuário específico e se o código não foi alterado desde a sua criação.

## Por que Assinar Commits?

- **Autenticidade**: Prova que o commit foi feito por você.
- **Integridade**: Garante que o conteúdo do commit não foi adulterado.
- **Confiança**: Aumenta a confiança no histórico do projeto, especialmente em projetos de código aberto.

No GitHub, um commit assinado e verificado exibe um selo "Verified".

## Passo a Passo para Configurar Commits Assinados

### Passo 1: Gerar uma Chave GPG

Se você ainda não possui uma chave GPG, pode gerar uma nova.

1. **Instale o GnuPG**:
    Se necessário, instale o GnuPG. Para macOS, você tem duas opções principais:

    - **Via Homebrew (Recomendado para usuários de terminal)**:
      Se você usa o [Homebrew](https://brew.sh/), este é o método mais simples.

      ```bash
      brew install gnupg
      ```

    - **Via GPG Suite (Instalador com interface gráfica)**:
      O [GPG Suite](https://gpgtools.org/) instala não apenas o `gpg` para a linha de comando, mas também um conjunto de ferramentas gráficas para gerenciar suas chaves, o que pode ser útil para iniciantes. Basta baixar o instalador do site oficial e seguir as instruções.

2. **Gere a chave**:

    ```bash
    gpg --full-generate-key
    ```

3. **Siga as instruções**:
    - **Tipo de chave**: Aceite o padrão (`RSA and RSA`).
    - **Tamanho da chave**: Use `4096` bits para maior segurança.
    - **Validade**: Escolha um período de validade ou aceite o padrão (nunca expira).
    - **Dados do usuário**: Insira seu nome e o mesmo e-mail associado à sua conta do GitHub.
    - **Passphrase**: Crie uma senha forte para proteger sua chave.

### Passo 2: Adicionar a Chave Pública ao GitHub

#### ⚠️ Solução de Problemas: Aviso de Versão do `gpg-agent`

Se ao executar comandos `gpg` você receber o aviso `gpg: WARNING: server 'gpg-agent' is older than us`, isso significa que uma versão antiga do agente GPG está rodando. Isso geralmente acontece quando há múltiplas instalações do GnuPG (ex: uma via Homebrew e outra via GPG Suite).

Para resolver isso, force o agente a reiniciar com o comando abaixo. A nova versão será iniciada na próxima vez que for necessária.

```bash
gpg-connect-agent killagent /bye
```

Para uma solução permanente, é recomendado desinstalar uma das versões do GnuPG, mantendo apenas uma no sistema.

---

Retomando os passos:

1. **Listar suas chaves**: Encontre o ID da sua nova chave.

    ```bash
    gpg --list-secret-keys --keyid-format=long
    ```

    A saída mostrará algo como `sec rsa4096/872118ADFEA1517E`. O ID é `872118ADFEA1517E`.

2. **Exportar a chave pública**: Substitua `<KEY_ID>` pelo seu ID.

    ```bash
    gpg --armor --export <KEY_ID>
    ```

3. **Copie a chave**: Copie todo o bloco de texto, incluindo `-----BEGIN PGP PUBLIC KEY BLOCK-----` e `-----END PGP PUBLIC KEY BLOCK-----`.

4. **Adicionar ao GitHub**:
    - Vá para **Settings > SSH and GPG keys** na sua conta do GitHub.
    - Clique em **New GPG key**.
    - Cole a chave pública no campo de texto e salve.

### Passo 3: Configurar o Git

1. **Informar ao Git qual chave usar**:

    ```bash
    git config --global user.signingkey <KEY_ID>
    ```

2. **Habilitar a assinatura automática (recomendado)**:

    ```bash
    git config --global commit.gpgsign true
    ```

    Com essa configuração, todos os seus commits futuros serão assinados automaticamente.

### Passo 4: Fazer um Commit Assinado

Agora, o processo de commit é o mesmo de sempre.

```bash
git add .
git commit -S -m "feat: Adiciona nova funcionalidade com commit assinado"
```

Ao commitar, você pode ser solicitado a digitar a *passphrase* da sua chave GPG.

Se você não configurou a assinatura automática (passo 3.2), use a flag `-S` para assinar um commit específico:

```bash
git commit -S -m "docs: Atualiza documentação"
```

Após enviar o commit para o GitHub (`git push`), você verá o selo "Verified" ao lado dele.

## Passo a Passo para Desfazer Commits Assinados

Para desabilitar a assinatura GPG e fazer o Git voltar ao comportamento padrão, execute os seguintes comandos no seu terminal:

Desabilitar a assinatura automática de commits: Este comando remove a configuração que obriga o Git a assinar todos os commits.

```bash
git config --global --unset commit.gpgsign
```

Remover a associação da chave de assinatura: Este comando desvincula a sua chave GPG do Git.

```bash
git config --global --unset user.signingkey
```

Pronto! Após executar esses dois comandos, seu Git não tentará mais assinar os commits automaticamente. Você poderá fazer commits normalmente, como antes.

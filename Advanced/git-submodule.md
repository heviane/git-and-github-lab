# Sub Módulos Git

A abordagem com git submodule é muito poderosa, mas brilha mais em cenários onde um projeto depende do código de outro para funcionar (ex: uma biblioteca compartilhada entre vários projetos).

```bash
# Adicionar o link do seu outro repositório.
git submodule add <URL_repositório> <diretório_local>
```

O Git criaria um arquivo .gitmodules para rastrear essa dependência.
Quem clonar o seu repositório poderá, com um comando extra, baixar também todo o conteúdo do outro repositório linkado.

Vantagens:

- Conteúdo integrado: O código do repo linkado fica disponível diretamente para quem clona o repositório principal (usando `git clone --recurse-submodules`).
- Versionamento: O repositório principal "trava" em uma versão (commit) específica do submódulo, garantindo consistência.

Desvantagens:

- Complexidade: Adiciona uma camada de complexidade ao projeto. Os colaboradores precisam aprender a trabalhar com submódulos (`git submodule update`, etc.).

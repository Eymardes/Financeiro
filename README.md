# Financeiro

App simples de organização financeira pessoal: receitas, despesas parceladas, assinaturas recorrentes, dívidas, histórico e resumo mensal/anual. Roda direto no navegador, sem servidor, sem instalação.

## Como usar

1. Baixe o repositório (ou apenas o arquivo `financeiro.html`).
2. Abra `financeiro.html` no **Chrome** ou **Edge** (clique duas vezes no arquivo).
3. Use as abas no topo:
   - **A Receber** — cadastre receitas (salário, freelance, etc.)
   - **A Pagar** — cadastre despesas (cartão, contas, assinaturas)
   - **Devendo** — registre dívidas a receber/pagar sem data fixa
   - **Histórico** — parcelas já marcadas como pagas
   - **Resumo** — totais gerais, do mês e do ano
   - **Calendário** — visão por mês de tudo que está agendado

## Tipos de lançamento

- **Parcelado** — valor total dividido em N parcelas (ex.: compra em 6x no cartão).
- **Recorrente** — valor mensal, com ou sem data final (ex.: Netflix). Sem data final = recorrência indefinida; o "Total a Pagar" do Resumo só conta a parcela do mês atual.

## Salvar e restaurar dados

Os dados ficam no `localStorage` do navegador por padrão. Para não depender disso:

- **⬇ Baixar backup** — baixa um JSON com todos os dados (funciona em qualquer navegador).
- **📥 Carregar do arquivo** — restaura a partir de um JSON.
- **📁 Conectar pasta** — usa a [File System Access API](https://developer.mozilla.org/docs/Web/API/File_System_Access_API) para sincronizar com uma pasta local (`data/` ao lado do HTML, por exemplo). Só funciona em Chrome/Edge/Opera.
- **💾 Salvar dados** — grava o estado atual no `database.json` da pasta conectada e cria um `backup-DATA.json` datado. Se não houver pasta conectada, faz download do JSON.

A pasta `data/` está incluída no `.gitignore`, então seu banco fica fora do controle de versão.

## Estrutura do projeto

```
financeiro.html    # o app inteiro (HTML + CSS + JS em um arquivo)
data/              # banco local — criado por você, ignorado pelo git
  database.json    # estado atual (gerado pelo botão "Salvar dados")
  backup-*.json    # snapshots datados
README.md
.gitignore
```

## Tecnologias

HTML + CSS + JavaScript puro. Sem build, sem dependências, sem framework. Persistência via `localStorage` + opcional File System Access API.

## Limitações

- File System Access API não funciona no Firefox e Safari (use Chrome ou Edge para a integração com pasta).
- Permissão de pasta é por sessão — o navegador pode pedir autorização novamente ao reabrir.
- O salvamento no arquivo não é automático: clique em **Salvar dados** para gravar.

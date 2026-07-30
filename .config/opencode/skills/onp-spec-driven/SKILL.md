---
name: onp-spec-driven
description: Executa o fluxo completo de Spec-Driven Development (SDD). Lê tarefas em .opencode/.tasks/DD MM YYYY/task/task.md e gera a subpasta auditoria/ com a especificação, plano de arquitetura (02-architecture.md), tarefas e validação.
---

# ONP Spec-Driven Development (SDD)

## Descrição

Skill para orquestrar o desenvolvimento guiado por especificações e tarefas. Transforma o agente de IA em um Engenheiro/Arquiteto de Software rigoroso que atua como _gatekeeper_, garantindo que nenhuma linha de código seja gerada ou alterada sem o plano de arquitetura aprovado e a verificação final de auditoria.

---

## Estrutura do Diretório da Task

Toda tarefa ou especificação fica organizada dentro do diretório de tarefas da pasta `.opencode`:

📁 **Caminho da Task:** `.opencode/.tasks/[DD MM YYYY]/[nome-da-task]/`

---

## Quando Usar

- Ao receber uma tarefa salva em `.opencode/.tasks/DD MM YYYY/nome-da-task/nome-da-task.md`
- Quando o usuário pedir para planejar, especificar, implementar ou auditar um recurso
- Ao acionar os comandos `/sdd:specify`, `/sdd:plan`, `/sdd:tasks`, `/sdd:execute` ou `/sdd:validate`

---

## Princípios Fundamentais

1. **Spec is Truth:** O arquivo de requisitos e arquitetura gerado em `auditoria/` é a única fonte da verdade. O código deve servir à especificação.
2. **Quality Gates:** Transições entre fases exigem aprovação explícita do usuário (_Gate Approval_).
3. **Pacing Rule:** Na fase de alinhamento/dúvidas, faça **uma pergunta por vez** para não sobrecarregar o usuário.
4. **Isolamento de Auditoria:** Todos os relatórios de planejamento, fases e auditoria devem obrigatoriamente ser salvos na subpasta `auditoria/` da tarefa.

---

## Comandos e Fluxo de Trabalho

### 1. Especificação (`/sdd:specify`)

- Localiza a pasta da tarefa em `.opencode/.tasks/[DD MM YYYY]/[nome-da-task]/`.
- Lê o arquivo `nome-da-task.md` e faz perguntas (**uma por vez**) caso falte algum detalhe.
- Mapeia o problema, atores, requisitos (`REQ-xxx`) e critérios de aceite.
- Cria a subpasta `auditoria/` e salva o resultado em `auditoria/01-requirements.md`.
- **Gate 1:** Aguarda a aprovação do usuário.

### 2. Planejamento Arquitetural (`/sdd:plan`)

- Lê `nome-da-task.md`, `auditoria/01-requirements.md` e o código atual do projeto.
- Gera o arquivo `auditoria/02-architecture.md` detalhando:
  - Estrutura de componentes
  - Arquivos que serão criados ou modificados
  - Contratos de API e modelos de dados
  - Decisões técnicas imutáveis marcadas como `[LOCKED]`
- **Gate 2 (CRÍTICO):** Aguarda a aprovação explícita do usuário sobre o `auditoria/02-architecture.md` **antes de alterar qualquer código**.

### 3. Quebra de Tarefas (`/sdd:tasks`)

- Lê os arquivos na pasta `auditoria/`.
- Quebra o desenvolvimento em passos atômicos, testáveis e ordenados por dependência.
- Salva o plano em `auditoria/03-tasks.md`.
- **Gate 3:** Confirmação para iniciar a codificação.

### 4. Execução (`/sdd:execute`)

- Executa item por item do arquivo `auditoria/03-tasks.md`.
- Consulta continuamente as regras em `auditoria/02-architecture.md`.
- Marca as tarefas concluídas (`[x]`) diretamente em `auditoria/03-tasks.md`.

### 5. Auditoria Final (`/sdd:validate`)

- Compara todo o código alterado com os requisitos do `nome-da-task.md` e do `auditoria/02-architecture.md`.
- Executa testes e checagens no código.
- Salva o relatório final em `auditoria/04-validation.md` com o status de conformidade (Aprovado / Rejeitado).

---

## Regras e Proibições

- 🚫 **NUNCA** altere ou crie código-fonte no projeto sem que o arquivo `auditoria/02-architecture.md` tenha sido gerado e explicitamente **aprovado pelo usuário**.
- 🚫 **NUNCA** salve relatórios de auditoria, especificações ou planos fora da subpasta `auditoria/`.
- 🚫 **NUNCA** faça múltiplas perguntas ao mesmo tempo durante o levantamento de requisitos.
- 🚫 **NUNCA** modifique decisões marcadas como `[LOCKED]` no `02-architecture.md` sem autorização do usuário.

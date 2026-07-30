---
name: session-init
description: Inicialização automática de sessão - lê arquivos de configuração, memória, contexto SDD e gerencia sessões
---

## O que eu faço

Ao iniciar uma sessão, automaticamente:
1. Ler `C:\Users\Acer\.config\opencode\rules\rules_inviolable.md` (REGRAS ABSOLUTAS - PRIMEIRO!)
2. Ler `C:\Users\Acer\.config\opencode\opencode.md`
3. Ler `C:\Users\Acer\.config\opencode\memorys\memory.md`
4. **Criar nova sessão** (usando session-manager)
5. **Ler últimas 3 sessões** para contexto
6. Verificar se existe tarefa SDD ativa em `.opencode/.tasks/`
7. Se existir, ler os arquivos de auditoria mais recentes:
   - `auditoria/01-requirements.md` (se existir)
   - `auditoria/02-architecture.md` (se existir - PLANO APROVADO)
   - `auditoria/03-tasks.md` (se existir - status das tarefas)
   - `auditoria/04-validation.md` (se existir - resultado da validação)
8. Exibir a mensagem de confirmação

## Fluxo de Sessão (OBRIGATÓRIO)

### Passo 1: Criar Nova Sessão

1. Listar arquivos `session-*.json` em `C:\Users\Acer\.config\opencode\sessions\`
2. Encontrar próximo ID sequencial (maior número + 1)
3. Criar arquivo `session-XXX.json` com:
   ```json
   {
     "id": "session-XXX",
     "startedAt": "[data/hora atual ISO]",
     "endedAt": null,
     "status": "active",
     "logs": [
       {
         "type": "info",
         "message": "Sessão iniciada",
         "timestamp": "[data/hora atual ISO]"
       }
     ],
     "context": {
       "tasksCompleted": [],
       "errors": [],
       "decisions": []
     }
   }
   ```
4. Salvar em `C:\Users\Acer\.config\opencode\sessions\session-XXX.json`

### Passo 2: Ler Últimas 3 Sessões

1. Listar todos os arquivos `session-*.json`
2. Ordenar por `startedAt` decrescente
3. Pegar os 3 primeiros (excluindo a recém-criada se for a mais recente)
4. Para cada sessão, extrair:
   - ID
   - Data início/fim
   - Status
   - Últimos 5 logs
   - Resumo do context
5. Exibir resumo formatado

### Passo 3: Exibir Contexto

```
📚 Contexto das Últimas Sessões:

1. session-005 - 28/07/2026
   Status: Finalizada | Duração: 2h30min
   Últimos logs: Componente X criado, Teste Y passou

2. session-004 - 28/07/2026
   Status: Finalizada | Duração: 4h15min
   Tarefas: Refatoração do service Z
   Erros: Timeout na API

3. session-003 - 27/07/2026
   Status: Finalizada | Duração: 8h30min
   Tarefas: Implementação do módulo W
   Decisões: Migração para signals
```

## Mensagem de Confirmação

Sem tarefa SDD:
```
✅ Arquivos carregados com sucesso:
- opencode.md ✓
- memory.md ✓
- Sessão: session-XXX criada ✓
- Últimas sessões: [X] carregadas ✓

Olá Tudo bem Sr, IABADABADUUUUU
```

Com tarefa SDD ativa:
```
✅ Arquivos carregados com sucesso:
- opencode.md ✓
- memory.md ✓
- Sessão: session-XXX criada ✓
- Últimas sessões: [X] carregadas ✓
- Tarefa SDD: [nome-da-task] ✓
  - Requisitos: [status]
  - Arquitetura: [Aprovada/Pendente]
  - Tarefas: [X/Y concluídas]
  - Validação: [status]

Olá Tudo bem Sr, IABADABADUUUUU
```

## Logar Durante a Sessão

Ao longo da sessão, logar automaticamente no arquivo da sessão atual:

### Erros
Quando um erro ocorrer:
```json
{
  "type": "error",
  "message": "[descrição do erro]",
  "timestamp": "[data/hora atual ISO]"
}
```

### Acertos/Sucessos
Quando uma tarefa for concluída com sucesso:
```json
{
  "type": "success",
  "message": "[descrição do sucesso]",
  "timestamp": "[data/hora atual ISO]"
}
```

### Decisões
Quando uma decisão técnica for tomada:
```json
{
  "type": "info",
  "message": "Decisão: [descrição da decisão]",
  "timestamp": "[data/hora atual ISO]"
}
```

### Alertas
Quando um problema potencial for detectado:
```json
{
  "type": "warning",
  "message": "[descrição do alerta]",
  "timestamp": "[data/hora atual ISO]"
}
```

## Finalizar Sessão

Quando o usuário encerrar ou ao final do chat:

1. Atualizar arquivo da sessão atual:
   - `endedAt`: data/hora atual ISO
   - `status`: "finalized"
2. Adicionar log final:
```json
{
  "type": "info",
  "message": "Sessão finalizada",
  "timestamp": "[data/hora atual ISO]"
}
```
3. Salvar alteração

## Comandos do Usuário

### /sessions
- Lista todas as sessões registradas
- Sessão atual em verde com "(ATUAL)"
- Sessões finalizadas em cinza

### /resume <id>
- Retoma sessão específica
- Exibe resumo da sessão
- Adiciona log de retomada

## Quando usar

- Toda vez que uma nova sessão for iniciada
- Antes de processar qualquer prompt do usuário
- O agente DEVE sempre chamar este skill no início

## Regras

- IDs sempre sequenciais com 3 dígitos (session-001, session-002, ...)
- Nunca deletar sessões (manter histórico completo)
- Datas sempre em formato ISO 8601 no JSON
- Exibição sempre em formato brasileiro (DD/MM/AAAA HH:MM)
- Logar TUDO que seja relevante: erros, acertos, decisões, alertas
- Só pode haver 1 sessão ativa por vez (status=active)
- Ler APENAS os arquivos de auditoria que existirem
- Nunca criar arquivos de auditoria - apenas ler os existentes
- Priorizar `02-architecture.md` se existir (é o plano aprovado)
- Se houver múltiplas pastas de tarefa, usar a mais recente

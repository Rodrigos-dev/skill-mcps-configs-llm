---
name: session-manager
description: Gerencia sessões do Gemini - criar, listar, retomar, finalizar e logar erros/acertos
---

## O que eu faço

Gerencio o ciclo de vida completo das sessões do Gemini, mantendo um histórico persistente com contexto.

## Estrutura de Armazenamento

```
C:\Users\Acer\.gemini\sessions\
├── session-001.json
├── session-002.json
└── ...
```

## Formato do Arquivo de Sessão

```json
{
  "id": "session-XXX",
  "startedAt": "2026-07-28T14:30:00.000Z",
  "endedAt": null,
  "status": "active",
  "logs": [
    {
      "type": "info|success|error|warning",
      "message": "Descrição do evento",
      "timestamp": "2026-07-28T14:30:00.000Z"
    }
  ],
  "context": {
    "tasksCompleted": ["Tarefa 1", "Tarefa 2"],
    "errors": ["Erro 1"],
    "decisions": ["Decisão 1"]
  }
}
```

## Comandos Disponíveis

### /sessions - Listar Sessões

Ao receber `/sessions`:

1. Ler todos os arquivos `session-*.json` na pasta `sessions/`
2. Ordenar por data de início (mais recente primeiro)
3. Exibir lista formatada:

```
📋 Sessões Registradas:

🟢 session-005 - 28/07/2026 14:30 (ATUAL)
   Status: Em andamento | Logs: 12

⚪ session-004 - 28/07/2026 10:15 - 28/07/2026 12:45
   Status: Finalizada | Duração: 2h30min | Logs: 8

⚪ session-003 - 27/07/2026 09:00 - 27/07/2026 17:30
   Status: Finalizada | Duração: 8h30min | Logs: 25
```

**Regras de Exibição:**
- Sessão atual (status=active): 🟢 verde + "(ATUAL)"
- Sessões finalizadas: ⚪ cinza
- Data/hora no formato brasileiro: DD/MM/AAAA HH:MM
- Duração calculada quando finalizada

### /resume <id> - Retomar Sessão

Ao receber `/resume session-XXX`:

1. Verificar se o arquivo existe
2. Se não existir: `❌ Sessão não encontrada: session-XXX`
3. Se existir:
   - Ler conteúdo completo da sessão
   - Exibir resumo da sessão:
   ```
   📂 Retomando sessão: session-003
   📅 Início: 27/07/2026 09:00
   ⏱️ Duração até agora: 8h30min
   📝 Logs: 25 registros
   🎯 Tarefas concluídas: 5
   ⚠️ Erros: 2
   ```
   - Adicionar log de retomada:
   ```json
   {
     "type": "info",
     "message": "Sessão retomada pelo usuário",
     "timestamp": "2026-07-28T15:00:00.000Z"
   }
   ```
   - Salvar alteração no arquivo
   - Retornar contexto completo para o agente usar

### Criar Nova Sessão (Automático)

Ao iniciar sessão (chamado pelo session-init):

1. Verificar sessões existentes na pasta `sessions/`
2. Gerar próximo ID sequencial: `session-XXX` (XXX = número com 3 dígitos)
3. Criar arquivo com:
   - `id`: próximo número
   - `startedAt`: data/hora atual ISO
   - `endedAt`: null
   - `status`: "active"
   - `logs`: array com log inicial
   - `context`: objeto vazio
4. Salvar em `C:\Users\Acer\.gemini\sessions\session-XXX.json`
5. Retornar o ID da sessão criada

### Logar Eventos (Automático)

Durante a sessão, logar automaticamente:

**Erros:**
```json
{
  "type": "error",
  "message": "Falha ao compilar componente X: erro de tipagem",
  "timestamp": "2026-07-28T14:35:00.000Z"
}
```

**Acertos/Sucessos:**
```json
{
  "type": "success",
  "message": "Componente criado com sucesso: user-card",
  "timestamp": "2026-07-28T14:40:00.000Z"
}
```

**Decisões:**
```json
{
  "type": "info",
  "message": "Decisão: Usar signals em vez de observáveis para estado",
  "timestamp": "2026-07-28T14:45:00.000Z"
}
```

**Alertas:**
```json
{
  "type": "warning",
  "message": "Detectada duplicação entre services X e Y",
  "timestamp": "2026-07-28T14:50:00.000Z"
}
```

### Finalizar Sessão (Automático)

Quando o usuário encerrar ou ao final do dia:

1. Atualizar arquivo da sessão atual:
   - `endedAt`: data/hora atual ISO
   - `status`: "finalized"
2. Adicionar log final:
```json
{
  "type": "info",
  "message": "Sessão finalizada",
  "timestamp": "2026-07-28T18:00:00.000Z"
}
```
3. Salvar alteração

## Ler Últimas 3 Sessões (Para Contexto)

Ao iniciar sessão, ler as 3 mais recentes para contexto:

1. Listar arquivos `session-*.json` na pasta `sessions/`
2. Ordenar por `startedAt` decrescente
3. Pegar os 3 primeiros
4. Para cada sessão, extrair:
   - ID
   - Data início/fim
   - Status
   - Últimos 5 logs
   - Resumo do context (tarefas, erros, decisões)
5. Exibir resumo:
```
📚 Contexto das Últimas Sessões:

1. session-005 (ATUAL) - 28/07/2026
   Últimos logs: Componente X criado, Teste Y passou

2. session-004 - 28/07/2026
   Tarefas: Refatoração do service Z
   Erros: Timeout na API

3. session-003 - 27/07/2026
   Tarefas: Implementação do módulo W
   Decisões: Migração para signals
```

## Quando usar

- `/sessions` - Lista todas as sessões
- `/resume <id>` - Retoma sessão específica
- Automaticamente ao iniciar sessão (criar + ler contexto)
- Automaticamente ao finalizar sessão

## Regras

- IDs sempre sequenciais com 3 dígitos (session-001, session-002, ...)
- Nunca deletar sessões (manter histórico completo)
- Datas sempre em formato ISO 8601 no JSON
- Exibição sempre em formato brasileiro (DD/MM/AAAA HH:MM)
- Logar TUDO que seja relevante: erros, acertos, decisões, alertas
- Só pode haver 1 sessão ativa por vez (status=active)

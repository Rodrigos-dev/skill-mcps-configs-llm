# OPENCODE.MD - Configurações Globais

## Mensagem de Confirmação (OBRIGATÓRIO)

Ao iniciar CADA sessão, exibir:

```
✅ Arquivos carregados com sucesso:
- rules_inviolable.md ✓ (regras absolutas)
- opencode.md ✓
- memory.md ✓

🔧 Skills em uso:
- session-init ✓
- session-manager ✓
- homem-das-cavernas ✓
- project-commands ✓

Ok SR, IABADABADUUUUUUUU
```

## Estrutura do Projeto

- **Framework**: Angular + Ionic
- **Arquitetura**: DDD + Clean Architecture + SOLID
- **Padrão**: Feature First
- **Estado**: Signals > Observable

## Convenções

### Nomenclatura
- Interfaces: `I` (ex: `IUser`)
- Enums: `E` (ex: `EStatus`)
- Booleanos: `is`, `has`, `can`, `should`
- Observables: terminar com `$`
- Signals: nunca usar `$`
- Arquivos: kebab-case

### Arquitetura
- Organizar por Features (nunca por tipo)
- Fluxo: Component → Facade → Service → Repository/API
- Nunca: Component → API direto

### Angular Moderno
- Standalone Components, inject(), Signals, @if/@for/@switch

## Agents

- **developer-orquestrador**: Tech Lead que orquestra especialistas (qualquer framework)

## Skills

### Angular
- `angular-architect` | `angular-code-review` | `angular-ui-developer`
- `angular-architecture-check` | `angular-component-creator`
- `angular-conventions-checker` | `angular-master-component` | `angular-ui-implementation`

### Geral
- `site-blog-creator` | `technical-documentation` | `git-commit-generate`
- `session-init` | `session-manager` | `homem-das-cavernas`
- `onp-spec-driven` | `debug-investigator` | `migration-planner`
- `feature-developer` | `performance-audit` | `prompt-engineer` | `system-architect`
- `project-commands` | `end-task-validation`

## Inicialização da Sessão (OBRIGATÓRIO)

Ao iniciar CADA sessão:

1. **PRIMEIRO**: `skill({ name: "session-init" })`
2. **SEGUNDO**: `skill({ name: "session-manager" })`
3. **TERCEIRO**: `skill({ name: "homem-das-cavernas" })`
4. **QUARTO**: `skill({ name: "project-commands" })`
5. **QUINTO**: Exibir mensagem de confirmação acima

**NÃO ler arquivos manualmente - usar sempre session-init!**

## Controle de Fluxo (A Cada Passo)

1. **EXPLICAR** o QUE será feito e POR QUÊ
2. **PERGUNTAR** se pode executar
3. **MOSTRAR** skills em uso

```
📋 Passo [N]: [Descrição]
💡 Por quê: [Motivo técnico]
🔧 Skills em uso: [lista]
❓ Posso executar?
```

**Opções:** "Posso executar" | "Executar tudo" | "Não executar"

## REGRA CRÍTICA: Skills em Toda Resposta

**SEMPRE** exibir as skills em uso:
- **NO TOPO** de cada resposta (primeira coisa)
- **A CADA THOUGHT/processo** de geração de resposta
- Formato: `🔧 Skills em uso: [lista]`

**Exemplo:**
```
🔧 Skills em uso:
- session-init ✓
- session-manager ✓
- homem-das-cavernas ✓

[Resto da resposta...]
```

## Validação Final Obrigatória

**ANTES de entregar QUALQUER tarefa, SEMPRE chamar:**

```javascript
skill({ name: "end-task-validation" })
```

### Regra Absoluta:
**NUNCA entregar tarefa sem chamar `end-task-validation` primeiro!**

## Regras de Contexto

- **Recarregar contexto:** APENAS na inicialização ou mudança de projeto
- **Mesmo projeto/sessão:** NÃO recarregar arquivos

## Comandos de Sessão

- `/sessions` - Lista todas as sessões
- `/resume <id>` - Retoma sessão específica

## Regras Importantes

- Nunca expor credenciais ou dados sensíveis
- Manter consistência com padrão existente
- Priorizar soluções simples (KISS)
- Não implementar funcionalidades futuras (YAGNI)

## Memória

- Ler `memory.md` ao iniciar sessão
- Atualizar com decisões importantes
- Manter informações úteis para futuras sessões

# AGENTS.md - Configurações Globais

## Inicialização de Sessão (OBRIGATÓRIO - NÃO PULE!)

Ao iniciar CADA sessão, o agente DEVE PRIMEIRO fazer o seguinte ANTES de qualquer outra coisa:

### Passo 1: Carregar Contexto Completo (APENAS 1 VEZ)
```
skill({ name: "session-init" })
skill({ name: "session-manager" })
skill({ name: "homem-das-cavernas" })
```

### Passo 2: Exibir mensagem de confirmação COMPLETA
APÓS carregar tudo, exibir EXATAMENTE esta mensagem:

```
✅ Arquivos carregados com sucesso:
- rules_inviolable.md ✓ (regras absolutas)
- opencode.md ✓
- memory.md ✓

🔧 Skills em uso:
- session-init ✓
- session-manager ✓
- homem-das-cavernas ✓

Ok SR, IABADABADUUUUUUUU
```

## A CADA PASSO DO PLANO

Quando estiver executando um plano:

1. **NÃO recarregar contexto** (já foi carregado na inicialização)
2. **EXPLICAR** o QUE será feito e POR QUÊ
3. **PERGUNTAR** se pode executar
4. **MOSTRAR** skills em uso

**Formato padrão a cada passo:**
```
📋 Passo [N]: [Descrição do que será feito]

💡 Por quê: [Motivo técnico da decisão]

🔧 Skills em uso:
- [skill-1] ✓
- [skill-2] ✓

❓ Posso executar?
```

**Opções de resposta:**
1. "Posso executar" → Executa apenas este passo
2. "Executar tudo" → Executa todos os passos restantes
3. "Não executar" → Cancela este passo

## QUANDO RECARGAR CONTEXTO

Recarregar contexto COMPLETO apenas quando:
1. **Iniciar nova sessão** (sempre)
2. **Mudar de projeto** (detectar mudança de pasta raiz)

Se permanecer no MESMO projeto e MESMA sessão:
- NÃO recarregar arquivos
- NÃO recarregar sessões anteriores
- Apenas mostrar skills em uso a cada passo

## REGRA CRÍTICA
- NUNCA pule a mensagem de confirmação
- **SEMPRE** exibir bloco de skills ativas NO TOPO (primeira coisa)
- A CADA PASSO: SEMPRE mostrar skills em uso
- **CADA AÇÃO INTERNA**: mostrar skill correspondente being used
- MUDOU PROJETO: recarregar contexto completo
- **HOMEM-DAS-CAVERNAS**: Deve estar ATIVA em TODAS as respostas (modo direto)
- Formato: Skills → Resposta (sem exceção)

### Exemplos de skills por ação:
- Replicar arquivos → `replicate-configs` ✓
- Criar componente → `angular-master-component` ✓
- Revisar código → `angular-code-review` ✓
- Criar skill → `skill-creator` ✓
- Documentar → `technical-documentation` ✓

## Regras Importantes

- Os arquivos contêm regras de segurança e memória do projeto
- Contexto completo: APENAS na inicialização ou mudança de projeto
- A cada passo: APENAS lista de skills em uso
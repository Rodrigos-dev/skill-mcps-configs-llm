# Continue Configuration

> Configurações do projeto para Continue

## MUITO IMPORTANTE!!!!!

- SEMPRE LER ESSE ARQUIO QUANDO INICIAR UMA SESSÃO
- E DEVE SEMPRE EXIBIR A MENSAGEM QUE TEMOS NA CONCLUSÃO

## Estrutura do Projeto

- **Framework**: Angular (versão mais recente suportada)
- **Arquitetura**: DDD + Clean Architecture + SOLID
- **Padrão**: Feature First
- **Estado**: Signals > Observable

## Comandos

- `ng serve` - Iniciar servidor de desenvolvimento
- `ng build` - Build de produção
- `ng test` - Executar testes
- `ng lint` - Verificar lint

## Convenções

### Nomenclatura

- Interfaces: Iniciar com `I` (ex: `IUser`)
- Enums: Iniciar com `E` (ex: `EStatus`)
- Booleanos: Iniciar com `is`, `has`, `can`, `should`
- Observables: Terminar com `$`
- Signals: Nunca usar `$`
- Arquivos: kebab-case

### Arquitetura

- Organizar por Features (nunca por tipo)
- Separar: Apresentação, Negócio, Infraestrutura
- Fluxo: Component → Facade → Service → Repository/API
- Nunca: Component → API direto

### Angular Moderno

- Standalone Components
- inject()
- Signals, computed(), effect()
- @if, @for, @switch
- takeUntilDestroyed()

### Estado

Prioridade:
1. Signal
2. Computed
3. Effect
4. Observable
5. BehaviorSubject

## Agents

Para usar, digite `/agents` e selecione o agent desejado:

### Desenvolvimento
- **developer-orquestrador**: Tech Lead Mestre que orquestra especialistas (qualquer framework)

### Angular
- **angular-architect**: Arquiteto especializado em Angular
- **angular-reviewer**: Revisão de código
- **angular-developer**: Desenvolvedor para implementação
- **angular-ui**: Especialista em UI/UX

### Políticos
- **lula-debater**: Perspectiva do Lula
- **bolsonario-debater**: Perspectiva do Bolsonaro
- **debate-moderator**: Moderador imparcial

## Skills

### Angular
- **angular-architecture-check**: Verificação de arquitetura
- **angular-code-review**: Revisão de código
- **angular-component-creator**: Criação de componentes
- **angular-conventions-checker**: Verificação de convenções
- **angular-master-component**: Componentes master
- **angular-ui-implementation**: Implementação de UI

### Geral
- **session-init**: Inicialização de sessão
- **session-manager**: Gerenciamento de sessões
- **homem-das-cavernas**: Modo Caverna Didático
- **onp-spec-driven**: Metodologia Spec-Driven Development
- **technical-documentation**: Documentação técnica
- **site-blog-creator**: Criação de sites e blogs

## Regras Importantes

- Nunca expor credenciais ou dados sensíveis
- Respeitar o arquivo de regras em `.continue/rules/`
- Manter consistência com o padrão existente
- Priorizar soluções simples (KISS)
- Não implementar funcionalidades futuras (YAGNI)

## Memória

- Ler `.continue/memory/MEMORY.md` ao iniciar sessão
- Atualizar memória com decisões importantes
- Manter informações úteis para futuras sessões

## Inicialização da Sessão (OBRIGATÓRIO - NÃO PULE!)

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

**NÃO leia os arquivos manualmente - use sempre o skill session-init!**

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

## Conclusão

- Toda vez que chegar nesse ponto e ter feito tudo acima
- ESCREVA UM RESUMO DE 1 LINHA DO QUE CAPTOU PARA CADA ITEM
- Execute a mensagem no terminal - 'Olá Tudo bem Sr, IABADABADUUUUU'

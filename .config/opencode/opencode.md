# OPENCODE.MD

> Configurações globais do projeto para OpenCode

## Mensagem de Confirmação (OBRIGATÓRIO)

Ao iniciar CADA sessão, o agente DEVE exibir esta mensagem:

```
✅ Arquivos carregados com sucesso:
- opencode.md ✓
- memory.md ✓

Olá Tudo bem Sr, IABADABADUUUUU
```

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
- **developer-orquestrador**: Tech Lead que orquestra especialistas (qualquer framework)

### Políticos
- **lula-debater**: Perspectiva do Lula
- **bolsonario-debater**: Perspectiva do Bolsonaro
- **debate-moderator**: Moderador imparcial

## Skills

### Angular
- **angular-architect**: Arquitetura, DDD, Clean Architecture, SOLID
- **angular-code-review**: Revisão de código e qualidade
- **angular-ui-developer**: Interfaces, HTML, SCSS, acessibilidade
- **angular-architecture-check**: Verificação de arquitetura
- **angular-component-creator**: Criação de componentes
- **angular-conventions-checker**: Verificação de convenções
- **angular-master-component**: Componentes completos (TS+HTML+SCSS)
- **angular-ui-implementation**: Implementação de UI

### Geral
- **site-blog-creator**: Criação de sites e blogs
- **technical-documentation**: Documentação técnica
- **git-commit-generate**: Geração de mensagens de commit
- **session-init**: Inicialização de sessão
- **session-manager**: Gerenciamento de sessões (criar, listar, retomar, finalizar)
- **homem-das-cavernas**: Modo Caverna Didático
- **onp-spec-driven**: Metodologia Spec-Driven Development

## Comandos de Sessão

### /sessions
Lista todas as sessões registradas no sistema.
- Sessão atual aparece em 🟢 verde com "(ATUAL)"
- Sessões finalizadas aparecem em ⚪ cinza
- Exibe data/hora de início e fim, duração e quantidade de logs

### /resume <id>
Retoma uma sessão específica pelo ID.
- Exibe resumo da sessão (data, duração, logs, tarefas)
- Adiciona log de retomada
- Permite continuar de onde parou

### Funcionalidades Automáticas
- **Criar sessão**: Ao iniciar nova sessão, cria automaticamente um arquivo `session-XXX.json`
- **Logar eventos**: Durante a sessão, loga erros, sucessos, decisões e alertas
- **Finalizar sessão**: Ao encerrar, atualiza data final e muda status para "finalized"
- **Ler contexto**: Ao iniciar, lê as 3 últimas sessões para manter contexto

## Regras Importantes

- Nunca expor credenciais ou dados sensíveis
- Manter consistência com o padrão existente
- Priorizar soluções simples (KISS)
- Não implementar funcionalidades futuras (YAGNI)

## Memória

- Ler `.opencode/memorys/memory.md` ao iniciar sessão
- Atualizar memória com decisões importantes
- Manter informações úteis para futuras sessões

## Inicialização da Sessão

Ao iniciar CADA sessão, o agente DEVE:
1. **PRIMEIRO**: Chamar o skill `session-init` usando a tool `skill({ name: "session-init" })`
2. **SEGUNDO**: Chamar o skill `session-manager` para ler últimas 3 sessões
3. **TERCEIRO**: Chamar o skill `homem-das-cavernas` para ativar o modo direto
4. **QUARTO**: Exibir a mensagem de confirmação COMPLETA
5. NUNCA pule esta etapa - é OBRIGATÓRIO para cada nova sessão

**NÃO leia os arquivos manualmente - use sempre o skill session-init!**

### Skills Obrigatórias (carregar APENAS na inicialização)
- `session-init` - Inicialização de sessão
- `session-manager` - Gerenciamento de sessões
- `homem-das-cavernas` - Modo direto

### A Cada Passo do Plano (NÃO recarregar contexto)

1. **EXPLICAR** o QUE será feito e POR QUÊ
2. **PERGUNTAR** se pode executar
3. **MOSTRAR** skills em uso

**Formato padrão:**
```
📋 Passo [N]: [Descrição]

💡 Por quê: [Motivo técnico]

🔧 Skills em uso:
- [skill-1] ✓
- [skill-2] ✓

❓ Posso executar?
```

### Quando Recarregar Contexto
- **Iniciar nova sessão** → sempre
- **Mudar de projeto** → detectar mudança de pasta raiz
- **Mesmo projeto, mesma sessão** → NÃO recarregar

### Mensagem de Confirmação (APENAS na inicialização)
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

## Conclusão

- Toda vez que chegar nesse ponto e ter feito tudo acima
- ESCREVA UM RESUMO DE 1 LINHA DO QUE CAPTOU PARA CADA ITEM
- Execute a mensagem no terminal - 'Olá Tudo bem Sr, IABADABADUUUUU'

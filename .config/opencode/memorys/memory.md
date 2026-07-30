# Memória do Projeto

> Última atualização: 2026-07-29

## Arquitetura

- **Framework:** Angular + Ionic
- **Padrão:** DDD + Clean Architecture + SOLID
- **Organização:** Feature First
- **Estado:** Signals > Observable
- **Formulários:** @Rodrigos-dev/ars-dynamic-form
- **DI:** InjectionToken para services (nunca injetar classe diretamente)

## Configurações

- **Mock Global:** `USE_MOCK_GLOBAL` em `global-config.service.ts`
- **Mock Individual:** `USE_[DOMAIN]_CONFIG_MOCK` em cada service
- **Lógica:** Global prevalece sobre individual
- **Factory:** `provideMockService()` para criar providers

## Decisões Tomadas

- **2026-07-06** - User service refatorado com DI pattern
- **2026-07-06** - Sistema de mock global implementado
- **2026-08-08** - Layout base para páginas internas criado
- **2026-07-10** - Sistema de menu completo (3 tipos: LATERAL, HORIZONTAL, INSIDE_HEADER)
- **2026-07-13** - Interfaces e enums reorganizados por domínio (prefixo I, sufixo Enum)
- **2026-07-13** - Crypto interceptors desacoplados via DI
- **2026-07-13** - Cache Interceptor criado (TTL 5min, max 100 entradas)
- **2026-07-20** - Dados dinâmicos no header (UserLoggedStore + NotificationService)
- **2026-07-28** - Agents Angular migrados para Skills
- **2026-07-29** - Developer Orchestrator generalizado (qualquer framework)
- **2026-07-29** - Sistema de sessões implementado
- **2026-07-30** - Regra de exibição de skills em toda resposta adicionada
- **2026-07-30** - Skill end-task-validation criada (validação obrigatória antes de entregar)

## Padrões de Código

### Services
```
services/[domain]/
├── [domain].api.service.ts    # Interface + InjectionToken
├── [domain].service.ts        # Implementação real
├── [domain].mock.service.ts   # Implementação mock
└── [domain]-config.service.ts # Flag de configuração
```

### Components
```
features/[feature]/pages/[page]/
├── [page].page.ts
├── [page].page.html
├── [page].page.scss
└── forms-configs/             # Se tiver formulário
```

### Layouts
```
shared/layouts/[layout-name]/
├── [layout-name].component.ts
├── [layout-name].component.html
├── [layout-name].component.scss
├── index.ts
└── components/
    └── [sub-component]/
```

## Comandos Úteis

```bash
ng serve          # Servidor de desenvolvimento
ng build          # Build de produção
ng test           # Testes
ng lint           # Verificação de lint
```

## Regras de Sessão

- **Sempre ler automaticamente** no início de cada sessão:
  1. `C:\Users\Acer\.config\opencode\opencode.md`
  2. `C:\Users\Acer\.config\opencode\rules\rules_inviolable.md`
  3. `C:\Users\Acer\.config\opencode\memorys\memory.md`
- Exibir mensagem de conclusão: `Olá Tudo bem Sr, IABADABADUUUUU`

## Histórico

- 2026-06-27 - Criação do arquivo de memória
- 2026-07-06 - Refatoração completa do user service com DI
- 2026-07-06 - Implementação de select de estados brasileiros
- 2026-07-06 - Criação do sistema de mock global
- 2026-07-10 - Sistema de menu completo: lateral, horizontal, inside-header
- 2026-07-13 - Interfaces e enums reorganizados por domínio
- 2026-07-13 - Crypto interceptors desacoplados via DI
- 2026-07-13 - Cache Interceptor criado
- 2026-07-28 - Agents Angular migrados para Skills
- 2026-07-29 - Developer Orchestrator generalizado
- 2026-07-29 - Sistema de sessões implementado

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
  - Criado `IUserService` + `USER_SERVICE` token
  - Implementado `UserMockService` com banco em memória
  - Adicionado `getAll()` e `deleteById()` no mock

- **2026-07-06** - Campo de estado改为SELECT
  - Criado `brazilian-states.constants.ts` com 27 estados
  - Trocado `INPUT` por `SELECT` no formulário de endereço
  - Removido `as const` para compatibilidade com `ISelectOptions[]`

- **2026-07-06** - Sistema de mock global implementado
  - Criado `global-config.service.ts` com `USE_MOCK_GLOBAL`
  - Criado `shouldUseMock()` helper
  - Criado `provideMockService()` factory genérico
  - Refatorado `shared.provider.ts` para usar factory

- **2026-08-08** - Layout base para páginas internas criado
  - Criado `BasePagesLayoutComponent` com header, menu, notificações, avatar
  - Componentes: header, menu-lateral, menu-horizontal, notification-modal, user-settings
  - Menu mobile com accordion (3 níveis)
  - Badge de notificações posicionado via flexbox

- **2026-08-08** - Auth mock service ajustado
  - Adicionada lista de mock users
  - Implementado `handleAuthenticationSuccess()` para session handling
  - Adicionado `sendCodeEmailForgotPassword()` usando mock

- **2026-08-08** - Home page configurada
  - Menu com 3 níveis: Cadastro, Rotas, Produtos
  - Removidos "Meu Perfil" e "Configurações" (agora ficam no avatar)

- **2026-08-08** - Ajustes finais de UI
  - Header: ícones, título e badge aumentados
  - Badge subiu 1px para melhor posicionamento
  - Menu dividers apenas entre pais (filhos/netos sem divider)

- **2026-07-10** - Sistema de menu completo (3 tipos)
  - Criado `EMenuType` enum: LATERAL, HORIZONTAL, INSIDE_HEADER
  - Menu inside-header: itens à esquerda, sem título, dropdown 3 níveis
  - Settings service refatorado: `sideMenu: boolean` → `menuType: EMenuType`
  - Página de configurações: toggle → radio group com 3 opções
  - Atualização em tempo real do menu (sem reload)
  - Budget SCSS aumentado para 5kb (componentes de menu complexos)

- **2026-07-10** - Menu inside-header implementado
  - Componente `BasePagesMenuInsideHeaderComponent`
  - Dropdown com position: absolute (sem overflow no :host)
  - Cor hover: `#a8e6cf` (verde clarinho)
  - Backdrop escurecido ao abrir dropdown
  - Itens no canto esquerdo (oposto do avatar)

- **2026-07-10** - Logo no header desktop
  - Criado `assets.constants.ts` com caminho do logo
  - Logo 72px no canto esquerdo (visível apenas desktop ≥960px)
  - Filtro `brightness(0) invert(1)` para tornar logo branco
  - Click no logo navega para `/home`

- **2026-07-10** - Menu inside-header com scroll
  - Adicionado scroll horizontal com `overflow-x: auto`
  - Indicadores de overflow (linhas finas brancas)
  - Dropdown com posição dinâmica via `getBoundingClientRect()`
  - Fontes aumentadas: pai 18px, filho/neto 16px

- **2026-07-10** - Botão X no menu mobile/tablet
  - Setta branca (`arrow-back-outline`) no canto superior direito
  - Tamanho 32px, ícone 22px
  - Visível apenas em mobile/tablet (≤959px)

- **2026-07-10** - Badge de notificações aumentado no desktop
  - Mobile: 18px, Desktop: 24px
  - Fonte: 10px mobile, 13px desktop

- **2026-07-10** - Botão voltar sempre visível
  - Seta `arrow-back-outline` em todos os dispositivos
  - Layout reestruturado: seta → logo → menu items
  - Hamburger escondido no desktop (seta permanece)

- **2026-07-10** - Header dinâmico com booleanos
  - Inputs: showBackButton, showMenuToggle, showTitle, showNotifications, showAvatar, showLogo, showSidebar
  - Input: contentMaxWidth para controlar largura do conteúdo
  - Settings: só seta e título, max-width 800px, sem sidebar
  - Home: tudo visível, exceto seta

- **2026-07-10** - Conteúdo centralizado
  - `margin: 0 auto` no container de conteúdo
  - Título centralizado quando sidebar está oculto
  - Classe `base-header--no-sidebar` para centralização

- **2026-07-20** - Dados dinâmicos no header (UserLoggedStore + NotificationService)
  - Layout busca dados do usuário internamente via UserLoggedStore
  - Layout busca notificações internamente via NotificationService (DI pattern)
  - Removidos inputs hardcoded: userName, userEmail, userAvatarUrl, userId, notificationCount, notifications
  - Criado NotificationService com mock (4 notificações seed)
  - Home page limpa de dados hardcoded

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

## Referências

- **Documentação do projeto:** `.opencode/.memorys/`
  - `PROJECT_CONTEXT.md` - Visão geral
  - `ARCHITECTURE.md` - Padrões arquiteturais
  - `MOCK_SYSTEM.md` - Sistema de mock
  - `SERVICES.md` - Serviços
  - `FORMS.md` - Formulários

## Regras de Sessão

- **Sempre ler automaticamente** no início de cada sessão:
  1. `C:\Users\Acer\.config\opencode\opencode.md`
  2. `C:\Users\Acer\.config\opencode\rules\rules_security.md`
  3. `C:\Users\Acer\.config\opencode\memorys\memory.md`
- Exibir mensagem de conclusão: `Olá Tudo bem Sr, IABADABADUUUUU`

## Histórico

- 2026-06-27 - Criação do arquivo de memória
- 2026-07-06 - Refatoração completa do user service com DI
- 2026-07-06 - Implementação de select de estados brasileiros
- 2026-07-06 - Criação do sistema de mock global
- 2026-07-06 - Documentação completa do projeto em `.opencode/.memorys/`
- 2026-08-08 - Criação do base-pages-layout com header, menu, notificações, avatar
- 2026-08-08 - Implementação de accordion no menu mobile
- 2026-08-08 - Ajuste do auth mock service com session handling
- 2026-08-08 - Configuração da home page com menu de teste
- 2026-08-08 - Ajustes finais de UI (ícones, título, badge, dividers)
- 2026-07-10 - Sistema de menu completo: lateral, horizontal, inside-header
- 2026-07-10 - Criação do EMenuType enum e refatoração do settings service
- 2026-07-10 - Implementação do menu inside-header com dropdown 3 níveis
- 2026-07-10 - Página de configurações com radio group para 3 tipos de menu
- 2026-07-10 - Logo no header desktop com filtro branco
- 2026-07-10 - Menu inside-header com scroll e indicadores de overflow
- 2026-07-10 - Botão X no menu mobile/tablet
- 2026-07-10 - Badge de notificações aumentado no desktop
- 2026-07-10 - Botão voltar sempre visível em todos os dispositivos
- 2026-07-10 - Header dinâmico com booleanos (showLogo, showSidebar, contentMaxWidth)
- 2026-07-10 - Conteúdo centralizado com margin auto
- 2026-07-10 - Settings page: layout base com sidebar oculto

- **2026-07-13** - Interfaces e enums reorganizados por domínio
  - Interfaces renomeadas com prefixo `I` (ex: `IUserLogged`)
  - Enums renomeados com sufixo `Enum` (ex: `MenuTypeEnum`)
  - Estrutura: `shared/[category]/[domain]/` com `index.ts`
  - Comentários `@property` removidos (~113 comentários)

- **2026-07-13** - Crypto interceptors desacoplados
  - `responseDecryptInterceptor` e `requestCryptoInterceptor` usam `CryptoService` via DI
  - Eliminado acoplamento direto com `crypto-js`
  - `errorInterceptor` mantido acoplado (SessionService + ModalErrorService)

- **2026-07-13** - SettingsStore criado
  - `shared/stores/settings/settings.store.ts` com load/update/clear
  - `BasePagesLayout` usa SettingsStore em vez de signal local
  - Subscription leak corrigido com `takeUntilDestroyed`

- **2026-07-13** - Cache Interceptor criado
  - `core/interceptors/cache.interceptor.ts` com TTL de 5 minutos
  - Cache de GET requests com max 100 entradas (LRU eviction)
  - Exclusões automáticas: `/auth/`, `/refresh`
  - Header `X-Cache-Disable: true` para pular cache
  - Funções utilitárias: `clearCache()`, `clearCacheByUrl()`, `getCacheStats()`
  - Core complete: 8 interceptors ativos

- **2026-07-13** - Inicialização de sessão configurada
  - Adicionada seção "Inicialização da Sessão" no `opencode.md`
  - Mensagem de confirmação: `✅ Arquivos carregados com sucesso: ...`
  - Atualizado `memory.md` com regras de sessão

- **2026-07-17** - Skill session-init criado
  - Criado `C:\Users\Acer\.config\opencode\skills\session-init\SKILL.md`
  - Atualizado `opencode.md` para usar skill em vez de leitura manual
  - Agora o agente DEVE chamar `skill({ name: "session-init" })` no início

- **2026-07-17** - Auto-inicialização de sessão configurada
  - Adicionado plugin `opencode-plugin-preload-skills` no `opencode.json`
  - Criado `preload-skills.json` com configuração para carregar `session-init` automaticamente
  - Skill será chamado automaticamente no início de cada sessão

- **2026-07-17** - AGENTS.md criado para auto-inicialização
  - Criado `C:\Users\Acer\.config\opencode\AGENTS.md` com instruções de leitura automática
  - Arquivo será lido automaticamente pelo opencode no início de cada sessão

- **2026-07-28** - Skill "homem-das-cavernas" verificada
  - Skill está no diretório correto: `C:\Users\Acer\.config\opencode\skills\homem-das-cavernas\SKILL.md`
  - Skill pode ser carregada via `skill({ name: "homem-das-cavernas" })`
  - Não está na lista estática do system prompt, mas funciona via skill tool
  - Ativada quando usuário pede "modo caverna", "seja direto", etc.

- **2026-07-28** - Agents Angular migrados para Skills
  - Agents migrados: angular-architect, angular-code-reviewer, angular-ui-developer
  - Skills criadas: angular-architect, angular-ui-developer
  - Skill angular-code-review já existia e foi atualizada
  - Agent angular-developer-orquestrador mantido (orqestrador)
  - Orquestrador agora chama skills via `skill({ name: "..." })`
  - Agents removidos: angular-architect.md, angular-code-reviewer.md, angular-ui-developer.md
  - opencode.md atualizado com nova estrutura de agents e skills

- **2026-07-28** - Agent developer-orquestrador generalizado
  - Renomeado `angular-developer-orquestrador.md` → `developer-orquestrador.md`
  - Agent agora é genérico (não restrito a Angular)
  - Detecção automática do framework do projeto
  - Skills chamadas dinamicamente: `[framework]-architect`, `[framework]-ui-developer`, etc.
  - Ativação obrigatória: session-init → homem-das-cavernas → onp-spec-driven
  - Bootstrapping: detecta tecnologias, mapeia skills, lê últimos 5 commits
  - Regra dos 2 `if` máxima por função
  - Indicadores visuais: badges verdes com skills ativas
  - Memória atualizada com decisão

- **2026-07-29** - Sistema de sessões implementado
  - Criada pasta `C:\Users\Acer\.config\opencode\sessions\`
  - Criado skill `session-manager` com funcionalidades:
    - Criar nova sessão (auto)
    - Listar sessões (`/sessions`)
    - Retomar sessão (`/resume <id>`)
    - Finalizar sessão (auto)
    - Logar erros, sucessos, decisões, alertas
  - Atualizado `session-init` para criar sessão e ler últimas 3
  - Atualizado `developer-orquestrador` para ler 3 últimas sessões no bootstrapping
  - Atualizado `opencode.md` com documentação dos comandos
  - Formato de sessão: `session-XXX.json` com ID, data, status, logs, context

- **2026-07-29** - Developer Orchestrator Nível Mestre implementado
  - Reescrito `developer-orquestrador.md` com lógica 100% genérica
  - Detecção automática de framework: Angular, React, Vue, Python, NestJS, Go, Rust, Java, PHP, Ruby, .NET
  - Skills chamadas dinamicamente: `[framework]-architect`, `[framework]-ui-developer`, etc.
  - Pipeline de execução: Análise → Planejamento → Execução → Validação → Entrega
  - Sistema de fallback: skill não existe → genérica → execução direta
  - Classificação automática de tarefas por palavras-chave
  - Validação contínua antes/durante/depois de cada alteração
  - Relatório de progresso visual com indicadores
  - Regra: projetos futuros usam skills `[framework]-*` conforme necessário

- **2026-07-29** - Plugin auto-session-init removido
  - Removido `"./plugins/auto-session-init.ts"` do `opencode.json`
  - Deletado arquivo `plugins/auto-session-init.ts`
  - Motivo: usuário não gostou da inicialização automática
  - Session-init agora é chamado manualmente quando solicitado

- **2026-07-29** - Inicialização de sessão reforçada
  - Atualizado `AGENTS.md` com ordem obrigatória: developer-orquestrador → session-init → session-manager → homem-das-cavernas
  - Atualizado `opencode.md` com lista de skills obrigatórias
  - Atualizado `developer-orquestrador.md` com mensagem de confirmação padronizada
  - Atualizado `session-init` para ler `rules_inviolable.md` primeiro
  - Mensagem de confirmação agora inclui lista de skills em uso
  - Regra: SEMPRE exibir lista de skills ativas no início de cada sessão

- **2026-07-29** - Inicialização de sessão reforçada (versão 2)
  - Contexto completo: APENAS na inicialização ou mudança de projeto
  - A cada passo: APENAS mostrar skills em uso (sem recarregar contexto)
  - Evita recarregamento desnecessário de arquivos e sessões
  - Mantém performance e evita repetição

- **2026-07-29** - Inicialização de sessão reforçada (versão 3)
  - `developer-orquestrador` é um agent, não uma skill
  - Agent já está ativo via system prompt (não precisa chamar)
  - Skills obrigatórias: session-init, session-manager, homem-das-cavernas
  - Mensagem de confirmação atualizada (sem developer-orquestrador na lista)

- **2026-07-29** - Controle de fluxo a cada passo
  - A cada passo do plano: explicar o QUE e POR QUÊ
  - Sempre perguntar antes de executar: "Posso executar?"
  - 3 opções: "Posso executar", "Executar tudo", "Não executar"
  - Formato padrão: Passo → Por quê → Skills em uso → Pergunta

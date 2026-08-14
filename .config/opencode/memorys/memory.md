# Memória do Projeto

> Última atualização: 2026-08-13

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
- **2026-07-30** - Skill unit-test-jest criada para testes unitários Angular + Jest
- **2026-07-30** - Skill unit-test-vitest criada para testes unitários Angular + Vitest
- **2026-07-30** - Skill test-framework-detector criada para detectar framework automaticamente
- **2026-07-30** - Orchestrador atualizado para detectar framework de teste automaticamente
- **2026-07-30** - Skills de teste corrigidas conforme code review (exemplos Pipe/Guard, alternativas @analogjs, comandos Windows)
- **2026-07-30** - Skills de teste replicadas para todos os diretórios (gemini, continue, claude, openclaude, backup)
- **2026-07-30** - Regra de exibição de skills reforçada: skills NO TOPO de cada resposta
- **2026-07-30** - Validação final end-task-validation obrigatória antes de entregar qualquer tarefa
- **2026-07-31** - Cobertura shared module: Statements 94.5%, Branches 90.04%, Functions 90.63%, Lines 95.32% (365 testes, 34 arquivos)
- **2026-07-31** - Cobertura auth module: ~95-100% (175 testes)
- **2026-07-31** - Cobertura core module: Statements 96.22%, Branches 86.56%, Functions 98%, Lines 96.44% (68 testes)
- **2026-08-01** - global-config.service.ts: globalFlag parameter adicionado (DI-based mock control)
- **2026-08-01** - global-config.service.ts: 100% branch coverage (antes 50%)
- **2026-08-01** - menu-horizontal-desktop.component.ts: 100% branch coverage (antes 96.15%)
- **2026-08-01** - Commit 6ef674c: 63 arquivos, 5974 linhas adicionadas (testes shared + core)
- **2026-08-13** - Regra de controle de commits adicionada (seção 16 rules_inviolable.md)
- **2026-08-09** - LoggerService refatorado: isDevMode via InjectionToken (LOGGER_DEV_MODE) para testes confiáveis em CI
- **2026-08-09** - CI/CD pipeline configurado: lint → test → build com composite action
- **2026-08-09** - PR Validation: regras de branch (feature→develop→master, sem push direto)
- **2026-08-09** - workflow_dispatch adicionado para execução manual do CI
- **2026-08-09** - Documento CI_CD_RULES.md criado (.github/) com regras completas de CI/CD e testes

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

### Desenvolvimento
```bash
npm run start        # ng serve (porta 4200)
npm run build        # ng build → output em www/
npm run lint         # ng lint
npm run lint --fix   # corrige erros automaticamente
```

### Testes Unitários (SEMPRE arquivo por arquivo)
```bash
# Framework: Vitest 4.1.10 + @analogjs/vitest-angular
# Executor: node direto (NÃO usar npx vitest)

# Comando padrão para testar arquivo específico:
node "<path-do-projeto>/node_modules/vitest/vitest.mjs" run "<caminho-do-arquivo.spec.ts>"

# Exemplo real:
node "D:/2 - workspace/4 - basic inicial core angular ionic/basic-initial-core-full/node_modules/vitest/vitest.mjs" run "D:/2 - workspace/4 - basic inicial core angular ionic/basic-initial-core-full/src/app/features/auth/pages/login/login.page.spec.ts"

# Filtrar describe específico:
node "<path-do-projeto>/node_modules/vitest/vitest.mjs" run "<arquivo.spec.ts>" -t "^NomeDoDescribe(\s.*)?$"

# Cobertura (silenciosa):
npx vitest run <pasta> --coverage --silent

# Exemplo cobertura auth:
npx vitest run src/app/features/auth --coverage --silent
```

### Cobertura com Tabela (formato Jest)
```bash
# Shared module (com tabela text):
npx vitest run src/app/shared --coverage --silent --reporter=default --no-file-parallelism --coverage.reporter=text --coverage.include="src/app/shared/**/*.ts" --coverage.exclude="**/*.routes.ts" --coverage.exclude="**/*.module.ts" --coverage.exclude="**/*.config.ts" --coverage.exclude="**/environment*.ts" --coverage.exclude="**/test-setup.ts" --coverage.exclude="**/*.spec.ts" --coverage.exclude="**/*.test.ts"

# Auth module:
npx vitest run src/app/features/auth --coverage --silent --reporter=default --no-file-parallelism --coverage.reporter=text --coverage.include="src/app/features/auth/**/*.ts"

# Projeto inteiro:
npx vitest run --coverage --silent --reporter=default --no-file-parallelism --coverage.reporter=text
```

### Resultados de Cobertura (Atualizados 2026-07-31)

| Módulo | Statements | Branches | Functions | Lines | Testes |
|--------|-----------|----------|-----------|-------|--------|
| **shared** | 94.5% | 90.04% | 90.63% | 95.32% | 365 |
| **auth** | ~100% | ~95% | ~100% | ~100% | 175 |
| **core** | 96.22% | 86.56% | 98% | 96.44% | 68 |

### Arquivos com 100% Branch Coverage (Ajustados 2026-08-01)

| Arquivo | Branches | Antes | Mudança |
|---------|----------|-------|---------|
| `global-config.service.ts` | 100% | 50% | +50% (globalFlag param) |
| `menu-horizontal-desktop.component.ts` | 100% | 96.15% | +3.85% (line 61 false branch) |

### Configuração que FUNCIONA (não alterar sem testar!)

#### vite.config.mts
```typescript
/// <reference types="vitest" />
import { defineConfig, Plugin } from 'vite';
import angular from '@analogjs/vite-plugin-angular';
import { resolve } from 'path';

function ionicDirectoryPlugin(): Plugin {
  return {
    name: 'ionic-directory-resolver',
    enforce: 'pre',
    resolveId(source, importer) {
      if (!importer) return null;
      if (source === '@ionic/core/components') {
        return resolve(process.cwd(), 'node_modules', '@ionic', 'core', 'components', 'index.js');
      }
      return null;
    },
  };
}

export default defineConfig(({ mode }) => ({
  plugins: [angular(), ionicDirectoryPlugin()],
  test: {
    globals: true,
    setupFiles: ['src/test-setup.ts'],
    environment: 'jsdom',
    include: ['src/**/*.{test,spec}.{js,mjs,cjs,ts,mts,cts,jsx,tsx}'],
    reporters: ['dot'],
    server: { deps: { inline: [/@ionic/, /ionicons/], fallbackCJS: true } },
    deps: { inline: [/@ionic/, /ionicons/] },
    ssr: { noExternal: true },
    coverage: {
      provider: 'v8',
      reporter: ['html', 'text-summary'],
      reportsDirectory: 'coverage/app',
      thresholds: { branches: 80, functions: 80, lines: 80, statements: 80 },
    },
    onConsoleLog(log: string, type: 'stdout' | 'stderr'): boolean | void {
      if (log.includes('Could not parse CSS stylesheet')) return false;
      if (log.includes('Ionicons Warning')) return false;
    },
  },
  ssr: { noExternal: true },
  optimizeDeps: { include: ['@ionic/core', '@ionic/angular', 'ionicons'] },
  resolve: { alias: { src: '/src' }, conditions: ['import', 'module', 'default'] },
}));
```

#### src/test-setup.ts
```typescript
import '@angular/compiler';
import '@analogjs/vitest-angular/setup-zone';
import { setupTestBed } from '@analogjs/vitest-angular/setup-testbed';

// Suprimir warnings de CSS do Ionic/jsdom (escritos direto no process.stderr)
const originalStderrWrite = process.stderr.write.bind(process.stderr);
process.stderr.write = function (chunk: any, ...args: any[]): boolean {
  const str = typeof chunk === 'string' ? chunk : chunk.toString();
  if (str.includes('Could not parse CSS stylesheet')) return true;
  if (str.includes('Ionicons Warning')) return true;
  return originalStderrWrite(chunk, ...args as any);
} as typeof process.stderr.write;

setupTestBed();
```

### Regra de Ouro para Testes
1. **SEMPRE** testar arquivo por arquivo
2. **NUNCA** usar `npx vitest` (falha por resolução de módulos)
3. Usar `node` direto apontando para `vitest.mjs`
4. Após todos passarem individualmente, pode rodar suite completa
5. **Output limpo**: reporter `dot` + supressão de warnings CSS/Ionicons

### Gotchas Conhecidos
- **`input()` e `output()` do Angular** precisam de injection context → usar `TestBed` + `fixture.componentRef.setInput()` (não `new Component()`)
- **`ResizeObserver`** não existe no jsdom → mockar com `globalThis.ResizeObserver = class { ... }`
- **`MenuTypeEnum.LATERAL`** tem valor `'lateral'` (lowercase), não `'LATERAL'`
- **`BasePagesLayoutComponent`** precisa de providers para child components: `AUTH_SERVICE`, `NOTIFICATION_SERVICE`, `AlertController`, etc.
- **`global-config.service.ts`**: `shouldUseMock()` e `provideMockService()` aceitam `globalFlag` param (default `USE_MOCK_GLOBAL`)
- **`menu-horizontal-desktop.component.ts`**: line 61 é `if (this.scrollContainer?.nativeElement)` — precisa testar branch false (null nativeElement)
- **`vi.mock('@angular/core')`** pode falhar no CI por resolução de módulos → usar InjectionToken + DI para `isDevMode` e afins

## CI/CD

### Pipeline
- **Workflow:** `ci.yml` (lint → test → build) + `pr-validation.yml` (validação de branch + coverage)
- **Triggers:** `pull_request` (develop/main/master) + `workflow_dispatch` (manual)
- **Composite Action:** `.github/actions/setup-node/action.yml` (setup Node + npm auth + install)
- **Runner:** GitHub-hosted (`ubuntu-latest`)

### Regras de Branch
- **Push:** APENAS em `feature/*`, `fix/*`, `hotfix/*`
- **PR:** `feature/*` → `develop` → `master`
- **NUNCA:** `master` → `develop` (bloqueado no pr-validation.yml)
- **NUNCA:** push direto em `develop` ou `master`

### Comandos CI
```bash
npm run test:ci  # vitest run --coverage --silent --reporter=default --no-file-parallelism --coverage.reporter=json-summary --coverage.reporter=text
```

### Cobertura
- **Threshold:** 80% (branches, functions, lines, statements)
- **Artifact:** `coverage-report` (retido 7 dias)

### Documentação
- `.github/CI_CD_RULES.md` — guia completo em português

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
- 2026-07-30 - Regra de exibição de skills em toda resposta
- 2026-07-30 - Skill end-task-validation criada
- 2026-07-30 - Skills de teste (jest/vitest) criadas e replicadas
- 2026-07-31 - Cobertura shared: 94.5% statements, 90.04% branches
- 2026-07-31 - Cobertura auth: ~95-100%
- 2026-07-31 - Cobertura core: 96.22% statements, 86.56% branches
- 2026-08-01 - global-config.service.ts: 100% branch coverage (globalFlag param)
- 2026-08-01 - menu-horizontal-desktop.component.ts: 100% branch coverage
- 2026-08-01 - Commit 6ef674c: 63 arquivos, 5974 linhas (testes shared + core)
- 2026-08-09 - LoggerService refatorado: isDevMode via InjectionToken (LOGGER_DEV_MODE) para testes confiáveis em CI
- 2026-08-09 - CI/CD pipeline configurado: lint → test → build com composite action
- 2026-08-09 - PR Validation: regras de branch (feature→develop→master, sem push direto)
- 2026-08-09 - workflow_dispatch adicionado para execução manual do CI
- 2026-08-09 - Documento CI_CD_RULES.md criado (.github/) com regras completas de CI/CD e testes

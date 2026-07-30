---
name: unit-test-vitest
description: Use quando o usuário pedir para criar, corrigir, completar ou revisar testes unitários com Vitest em um projeto Angular.
---

# Skill: Testes Unitários - Angular + Vitest

## Descrição
Cria, corrige, completa ou revisa testes unitários com Vitest em qualquer projeto Angular, cobrindo componentes, services, effects, reducers, selectors, facade, signal stores e utilitários.

## Quando usar
Use esta skill quando o usuário pedir para criar, corrigir, completar ou revisar testes unitários com Vitest em qualquer arquivo de um projeto Angular.

## Stack e configurações

- **Framework de testes:** Vitest (Vite-native, Jest-compatible)
- **Arquivos:** *.spec.ts ou *.test.ts (configurável)
- **Configuração:** "vitest.config.ts" ou "vite.config.ts" com bloco test
- **Setup:** "setup-vitest.ts" ou "setup.ts" (configurável)
- **Cobertura:** "@vitest/coverage-v8" ou "@vitest/coverage-istanbul"
- **Assertions:** Built-in Chai + jest-compatible API

## Comandos Úteis

```bash
# Rodar todos os testes
npx vitest

# Rodar com cobertura
npx vitest --coverage

# Rodar uma vez (sem watch)
npx vitest run

# Rodar teste específico
npx vitest run path/to/file.test.ts

# Rodar em modo UI
npx vitest --ui

# Rodar em modo browser
npx vitest --browser
```

## Detectar Framework de Teste

O orquestrador DEVE detectar automaticamente qual framework está configurado:

1. **Verificar package.json** do projeto:
   - Se tiver `"vitest"` nas devDependencies → Vitest
   - Se tiver `"jest"` ou `"@angular/cli"` com jest → Jest
   - Se tiver ambos → Perguntar ao usuário qual usar

2. **Verificar arquivos de configuração**:
   - `vitest.config.ts` ou `vitest.config.js` → Vitest
   - `jest.config.ts` ou `jest.config.js` → Jest
   - `angular.json` com `"test": { "builder": "@angular-builders/jest:run" }` → Jest
   - `angular.json` com `"test": { "builder": "@angular-builders/vitest:run" }` → Vitest

3. **Se não encontrar nenhum** → Perguntar ao usuário qual framework usar

## Regras Simples - Sempre Valer

1. **Use `vi` do Vitest** para mocks (não `jest`):
   - `vi.fn()` para criar mocks
   - `vi.mock()` para mockar módulos
   - `vi.spyOn()` para espiar métodos
   - `vi.restoreAllMocks()` para restaurar

2. **Configure `restoreMocks: true`** no vitest.config.ts para limpeza automática

3. **Use `vi.mock(import('./module'))`** em vez de strings para type safety

4. **Use `vi.hoisted()`** quando precisar de factories antes dos imports

5. **Para services Angular**, use `mockProvider()` do `@vitest/angular` ou crie mocks manualmente

6. **Para componentes**, use `TestBed.configureTestingModule()` com imports necessários

7. **Prefira `TestBed.inject()`** em vez de `TestBed.get()` (deprecated)

8. **Use `fixture.detectChanges()`** para trigger ngOnInit

9. **Para signals**, use `fixture.componentRef.setInput()` e `fixture.componentRef.getInput()`

10. **Agrupar testes com `describe`**, usar `it` ou `test` para cada caso

## Padrões de Mock

### Services Angular
```typescript
import { vi } from 'vitest'

const mockService = {
  metodo: vi.fn()
}

await TestBed.configureTestingModule({
  providers: [
    { provide: ServiceName, useValue: mockService }
  ]
}).compileComponents();
```

### HTTP Calls (MSW)
```typescript
import { http, HttpResponse } from 'msw'
import { setupServer } from 'msw/node'

const server = setupServer(
  http.get('/api/endpoint', () => {
    return HttpResponse.json({ data: 'mocked' })
  })
)

beforeAll(() => server.listen({ onUnhandledRequest: 'error' }))
afterAll(() => server.close())
afterEach(() => server.resetHandlers())
```

### Módulos
```typescript
vi.mock(import('./service'), () => ({
  ServiceName: vi.fn().mockImplementation(() => ({
    metodo: vi.fn()
  }))
}))
```

### Signals
```typescript
component.signalName.set(value)
expect(component.signalName()).toBe(value)
```

### Espiando Métodos
```typescript
const spy = vi.spyOn(object, 'method')
expect(spy).toHaveBeenCalledWith(args)
```

## Estrutura de Teste Padrão

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { describe, it, expect, beforeEach } from 'vitest';
import { ComponentName } from './component-name';

describe('ComponentName', () => {
  let component: ComponentName;
  let fixture: ComponentFixture<ComponentName>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [ComponentName],
      providers: []
    }).compileComponents();

    fixture = TestBed.createComponent(ComponentName);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

  it('should [comportamento esperado]', () => {
    // Arrange
    // Act
    // Assert
  });
});
```

## Configuração Recomendada (vitest.config.ts)

### Opção 1: Com @analogjs/vite-plugin-angular (se disponível)

```typescript
import { defineConfig } from 'vitest/config'
import angular from '@analogjs/vite-plugin-angular'

export default defineConfig({
  plugins: [angular()],
  test: {
    globals: true,
    environment: 'jsdom',
    include: ['src/**/*.spec.ts', 'src/**/*.test.ts'],
    setupFiles: ['src/setup-vitest.ts'],
    restoreMocks: true,
    coverage: {
      provider: 'v8',
      reporter: ['text', 'json', 'html'],
      include: ['src/**/*.ts'],
      exclude: ['src/**/*.spec.ts', 'src/**/*.test.ts', 'src/main.ts', 'src/polyfills.ts']
    }
  }
})
```

### Opção 2: Sem @analogjs (alternativa genérica)

```typescript
import { defineConfig } from 'vitest/config'

export default defineConfig({
  test: {
    globals: true,
    environment: 'jsdom',
    include: ['src/**/*.spec.ts', 'src/**/*.test.ts'],
    restoreMocks: true,
    coverage: {
      provider: 'v8',
      reporter: ['text', 'json', 'html'],
      include: ['src/**/*.ts'],
      exclude: ['src/**/*.spec.ts', 'src/**/*.test.ts', 'src/main.ts', 'src/polyfills.ts']
    }
  }
})
```

## Setup File (setup-vitest.ts)

### Opção 1: Com @analogjs (se disponível)

```typescript
import '@analogjs/vitest-zone-r8'
```

### Opção 2: Sem @analogjs (alternativa)

```typescript
// Configuração básica para Angular + Vitest
// Se precisar de Zone.js, importe manualmente
```

## Tipos de Teste

### Componentes
- Criação
- Renderização
- Interações (click, input)
- Outputs/Events
- Inputs/Props
- Lifecycle hooks

### Services
- Métodos públicos
- Tratamento de erros
- Chamadas HTTP
- States/Signals

### Pipes
- Transformação
- Casos extremos

### Guards
- Retorno true/false
- Redirecionamento

## Quando não usar

- Para testes de integração usar "cypress" ou "playwright"
- Para testes de performance usar ferramentas específicas
- Para testes visuais usar "storyshot" ou similar

## Saída Esperada

Arquivo .spec.ts ou .test.ts seguindo padrão do projeto, com:
- Imports corretos (vitest em vez de jest)
- Configuração adequada do TestBed
- Mocks usando vi.fn(), vi.mock(), vi.spyOn()
- Testes cobrindo cenários principais
- Organização clara (describe, it/test, expect)
---
name: unit-test-jest
description: Use quando o usuário pedir para criar, corrigir, completar ou revisar testes unitários com Jest em um projeto Angular.
---

# Skill: Testes Unitários - Angular + Jest

## Descrição
Cria, corrige, completa ou revisa testes unitários com Jest em qualquer projeto Angular que utilize "jest-preset-angular", cobrindo componentes, services, effects, reducers, selectors, facade, signal stores e utilitários.

## Quando usar
Use esta skill quando o usuário pedir para criar, corrigir, completar ou revisar testes unitários com Jest em qualquer arquivo de um projeto Angular - independente do nome do projeto.

## Instruções

## Stack e configurações

- **Framework de testes:** Jest ("jest-preset-angular")
- **Arquivos:** *.spec.ts (padrão Angular)
- **Configuração:** "jest.config.ts" ou "jest.config.js" na raiz do projeto
- **Setup:** "setup-jest.ts" na raiz
- **Cobertura:** "collectCoverage: false" por padrão (ativar potencialmente via CLI)
- **Comando para rodar todos os testes:** "ng test" ou "npm test" (configurar no package.json)
- **Comando para rodar com cobertura:** "ng test --code-coverage" ou "npm test -- --code-coverage"

## Regras Simples - Sempre Valer

1. **Apresente antes de executar e só exiba o nome da skill que está sendo usada.**
2. **Use o padrão de exports/imports do projeto** - mantenha consistência com o restante do código.
3. **Nunca use "jest.fn()"** para mocks - usar "jest.createMockFromFunction()" ou "jest.createMockFromModule()".
4. **Use "mockProvider()"** do "@angular/providers/testing" para services Angular.
5. **Para componentes, use "TestBed.configureTestingModule()"** com imports necessários.
6. **Prefira " TestBed.inject()"** em vez de "TestBed.get()" (deprecated).
7. **Use "fixture.detectChanges()"** para trigger ngOnInit.
8. **Para signals, use "fixture.componentRef.setInput()"** e "fixture.componentRef.getInput()".
9. **Mocke dependências externas** (HTTP, Router, etc.) com "HttpClientTestingModule" ou "RouterTestingModule".
10. **Agrupar testes com "describe"**, usar "it" para cada caso, e "expect" para asserções.

## Padrões de Mock

### Services Angular
```typescript
const mockService = {
  metodo: jest.fn()
};

await TestBed.configureTestingModule({
  providers: [
    { provide: ServiceName, useValue: mockService }
  ]
}).compileComponents();
```

### HTTP Calls
```typescript
const httpMock = TestBed.inject(HttpTestingController);
const req = httpMock.expectOne('/api/endpoint');
req.flush(data);
httpMock.verify();
```

### Signals
```typescript
component.signalName.set(value);
expect(component.signalName()).toBe(value);
```

## Estrutura de Teste Padrão

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
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

```typescript
describe('CurrencyNamePipe', () => {
  let pipe: CurrencyNamePipe;

  beforeEach(() => {
    pipe = new CurrencyNamePipe();
  });

  it('should transform value correctly', () => {
    expect(pipe.transform(1000)).toBe('R$ 1.000,00');
  });

  it('should handle null value', () => {
    expect(pipe.transform(null)).toBe('');
  });
});
```

### Guards
- Retorno true/false
- Redirecionamento

```typescript
describe('AuthGuard', () => {
  let guard: AuthGuard;
  let router: jasmine.SpyObj<Router>;

  beforeEach(() => {
    router = jasmine.createSpyObj('Router', ['navigate']);
    guard = new AuthGuard(router);
  });

  it('should allow access when authenticated', () => {
    spyOn(localStorage, 'getItem').and.returnValue('token');
    expect(guard.canActivate()).toBeTrue();
  });

  it('should redirect to login when not authenticated', () => {
    spyOn(localStorage, 'getItem').and.returnValue(null);
    guard.canActivate();
    expect(router.navigate).toHaveBeenCalledWith(['/login']);
  });
});
```

## Comandos Úteis

```bash
# Rodar todos os testes
ng test

# Rodar com cobertura
ng test --code-coverage

# Rodar teste específico
ng test --include='**/nome-do-arquivo.spec.ts'

# Rodar em modo watch
ng test --watch

# Rodar em modo CI (sem watch)
ng test --watch=false
```

## Quando não usar

- Para testes de integração usar "e2e" ou "cypress"
- Para testes de performance usar ferramentas específicas
- Para testes visuais usar "jest-image-snapshot" ou similar

## Saída Esperada

Arquivo .spec.ts seguindo padrão do projeto, com:
- Imports corretos
- Configuração adequada do TestBed
- Mocks bem definidos
- Testes cobrindo cenários principais
- Organização clara (describe, it, expect)
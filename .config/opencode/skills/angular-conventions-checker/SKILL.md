---
name: angular-conventions-checker
description: Use quando o usuário pedir para verificar convenções do projeto Angular, validar conformidade ou identificar padrões antes de iniciar tarefas.
---

# Angular Conventions Checker

## Descrição

Skill para verificar convenções do projeto Angular.

## Quando Usar

- Antes de iniciar qualquer tarefa
- Para validar conformidade
- Para identificar padrões

## Fluxo Obrigatório

1. **Procurar ANGULAR_CONVENTIONS.MD** na raiz
2. **Se existir**, seguir rigorosamente
3. **Se não existir**, usar convenções padrão abaixo
4. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

## Convenções Padrão

### Nomenclatura

#### Interfaces

- Iniciar com `I`
- Exemplos: `IUser`, `IProduct`, `ILogin`

#### Enums

- Iniciar com `E`
- Exemplos: `EStatus`, `ERole`, `EPermission`

#### Booleanos

- Iniciar com: `is`, `has`, `can`, `should`
- Exemplos: `isLoading`, `hasPermission`, `canEdit`

#### Observables

- Terminar com `$`
- Exemplo: `users$`

#### Signals

- Sem `$`
- Exemplo: `users`

#### Collections

- Sempre plural
- Exemplo: `products`, `users`

### Organização

#### Estrutura por Feature

```
features/
  authentication/
    components/
    pages/
    services/
    facades/
    interfaces/
    models/
    enums/
```

#### Estrutura Errada

```
components/
pages/
services/
```

### Arquitetura

#### Princípios

- DDD
- Clean Architecture
- SOLID
- Feature First
- Single Responsibility

#### Comunicação

- Page → Facade → Service → API
- Nunca Component → API

#### Estado

- Signals > Observable
- Computed para derivados
- Effect para side effects

## Saída

Relatório com:

- Convenções encontradas no projeto
- Conformidade com padrões
- Sugestões (se aplicável)

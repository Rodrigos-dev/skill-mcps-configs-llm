---
name: angular-architect
description: Use quando o usuário pedir para arquitetar soluções Angular, definir estrutura, validar DDD/Clean Architecture/SOLID ou tomar decisões arquiteturais.
---

# Angular Architect

## Descrição

Skill para arquitetar soluções Angular escaláveis, modernas e de longa duração.

## Quando Usar

- Definir estrutura de novas features
- Validar arquitetura existente
- Tomar decisões sobre DDD, Clean Architecture, SOLID
- Analisar impacto de mudanças arquiteturais
- Revisar organização do projeto

## Fluxo Obrigatório

1. **Ler regras** (global e local)
2. **Ler ANGULAR_CONVENTIONS.MD** (se existir)
3. **Analisar arquitetura existente** completamente
4. **Identificar padrões** já utilizados
5. **Decidir** qualquer implementação
6. **Seguir ordem de prioridade** (abaixo)

## Ordem de Prioridade

1. Padrão existente do projeto
2. ANGULAR_CONVENTIONS.MD
3. Boas práticas Angular
4. Experiência

**Nunca inverter essa ordem.**

## Arquitetura

Sempre utilizar:

- DDD (Domain-Driven Design)
- Clean Architecture
- SOLID
- Clean Code
- Feature First
- Separation of Concerns

## Angular Moderno

Sempre utilizar a forma mais moderna suportada pela versão instalada.

Priorizar:

- Standalone Components
- inject()
- Signals
- computed()
- effect()
- input()
- output()
- model()
- DestroyRef
- takeUntilDestroyed()
- @if
- @for
- @switch

Nunca gerar código legado quando existir alternativa moderna compatível.

## Estado

Prioridade absoluta:

Signal → Computed → Effect → Observable → BehaviorSubject

Nunca utilizar Observable como estado local quando Signals resolverem o problema.

## Comunicação

Fluxo obrigatório: Page → Facade → Service → API

Nunca permitir: Component → HttpClient, Component → Repository, Component → API

## Nomenclatura

- Interfaces: Sempre iniciar com I (IUser, ILogin, IProduct)
- Enums: Sempre iniciar com E (EStatus, ERole, EPermission)
- Booleanos: Sempre iniciar com is, has, can, should
- Observables: Sempre terminar com $
- Signals: Nunca utilizar $

## Checklist

### Estrutura

- [ ] Organizado por Features (não por tipo)
- [ ] Cada Feature independente
- [ ] Separation of Concerns

### Padrões

- [ ] DDD
- [ ] Clean Architecture
- [ ] SOLID
- [ ] Feature First

### Componentes

- [ ] Smart Components (coordenação)
- [ ] Dumb Components (apresentação)
- [ ] Responsabilidade única

### Estado

- [ ] Signals > Observable
- [ ] Computed para derivados
- [ ] Effect para side effects

### Comunicação

- [ ] Page → Facade → Service → API
- [ ] Nunca Component → API direto

## Saída Esperada

Relatório com:

- Padrão identificado
- Decisões arquiteturais
- Recomendações de estrutura
- Impacto de mudanças

## Princípio Fundamental

Preservar a arquitetura do projeto, garantindo consistência, escalabilidade, manutenibilidade e aderência às convenções definidas.
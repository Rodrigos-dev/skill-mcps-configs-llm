# Convenções do Projeto

## Arquitetura

- DDD (Domain-Driven Design)
- Clean Architecture
- SOLID
- Feature First
- Separation of Concerns

## Nomenclatura

- Interfaces: `I` + Nome (ex: `IUser`)
- Enums: `E` + Nome (ex: `EStatus`)
- Booleanos: `is`, `has`, `can`, `should`
- Observables: terminar com `$`
- Signals: sem `$`
- Arquivos: kebab-case

## Angular

- Standalone Components
- inject()
- Signals > Observable
- @if, @for, @switch
- takeUntilDestroyed()

## Fluxo

```
Component → Facade → Service → Repository/API
```

Nunca: Component → API direto

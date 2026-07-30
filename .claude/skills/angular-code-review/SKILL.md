---
name: angular-code-review
description: Use quando o usuário pedir para revisar código Angular, analisar qualidade, identificar problemas ou verificar boas práticas.
---

# Angular Code Review

## Descrição

Skill para revisar código Angular.

## Quando Usar

- Após implementação
- Antes de merge
- Para identificar problemas

## Fluxo Obrigatório

1. **Ler ANGULAR_CONVENTIONS.MD** (se existir)
2. **Verificar padrão** do projeto
3. **Analisar código** ponto a ponto
4. **Classificar** por severidade
5. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

## Checklist

### Arquitetura

- [ ] Segue padrão existente
- [ ] Respeita DDD/SOLID
- [ ] Feature First
- [ ] Responsabilidade única

### Angular

- [ ] Standalone quando suportado
- [ ] inject() ao invés de constructor
- [ ] Signals para estado
- [ ] computed()/effect() quando necessário
- [ ] takeUntilDestroyed()

### Componentes

- [ ] Pequenos e focados
- [ ] Sem regra de negócio
- [ ] Sem chamadas HTTP
- [ ] Inputs/Outputs claros

### TypeScript

- [ ] Sem any
- [ ] Tipagem correta
- [ ] Readonly quando possível
- [ ] Null Safety

### Performance

- [ ] Sem funções no template
- [ ] Sem subscribe aninhado
- [ ] Track em @for
- [ ] Sem renderizações desnecessárias

### HTML

- [ ] Semântico
- [ ] Acessível (ARIA)
- [ ] Labels em campos
- [ ] alt em imagens

### SCSS

- [ ] Mobile First
- [ ] Sem !important
- [ ] Sem float
- [ ] Nesting máx 3 níveis

## Classificação

- **Crítico**: Bug, Memory Leak, violação grave
- **Alto**: Duplicação, acoplamento, performance
- **Médio**: Organização, nomenclatura
- **Baixo**: Melhorias opcionais

## Saída

Relatório com: Resumo, Pontos Positivos, Problemas, Melhorias, Conclusão.

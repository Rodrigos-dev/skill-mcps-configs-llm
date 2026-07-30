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

### Crítico
- Quebra arquitetura
- Bug
- Memory Leak
- Problema de segurança
- Problema de acessibilidade grave
- Violação importante do ANGULAR_CONVENTIONS.MD

### Alto
- Duplicação
- Acoplamento elevado
- Baixa coesão
- Performance ruim
- HTML incorreto
- Signals utilizados incorretamente

### Médio
- Organização
- Legibilidade
- Nomenclatura
- Estrutura
- Responsabilidades

### Baixo
- Melhorias
- Simplificações
- Refatorações opcionais

## Formato da Revisão

Sempre apresentar a revisão nesta ordem:

### Resumo
Breve visão geral da qualidade do código.

### Pontos Positivos
O que está correto.

### Problemas Críticos
Apenas problemas que exigem correção.

### Melhorias Recomendadas
Sugestões que agregam valor sem quebrar o padrão.

### Conclusão
Informar se o código está aprovado, precisa de ajustes, ou deve ser refatorado antes do merge.

## Saída

Relatório com: Resumo, Pontos Positivos, Problemas Críticos, Melhorias Recomendadas, Conclusão.

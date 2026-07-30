---
name: angular-component-creator
description: Use quando o usuário pedir para criar componentes Angular, refatorar componentes ou implementar novos componentes seguindo boas práticas.
---

# Angular Component Creator

## Descrição
Skill para criar componentes Angular seguindo boas práticas.

## Quando Usar
- Criar novos componentes
- Refatorar componentes existentes

## Fluxo Obrigatório

1. **Verificar se já existe** componente similar
2. **Definir responsabilidade** única
3. **Escolher tipo** (Smart/Dumb)
4. **Implementar** seguindo padrão do projeto
5. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

## Regras

### Componentes Devem Ser

- Pequenos e focados
- Tipados (TypeScript)
- Reutilizáveis
- Testáveis

### Smart Components

- Coordenação e estado
- Chamam Facades
- Templates simples

### Dumb Components

- Apenas apresentação
- Inputs e Outputs claros
- Sem lógica de negócio
- Sem chamadas HTTP

## Angular Moderno

- Standalone Components
- input() / output() / model()
- Signals para estado
- @if / @for / @switch
- track obrigatório em @for

## Nomenclatura

- Componentes: `nome-feature.component.ts`
- Templates: `nome-feature.component.html`
- Estilos: `nome-feature.component.scss`

## Saída Esperada

Arquivos do componente seguindo padrão do projeto.

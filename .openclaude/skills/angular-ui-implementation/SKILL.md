---
name: angular-ui-implementation
description: Use quando o usuário pedir para implementar interfaces Angular, criar templates HTML, implementar estilos SCSS ou garantir responsividade.
---

# Angular UI Implementation

## Descrição

Skill para implementar interfaces Angular (HTML/SCSS).

## Quando Usar

- Criar templates
- Implementar estilos
- Garantir responsividade

## Fluxo Obrigatório

1. **Ler ANGULAR_CONVENTIONS.MD** (se existir)
2. **Analisar padrão** visual existente
3. **Implementar** HTML semântico
4. **Implementar** SCSS Mobile First
5. **Garantir** acessibilidade
6. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

## HTML Semântico

### Preferir

- header, main, footer
- section, article, aside
- nav, figure, figcaption
- form, fieldset, legend
- button, label, dialog

### Evitar

- Excesso de divs
- Elementos não semânticos
- span clicável
- div como botão

## Acessibilidade

### Obrigatório

- aria-label quando necessário
- Labels em campos
- alt em imagens
- Navegação por teclado
- Focus visível

### Proibido

- Interfaces inacessíveis
- Remover outline sem substituir
- Contraste insuficiente

## SCSS

### Organização

1. Variáveis locais
2. Host
3. Layout
4. Componentes
5. Estados
6. Media Queries

### Preferir

- Flexbox / Grid
- Gap ao invés de margin
- clamp() para responsivo
- variáveis CSS

### Evitar

- !important
- Float
- Nesting profundo (>3)
- Seletores específicos

## Responsividade

- Mobile First (sempre)
- Breakpoints: mobile → tablet → desktop → wide
- Usar rem/em/% ao invés de px

## Angular Templates

- @if / @for / @switch
- track obrigatório em @for
- Sem lógica complexa no HTML
- Preferir computed/signals

## Saída

Arquivos .html e .scss seguindo padrão do projeto.

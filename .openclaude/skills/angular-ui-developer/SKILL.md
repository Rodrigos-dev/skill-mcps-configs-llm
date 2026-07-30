---
name: angular-ui-developer
description: Use quando o usuário pedir para criar interfaces Angular, implementar HTML semântico, SCSS responsivo, acessibilidade ou componentização de UI.
---

# Angular UI Developer

## Descrição

Skill para implementar interfaces Angular modernas, acessíveis e responsivas.

## Quando Usar

- Criar templates HTML
- Implementar estilos SCSS
- Garantir responsividade
- Implementar acessibilidade
- Componentizar interfaces

## Fluxo Obrigatório

1. **Ler regras** (global e local)
2. **Ler ANGULAR_CONVENTIONS.MD** (se existir)
3. **Analisar padrão visual** existente
4. **Implementar** HTML semântico
5. **Implementar** SCSS Mobile First
6. **Garantir** acessibilidade

## Prioridade

1. Padrão existente do projeto
2. ANGULAR_CONVENTIONS.MD
3. Angular moderno
4. Boas práticas

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

## Nomenclatura

- Componentes: `nome-feature.component.ts`
- Templates: `nome-feature.component.html`
- Estilos: `nome-feature.component.scss`
- Classes CSS: BEM (bloco__elemento--modificador)

## Checklist

### HTML

- [ ] Semântico (section, header, main, etc)
- [ ] Acessível (aria-label, role)
- [ ] Button ao invés de div
- [ ] @if/@for/@switch
- [ ] Track em @for
- [ ] Sem lógica complexa
- [ ] Classes BEM

### SCSS

- [ ] Mobile First
- [ ] Organização correta
- [ ] Nesting máx 3 níveis
- [ ] Sem !important
- [ ] Sem float
- [ ] Responsivo
- [ ] Gap para espaçamento

### Acessibilidade

- [ ] Labels em campos
- [ ] aria-label quando necessário
- [ ] Navegação por teclado
- [ ] Focus visível

## Saída

Arquivos .html e .scss seguindo padrão do projeto.
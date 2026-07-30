---
name: angular-master-component
description: Use quando o usuário pedir para criar componentes Angular completos com HTML, SCSS e TS seguindo o padrão do projeto.
---

# Angular Master Component

## Descrição

Skill completa para criar componentes Angular com HTML, SCSS e TS seguindo o padrão do projeto.

## Quando Usar

- Criar novos componentes completos
- Implementar interface de componente do zero
- Quando precisar dos 3 arquivos (TS + HTML + SCSS)

## Fluxo Obrigatório

1. **Ler regras** (global e local)
2. **Ler ANGULAR_CONVENTIONS.MD** (se existir)
3. **Analisar padrão** existente do projeto
4. **Verificar se já existe** componente similar reutilizável
5. **Definir tipo** (Smart/Dumb)
6. **Implementar** os 3 arquivos seguindo padrão
7. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

## Estrutura do Componente

```
nome-feature/
  nome-feature.component.ts
  nome-feature.component.html
  nome-feature.component.scss
```

---

## 1. TypeScript (`.component.ts`)

### Regras Obrigatórias

```typescript
import { Component, input, output, signal, computed } from '@angular/core';

@Component({
  selector: 'app-nome-feature',
  standalone: true,
  templateUrl: './nome-feature.component.html',
  styleUrl: './nome-feature.component.scss',
})
export class NomeFeatureComponent {
  // Inputs com input()
  titulo = input.required<string>();
  dados = input<DadosType[]>([]);

  // Outputs com output()
  itemClicado = output<DadosType>();
  fechar = output<void>();

  // Estado com signals
  isLoading = signal(false);
  searchText = signal('');

  // Computed
  itensFiltrados = computed(() => {
    const termo = this.searchText().toLowerCase();
    return this.dados().filter(d => d.nome.toLowerCase().includes(termo));
  });

  // Métodos
  onClicar(item: DadosType): void {
    this.itemClicado.emit(item);
  }
}
```

### Regras TypeScript

- **Standalone**: sempre `standalone: true`
- **Inputs**: usar `input()` ou `input.required()`
- **Outputs**: usar `output()`
- **Estado**: usar `signal()`
- **Derivados**: usar `computed()`
- **Inject**: usar `inject()` ao invés de constructor
- **Tipagem**: sem `any`, interfaces com `I`, enums com `E`
- **Readonly**: quando aplicável
- **DestroyRef**: usar `takeUntilDestroyed()` para subscriptions

### Nomenclatura TS

- Interface: `IUser`, `IProduct`
- Enum: `EStatus`, `ERole`
- Boolean: `isLoading`, `hasPermission`, `canEdit`
- Signal: `users` (sem $)
- Observable: `users$` (com $)

---

## 2. HTML (`.component.html`)

### Regras Obrigatórias

```html
<!-- HTML semântico e acessível -->
<section class="nome-feature">
  <header class="nome-feature__header">
    <h2>{{ titulo() }}</h2>
  </header>

  <main class="nome-feature__content">
    @if (isLoading()) {
    <div class="nome-feature__loading" role="status">
      <span>Carregando...</span>
    </div>
    } @else if (itensFiltrados().length === 0) {
    <div class="nome-feature__empty">
      <p>Nenhum item encontrado.</p>
    </div>
    } @else {
    <ul class="nome-feature__lista">
      @for (item of itensFiltrados(); track item.id) {
      <li class="nome-feature__item">
        <button
          type="button"
          (click)="onClicar(item)"
          [attr.aria-label]="'Selecionar ' + item.nome"
        >
          {{ item.nome }}
        </button>
      </li>
      }
    </ul>
    }
  </main>

  <footer class="nome-feature__footer">
    <button type="button" (click)="fechar.emit()">Fechar</button>
  </footer>
</section>
```

### Regras HTML

- **Semântico**: usar header, main, section, article, footer, nav, button, label
- **Acessibilidade**: aria-label, role, alt, labels associados
- **Semântica**: button ao invés de div clicável
- **Controle fluxo**: @if, @for, @switch (nunca *ngIf, *ngFor)
- **Track**: sempre em @for com `track item.id`
- **Sem lógica**: não colocar funções complexas no template
- **Classes**: BEM (bloco\_\_elemento--modificador)

### Estrutura CSS Classes (BEM)

```
.componente
.componente__header
.componente__content
.componente__item
.componente--ativo
.componente--desabilitado
```

### Proibido no HTML

- Div como botão
- Span clicável
- Lógica complexa
- Funções no template
- ngClass/ngStyle (usar @class/@style)

---

## 3. SCSS (`.component.scss`)

### Regras Obrigatórias

```scss
// 1. Variáveis locais (se necessário)
$componente-padding: 1rem;

// 2. Host
:host {
  display: block;
}

// 3. Layout
.nome-feature {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: $componente-padding;

  // 4. Componentes internos
  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  &__content {
    flex: 1;
    min-height: 0;
  }

  &__lista {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    list-style: none;
    padding: 0;
    margin: 0;
  }

  &__item {
    display: flex;
    align-items: center;
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;
    transition: background-color 0.2s ease;

    &:hover {
      background-color: rgba(0, 0, 0, 0.05);
    }
  }

  // 5. Estados
  &__loading,
  &__empty {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 2rem;
    color: #666;
  }

  // 6. Responsividade
  @media (min-width: 768px) {
    padding: 1.5rem;
  }

  @media (min-width: 1024px) {
    padding: 2rem;
  }
}
```

### Regras SCSS

- **Mobile First**: sempre começar do mobile
- **Organização**: host → layout → componentes → estados → responsivo
- **Nesting**: máximo 3 níveis
- **Seletores**: simples, evitar IDs
- **Unidades**: rem, em, %, clamp() (evitar px)
- **Espaçamento**: gap ao invés de margin
- **Layout**: Flexbox/Grid
- **Variáveis**: CSS Variables ou SCSS vars
- **Transições**: apenas transform e opacity

### Proibido no SCSS

- !important
- Float
- Nesting profundo (>3)
- Seletores específicos
- Inline styles
- @extend complicado

### Breakpoints Padrão

```scss
// Mobile: padrão (até 767px)
// Tablet: 768px
// Desktop: 1024px
// Wide: 1440px

@media (min-width: 768px) {
  /* Tablet */
}
@media (min-width: 1024px) {
  /* Desktop */
}
@media (min-width: 1440px) {
  /* Wide */
}
```

---

## Checklist de Validação

### TypeScript

- [ ] Standalone: true
- [ ] Inputs com input()/input.required()
- [ ] Outputs com output()
- [ ] Estado com signal()
- [ ] Derivados com computed()
- [ ] Sem any
- [ ] Interfaces com I
- [ ] Enums com E
- [ ] Boolean com is/has/can/should

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

---

## Saída Esperada

3 arquivos seguindo padrão do projeto:

1. `nome-feature.component.ts`
2. `nome-feature.component.html`
3. `nome-feature.component.scss`

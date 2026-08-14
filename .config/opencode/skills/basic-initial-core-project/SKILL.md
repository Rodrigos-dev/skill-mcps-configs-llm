# Skill: basic-initial-core-project

## Descrição

Use quando o usuário pedir para criar novas pages, componentes, services ou features neste projeto Angular + Ionic.

**Project Name:** basic-initial-core-full
**Framework:** Angular 20 + Ionic 8 + Capacitor 8 + TypeScript 5.9
**Arquitetura:** DDD + Clean Architecture + SOLID (Feature First)

---

## 🏗️ Estrutura do Projeto

```
src/app/
├── core/                          # Core independente (NÃO importa Features)
│   ├── guards/                    # Guards de rota (funções CanActivateFn)
│   ├── interceptors/              # Interceptors HTTP (8 ativos)
│   └── providers/                 # Providers centrais
│
├── shared/                        # Shared "burro" (NÃO importa Core nem Features)
│   ├── components/                # Componentes compartilhados
│   ├── constants/                 # Constantes (routes, forms, address)
│   ├── enums/                     # Enums por domínio
│   ├── interfaces/                # Interfaces por domínio (prefixo I)
│   ├── layouts/                   # Layouts (BasePagesLayoutComponent)
│   ├── services/                  # Services (DI com InjectionToken)
│   ├── stores/                    # Stores (signals)
│   └── utils/                     # Utilitários
│
├── features/                      # Features lazy-loaded (domínios)
│   ├── auth/                      # Autenticação
│   │   ├── pages/
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   └── forgot-password/
│   │   ├── auth.routes.ts
│   │   └── auth.routes.spec.ts
│   │
│   ├── home/                      # Home
│   │   ├── pages/
│   │   │   └── home/
│   │   └── home.routes.ts
│   │
│   └── settings/                  # Configurações
│       ├── pages/
│       │   └── settings/
│       └── settings.routes.ts
│
├── app.component.ts
├── app.config.ts
├── app.routes.ts
└── environments/
    ├── environment.ts
    └── environment.prod.ts
```

---

## 📄 Estrutura Padrão de uma Page

```
src/app/features/[feature]/pages/[page]/
├── [page].page.ts           # Componente principal
├── [page].page.html         # Template
├── [page].page.scss         # Estilos
├── [page].page.spec.ts      # Testes unitários
└── forms-configs/           # Opcional: config de formulário
    └── [page]-form-config-fields.ts
```

---

## 📝 Template Padrão: Page Simples (Sem Layout)

```typescript
// [page].page.ts
import { Component, signal } from '@angular/core';
import { CommonModule } from '@angular/common';
import { Router } from '@angular/router';
import { 
  IonContent, 
  IonButton, 
  IonIcon 
} from '@ionic/angular/standalone';

@Component({
  selector: 'app-[page]',
  standalone: true,
  imports: [
    CommonModule,
    IonContent,
    IonButton,
    IonIcon,
  ],
  templateUrl: './[page].page.html',
  styleUrls: ['./[page].page.scss'],
})
export class [Page]Page {
  isLoading = signal(false);

  constructor(private router: Router) {}

  async navigateTo(path: string): Promise<void> {
    await this.router.navigate([path]);
  }
}
```

```html
<!-- [page].page.html -->
<ion-content class="ion-padding">
  <h1>[Page Title]</h1>
  
  <ion-button expand="block" (click)="navigateTo('/home')">
    Go to Home
  </ion-button>
</ion-content>
```

```scss
// [page].page.scss
:host {
  display: block;
  height: 100%;
}
```

---

## 📝 Template Padrão: Page com Layout (BasePagesLayoutComponent)

```typescript
// [page].page.ts
import { Component, signal, inject } from '@angular/core';
import { CommonModule } from '@angular/common';
import { BasePagesLayoutComponent } from '@shared/layouts/base-pages-layout/base-pages-layout.component';
import { 
  IonContent, 
  IonList, 
  IonItem, 
  IonLabel,
  IonIcon 
} from '@ionic/angular/standalone';

@Component({
  selector: 'app-[page]',
  standalone: true,
  imports: [
    CommonModule,
    BasePagesLayoutComponent,
    IonContent,
    IonList,
    IonItem,
    IonLabel,
    IonIcon,
  ],
  templateUrl: './[page].page.html',
  styleUrls: ['./[page].page.scss'],
})
export class [Page]Page {
  isLoading = signal(false);
  
  // Dados para o menu (se necessário)
  menuItems = [
    { title: 'Item 1', icon: 'home', route: '/home' },
    { title: 'Item 2', icon: 'settings', route: '/settings' },
  ];
}
```

```html
<!-- [page].page.html -->
<app-base-pages-layout
  [pageTitle]="'[Page Title]'"
  [showBackButton]="true"
  [showMenu]="true"
>
  <ion-content class="ion-padding">
    <ion-list>
      <ion-item *ngFor="let item of menuItems">
        <ion-icon [name]="item.icon" slot="start"></ion-icon>
        <ion-label>{{ item.title }}</ion-label>
      </ion-item>
    </ion-list>
  </ion-content>
</app-base-pages-layout>
```

---

## 🛣️ Configuração de Rotas

### app.routes.ts (Principal)

```typescript
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: '',
    redirectTo: 'auth',
    pathMatch: 'full',
  },
  {
    path: 'auth',
    loadChildren: () => 
      import('./features/auth/auth.routes').then(m => m.AUTH_ROUTES),
  },
  {
    path: 'home',
    loadChildren: () => 
      import('./features/home/home.routes').then(m => m.HOME_ROUTES),
  },
  {
    path: 'settings',
    loadChildren: () => 
      import('./features/settings/settings.routes').then(m => m.SETTINGS_ROUTES),
  },
];
```

### feature.routes.ts (Exemplo: auth.routes.ts)

```typescript
import { Routes } from '@angular/router';

export const AUTH_ROUTES: Routes = [
  {
    path: '',
    redirectTo: 'login',
    pathMatch: 'full',
  },
  {
    path: 'login',
    loadComponent: () => 
      import('./pages/login/login.page').then(m => m.LoginPage),
  },
  {
    path: 'register',
    loadComponent: () => 
      import('./pages/register/register.page').then(m => m.RegisterPage),
  },
  {
    path: 'forgot-password',
    loadComponent: () => 
      import('./pages/forgot-password/forgot-password.page').then(m => m.ForgotPasswordPage),
  },
];
```

### routes.constants.ts (Constantes)

```typescript
export const APP_ROUTES = {
  AUTH: {
    LOGIN: '/auth/login',
    REGISTER: '/auth/register',
    FORGOT_PASSWORD: '/auth/forgot-password',
    FULL_LOGIN: 'auth/login',
    FULL_REGISTER: 'auth/register',
    FULL_FORGOT_PASSWORD: 'auth/forgot-password',
  },
  HOME: {
    MAIN: '/home',
    FULL_MAIN: 'home',
  },
  SETTINGS: {
    MAIN: '/settings',
    FULL_MAIN: 'settings',
  },
} as const;
```

---

## 🔧 Services (DI com InjectionToken)

### Estrutura Padrão

```
src/app/shared/services/[domain]/
├── [domain].api.service.ts    # Interface + InjectionToken
├── [domain].service.ts        # Implementação real
├── [domain].mock.service.ts   # Implementação mock
└── [domain]-config.service.ts # Flag individual
```

### Exemplo: User Service

```typescript
// user.api.service.ts
import { InjectionToken } from '@angular/core';

export interface IUserService {
  getUser(id: string): Promise<any>;
  updateUser(id: string, data: any): Promise<any>;
}

export const USER_SERVICE = new InjectionToken<IUserService>('UserService');
```

```typescript
// user.service.ts
import { Injectable } from '@angular/core';
import { IUserService } from './user.api.service';

@Injectable()
export class UserService implements IUserService {
  async getUser(id: string): Promise<any> {
    // Implementação real (API)
  }

  async updateUser(id: string, data: any): Promise<any> {
    // Implementação real (API)
  }
}
```

```typescript
// user.mock.service.ts
import { Injectable } from '@angular/core';
import { IUserService } from './user.api.service';

@Injectable()
export class UserMockService implements IUserService {
  async getUser(id: string): Promise<any> {
    return { id, name: 'Mock User' };
  }

  async updateUser(id: string, data: any): Promise<any> {
    return { id, ...data };
  }
}
```

```typescript
// user-config.service.ts
import { InjectionToken } from '@angular/core';

export const USE_USER_CONFIG_MOCK = new InjectionToken<boolean>('UseUserConfigMock');
```

### Registro no shared.provider.ts

```typescript
import { Provider } from '@angular/core';
import { USER_SERVICE } from './services/user/user.api.service';
import { UserService } from './services/user/user.service';
import { UserMockService } from './services/user/user.mock.service';
import { USE_USER_CONFIG_MOCK } from './services/user/user-config.service';
import { USE_MOCK_GLOBAL } from './services/global-config.service';

export function provideMockService<T>(
  token: InjectionToken<T>,
  real: Type<T>,
  mock: Type<T>,
  individualFlag: InjectionToken<boolean>,
  globalFlag: InjectionToken<boolean> = USE_MOCK_GLOBAL
): Provider[] {
  return [
    { provide: token, useClass: UserService },
    { provide: USE_USER_CONFIG_MOCK, useValue: false },
  ];
}

// OU forma simplificada
export const APP_PROVIDERS: Provider[] = [
  ...provideMockService(USER_SERVICE, UserService, UserMockService, USE_USER_CONFIG_MOCK),
];
```

---

## 🧪 Testes Unitários (Vitest)

### Estrutura Padrão

```typescript
// [page].page.spec.ts
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { describe, it, expect, vi, beforeEach } from 'vitest';
import { [Page]Page } from './[page].page';

describe('[Page]Page', () => {
  let component: [Page]Page;
  let fixture: ComponentFixture<[Page]Page>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      imports: [[Page]Page],
      providers: [
        // Mocks de services via InjectionToken
        { provide: USER_SERVICE, useValue: { getUser: vi.fn() } },
      ],
    }).compileComponents();

    fixture = TestBed.createComponent([Page]Page);
    component = fixture.componentInstance;
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

  it('should have isLoading false initially', () => {
    expect(component.isLoading()).toBe(false);
  });
});
```

### Comando para Testar

```bash
# Testar arquivo específico
node "D:/2 - workspace/4 - basic inicial core angular ionic/basic-initial-core-full/node_modules/vitest/vitest.mjs" run "src/app/features/[feature]/pages/[page]/[page].page.spec.ts"

# Testar feature inteira
npx vitest run src/app/features/[feature] --coverage --silent
```

---

## 📦 Imports Ionic Standalone

```typescript
// Sempre importar componentes individualmente
import { 
  IonContent,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonButton,
  IonIcon,
  IonList,
  IonItem,
  IonLabel,
  IonInput,
  IonTextarea,
  IonSelect,
  IonSelectOption,
  IonCheckbox,
  IonRadio,
  IonRadioGroup,
  IonToggle,
  IonDatetime,
  IonImg,
  IonAvatar,
  IonBadge,
  IonChip,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonFab,
  IonFabButton,
  IonRefresher,
  IonRefresherContent,
  IonInfiniteScroll,
  IonInfiniteScrollContent,
  IonSkeletonText,
  IonSpinner,
  IonToast,
  IonModal,
  IonPopover,
  IonAlert,
  IonLoading,
  IonActionSheet,
  IonNote,
  IonText,
  IonBackButton,
  IonButtons,
  IonMenuButton,
  IonSearchbar,
  IonSegment,
  IonSegmentButton,
  IonTabBar,
  IonTabButton,
  IonTabs,
  IonRippleEffect,
  IonFooter,
  IonThumbnail,
  IonItemDivider,
  IonItemGroup,
  IonItemSliding,
  IonItemOptions,
  IonLabel,
} from '@ionic/angular/standalone';
```

---

## ⚠️ Regras de Arquitetura (ESLint)

| Regra | Descrição |
|-------|-----------|
| Features não importam Features | Comunique via `core/` ou `shared/` |
| Core não importa Features | Core é independente |
| Shared não importa Core nem Features | Shared é "burro" |
| Fluxo | Component → Service (via Token) → HttpService → Interceptors → API |

---

## 🎯 Convenções de Nomenclatura

| Tipo | Padrão | Exemplo |
|------|--------|---------|
| Interfaces | prefixo `I` | `IUserLogged` |
| Enums | sufixo `Enum` | `MenuTypeEnum` |
| Booleanos | `is/has/can/should` | `isLoading` |
| Signals | sem `$` | `userSignal` |
| Observables | sufixo `$` | `user$` |
| Arquivos | kebab-case | `user.service.ts` |
| Suffix classes | `Page` ou `Component` | `LoginPage` |

---

## 🚀 Checklist ao Criar Nova Page

- [ ] Criar pasta `src/app/features/[feature]/pages/[page]/`
- [ ] Criar 4 arquivos: `.ts`, `.html`, `.scss`, `.spec.ts`
- [ ] Criar `forms-configs/` se tiver formulário
- [ ] Adicionar rota em `[feature].routes.ts`
- [ ] Adicionar rota em `app.routes.ts` (lazy loading)
- [ ] Adicionar constante em `routes.constants.ts`
- [ ] Usar `BasePagesLayoutComponent` para pages internas
- [ ] Importar componentes Ionic standalone individualmente
- [ ] Usar InjectionToken para services (nunca classe diretamente)
- [ ] Criar testes unitários com Vitest
- [ ] Verificar imports (features não importam features)

---

## 📚 Referências

- `src/app/features/auth/` - Exemplo completo de feature (login, register, forgot-password)
- `src/app/shared/layouts/` - Layouts compartilhados
- `src/app/shared/services/` - Services com DI pattern
- `src/app/core/interceptors/` - 8 interceptors HTTP ativos
- `src/app/core/guards/` - Guards de rota (funções CanActivateFn)

---

> Última atualização: 2026-08-13
> Projeto: basic-initial-core-full
> Stack: Angular 20 + Ionic 8 + Capacitor 8 + TypeScript 5.9

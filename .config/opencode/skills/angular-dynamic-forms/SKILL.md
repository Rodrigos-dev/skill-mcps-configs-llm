# Skill: angular-dynamic-forms

## Descrição

Use quando o usuário pedir para criar, configurar ou modificar formulários dinâmicos usando a lib `@Rodrigos-dev/ars-dynamic-form` neste projeto Angular + Ionic.

**Documenta:** Configuração de campos, validações, mascaras, multi-step, persistência LocalStorage, e padrões arquiteturais.

---

## 📦 Dependência

```json
"@Rodrigos-dev/ars-dynamic-form": "npm:@Rodrigos-dev/ars-dynamic-form@^0.0.90"
```

**Peer Dependencies:** Angular 18/19/20, Ionic 8, Capacitor 6/7/8

---

## 🗂️ Estrutura de Pastas

```
src/app/
├── features/[feature]/pages/[page]/
│   ├── [page].page.ts
│   ├── [page].page.html
│   ├── [page].page.scss
│   └── forms-configs/                          ← PASTA DO FORMULÁRIO
│       └── [nome]-form-config-fields.ts        ← CONFIG DOS CAMPOS
│
├── shared/constants/forms/
│   ├── form-base-configs-default.ts            ← DEFAULTS GLOBAIS
│   ├── forms-names.constants.ts                ← NOMES DE STORAGE
│   └── forms-rules-regex-password.ts           ← REGEX SENHA
```

---

## 🔧 Imports Necessários

```typescript
// Componentes e interfaces
import { 
  DynamicFormComponent,
  IDynamicFormFieldsConfig,
  IDynamicFormContainerConfig,
  EFieldDynamicForm,
  EInputModeField,
  EMaskInputs,
  ValidatorDocumentsAndMore,
  Base_Model_4_Initial_Model_Form_Defaults_Fields_Configs
} from '@Rodrigos-dev/ars-dynamic-form';
```

---

## 📐 Interface Principal: IDynamicFormFieldsConfig

```typescript
interface IDynamicFormFieldsConfig {
  name: string;                    // formControlName
  typeFieldForm: EFieldDynamicForm; // tipo do campo
  initialValue?: any;              // valor inicial
  disabled?: boolean;              // desabilitado
  validations?: ValidatorFn | ValidatorFn[]; // validators Angular
  defaultAllFieldsConfigs?: IDefaultAllFieldsConfigs; // grid, bordas
  itemContainerFieldsConfigs?: IItemContainerFieldsConfigs; // padding
  baseFieldsConfigs?: IBaseConfigsFormFields; // config específica do tipo
}
```

---

## 🎨 Tipos de Campo Disponíveis (EFieldDynamicForm)

| Tipo | Uso |
|------|-----|
| `INPUT` | Campo de texto (email, password, text, tel, number) |
| `INPUT_NUMBER` | Campo numérico |
| `SELECT` | Dropdown/select |
| `TEXTAREA` | Área de texto |
| `CHECKBOX` | Checkbox |
| `DATE` | Seletor de data |
| `TIME` | Seletor de hora |
| `DATE_TIME` | Data + Hora |
| `SWITCH` | Toggle/switch |
| `AVATAR` | Upload de imagem |
| `TERMS_POLICY` | Termos e políticas |
| `SELECT_USER` | Seleção de usuário |
| `DIVIDER` | Separador visual com título |
| `RADIO` | Radio button |
| `IMAGE` | Upload de imagem |
| `VIDEO` | Upload de vídeo |
| `VIDEOIMAGEORDOCUMENTS` | Upload misto |
| `SIGNATURE` | Assinatura digital |

---

## 📝 Exemplos Reais de Configuração

### Campo INPUT (Email)

```typescript
{
  name: 'email',
  typeFieldForm: EFieldDynamicForm.INPUT,
  validations: [Validators.required, Validators.email],
  initialValue: undefined,
  disabled: undefined,
  defaultAllFieldsConfigs: defaultAllFieldsConfigsUse,
  itemContainerFieldsConfigs: itemContainerFieldsConfigUse,
  baseFieldsConfigs: {
    inputConfigs: {
      eInputModeField: EInputModeField.EMAIL,
      placeholderInput: 'Enter your email',
      labelInput: 'Email',
      iconNameInput: 'mail',
      iconFontSizeInput: '16px',
    },
  },
}
```

### Campo INPUT (Password) com Botões Abaixo

```typescript
{
  name: 'password',
  typeFieldForm: EFieldDynamicForm.INPUT,
  validations: [Validators.required, Validators.minLength(6)],
  defaultAllFieldsConfigs: defaultAllFieldsConfigsUse,
  itemContainerFieldsConfigs: itemContainerFieldsConfigUse,
  baseFieldsConfigs: {
    inputConfigs: {
      eInputModeField: EInputModeField.PASSWORD,
      placeholderInput: 'Enter password',
      labelInput: 'Password',
      showOrHideDataInFieldPassword: false,
    },
    buttonOneDownField: {                    // Checkbox "Remember Password"
      showButtonOneDownField: true,
      isCheckbox: true,
      checkboxValue: false,
      textButtonOneDownField: 'Remember Password',
      nameCheckBoxToVerify: 'rememberPassword',
    },
    buttonTwoDownField: {                    // Link "Forgot password?"
      showButtonTwoDownField: true,
      textButtonTwoDownField: 'Forgot password?',
      linkButtonTwoDownField: '/auth/forgot-password',
    },
  },
}
```

### Campo INPUT com Máscara (CPF)

```typescript
{
  name: 'document',
  typeFieldForm: EFieldDynamicForm.INPUT,
  validations: [Validators.required, ValidatorDocumentsAndMore.cpf()],
  baseFieldsConfigs: {
    inputConfigs: {
      eInputModeField: EInputModeField.TEXT,
      maskInput: EMaskInputs.Cpf,           // Máscara automática CPF
      placeholderInput: 'Enter your CPF',
      labelInput: 'CPF',
      iconNameInput: 'document-text',
    },
  },
}
```

### Campo INPUT com Validação de Igualdade

```typescript
{
  name: 'confirmPassword',
  typeFieldForm: EFieldDynamicForm.INPUT,
  validations: [Validators.required, Validators.minLength(6)],
  baseFieldsConfigs: {
    inputConfigs: {
      eInputModeField: EInputModeField.PASSWORD,
      placeholderInput: 'Confirm Password',
      labelInput: 'Confirm Password',
      valueEqualWithFieldFormName: 'password',  // Compara com campo 'password'
    },
  },
}
```

### Campo SELECT (Estados Brasileiros)

```typescript
{
  name: 'state',
  typeFieldForm: EFieldDynamicForm.SELECT,
  initialValue: '',
  defaultAllFieldsConfigs: { ...defaultAllFieldsConfigsUse, sizeGridMainColumn: 6 },
  baseFieldsConfigs: {
    selectConfigs: {
      selectLabel: 'State',
      selectPlaceholder: 'Select state',
      selectOptions: BRAZILIAN_STATES,  // [{ value: 'SP', label: 'São Paulo' }, ...]
      selectModeType: 'single',
    },
  },
}
```

### Campo SWITCH (Toggle)

```typescript
{
  name: 'receive_notifications',
  typeFieldForm: EFieldDynamicForm.SWITCH,
  initialValue: false,
  defaultAllFieldsConfigs: defaultAllFieldsConfigsUse,
  itemContainerFieldsConfigs: { ...itemContainerFieldsConfigUse, marginTopField: '10px' },
  baseFieldsConfigs: {
    toggleConfigs: {
      toggleLabel: 'Receive Notifications',
      toggleNote: 'Receive email notifications about updates',
      toggleFill: 'outline',
      toggleLabelPlacement: 'stacked',
    },
  },
}
```

### DIVIDER (Título Visual)

```typescript
{
  typeFieldForm: EFieldDynamicForm.DIVIDER,
  name: 'title',
  defaultAllFieldsConfigs: defaultAllFieldsConfigsUse,
  itemContainerFieldsConfigs: { ...itemContainerFieldsConfigUse, paddingStart: '15px' },
  itemDividerConfigs: {
    backgroundItemItemDivider: 'transparent',
    textAlignLabelItemDivider: 'left',
    colorLabelItemDivider: 'var(--ion-color-primary)',
    fontWeightLabelItemDivider: '900',
    fontSizeLabelItemDivider: '1.5rem',
    textLabelItemDivider: 'Welcome!',
    subTextLabelItemDivider: 'Sign in to continue',
    fontSizeSubTextItemDivider: '14px',
    colorSubTextItemDivider: 'var(--ion-color-secondary)',
  },
}
```

### Grid Layout (2 Colunas)

```typescript
// Campo ocupa metade (6 de 12 colunas):
defaultAllFieldsConfigs: { ...defaultAllFieldsConfigsUse, sizeGridMainColumn: 6 },

// Campo ocupa largura total (12 de 12):
defaultAllFieldsConfigs: { ...defaultAllFieldsConfigsUse, sizeGridMainColumn: 12 },
```

---

## 🎯 Padrão de Uso no Template (HTML)

### Formulário Simples (Login)

```html
<mb-dynamic-form
  [formConfigFields]="ILoginFormConfigs"
  (formValueChange)="onFormChange($event)"
  (listenFormValidStatus)="listenFormValidStatus($event)"
  [mbFormStorageName]="{
    name: keyNameFormStorage, 
    encrypt: false,
    key: secretKey,     
    enabled: rememberPassword()
  }"
  [formContainerConfig]="formContainerConfig"
></mb-dynamic-form>
```

### Formulário Multi-Step (Register)

```html
<!-- Step 1: Dados Pessoais -->
<mb-dynamic-form
  *ngIf="renderUserForm()"
  [formConfigFields]="userFormfieldsConfig"
  [formContainerConfig]="formContainerConfig"
  (formValueChange)="onFormChange($event, 'user')"
  (listenFormValidStatus)="listenFormValidStatus($event, 'user')"
  [mbFormStorageName]="{ name: 'undefined', encrypt: false, key: 'secretKey', enabled: false }"
></mb-dynamic-form>

<!-- Step 2: Endereço -->
<mb-dynamic-form
  *ngIf="renderAddressForm()"
  [formConfigFields]="addressFormfieldsConfig"
  [formContainerConfig]="formContainerConfig"
  (formValueChange)="onFormChange($event, 'address')"
  (listenFormValidStatus)="listenFormValidStatus($event, 'address')"
  [mbFormStorageName]="{ name: 'undefined', encrypt: false, key: 'secretKey', enabled: false }"
></mb-dynamic-form>
```

### Formulário com Reference (Acesso Direto)

```html
<mb-dynamic-form
  #formPassword
  [formConfigFields]="forgotPasswordFormConfigs"
  (formValueChange)="onFormChange($event, 'updateForgotPassword')"
  (listenFormValidStatus)="listenFormValidStatus($event)"
  [mbFormStorageName]="undefined"
  [formContainerConfig]="formContainerConfig"
></mb-dynamic-form>
```

---

## 🎯 Padrão de Uso no Component (TypeScript)

### Padrão Simples (Login)

```typescript
export class LoginPage {
  // 1. Config do form como função que retorna array
  ILoginFormConfigs = LOGIN_FORM_CONFIG();
  formContainerConfig = FORM_CONTAINER_CONFIG_DEFAULT;
  
  // 2. Signals para estado
  isFormValid = signal(false);
  isLoading = signal(false);

  // 3. Callback de mudança de valor
  onFormChange(form: ILoginForm) {
    this.submitForm = { email: form.email, password: form.password };
  }

  // 4. Callback de validade
  listenFormValidStatus(isValid: boolean) {
    this.isFormValid.set(isValid);
  }

  // 5. Submit - só funciona se form válido
  async login(): Promise<void> {
    if (!this.isFormValid() || this.isLoading()) return;
    // ... chamar API
  }
}
```

### Padrão Multi-Step (Register)

```typescript
// Dados retidos em memória entre steps
private userData: any = {};
private addressData: any = {};

// Rehidratação - injeta valores salvos no initialValue
private rehydrateFormConfigs(formType: 'user' | 'address'): void {
  const dataToApply = formType === 'user' ? this.userData : this.addressData;
  const configsToUpdate = formType === 'user' 
    ? this.userFormfieldsConfig 
    : this.addressFormfieldsConfig;
  
  configsToUpdate.forEach((field) => {
    if (dataToApply[field.name] !== undefined) {
      field.initialValue = dataToApply[field.name];
    }
  });
}

// Truque para destruir/recriar o form:
this.renderUserForm.set(false);    // remove do DOM
this.currentStep--;
setTimeout(() => {
  this.renderUserForm.set(true);   // recria limpo com dados rehidratados
}, 0);
```

### Acesso Direto ao FormGroup (ForgotPassword)

```typescript
@ViewChild('formPassword') passwordFormComponent!: DynamicFormComponent;

// Acessa o FormGroup interno da lib
const formGroup = this.passwordFormComponent?.form;
const isPasswordValid = !!formGroup.get('password')?.valid;
const confirmControl = formGroup.get('confirmPassword');

// Habilita/desabilita controle programaticamente
if (isPasswordValid) {
  confirmControl?.enable({ emitEvent: false });
} else {
  confirmControl?.disable({ emitEvent: false });
  confirmControl?.setValue('', { emitEvent: false });
}

// Modifica a config (afeta o template)
confirmField.disabled = !isPasswordValid;
```

### Rehidratação Dinâmica via Effect

```typescript
private readonly userEffect = effect(() => {
  const currentStoreUser = this.userStore.user();
  
  this.emailToCodeFormConfigs.forEach((field) => {
    if (field.name === 'email') {
      field.initialValue = user.email;
      field.baseFieldsConfigs.inputConfigs.readonlyInput = true;
      field.baseFieldsConfigs.inputConfigs.obfuscateField = true;
    }
  });
  
  // Destroi e recria o form
  this.codeFormRender.set(false);
  setTimeout(() => this.codeFormRender.set(true), 0);
});
```

---

## 🔐 Configuração de Storage (LocalStorage)

```typescript
interface IMbFormStorageConfig {
  name: string;       // chave no LocalStorage
  encrypt?: boolean;  // criptografia AES
  key?: string;       // chave secreta para cifrar
  enabled: boolean;   // ativa/desativa
}
```

**Uso no Login (Lembrar senha):**
```html
[mbFormStorageName]="{
  name: keyNameFormStorage,    // 'loginForm'
  encrypt: false,
  key: secretKey,              // environment.secretEncrypt
  enabled: rememberPassword()  // signal reativo
}"
```

**Uso sem persistência:**
```html
[mbFormStorageName]="undefined"
```

---

## ✅ Validadores Customizados (ValidatorDocumentsAndMore)

```typescript
ValidatorDocumentsAndMore.cpf()      // CPF (11 dígitos)
ValidatorDocumentsAndMore.cnpj()     // CNPJ (14 dígitos)
ValidatorDocumentsAndMore.rg()       // RG (9 dígitos, suporta 'X')
ValidatorDocumentsAndMore.cep()      // CEP (8 dígitos)
ValidatorDocumentsAndMore.cpfCnpj()  // Híbrido (detecta pelo tamanho)
```

---

## 🔑 Regex Rules para Senha

```typescript
// forms-rules-regex-password.ts
export const RULES_REGEX_PASSOWORD_FORM_CONFIGS = [
  { regex: '.{6,}', message: 'Minimum 6 characters' },
  { regex: '[A-Z]', message: 'At least one uppercase letter' },
  { regex: '[0-9]', message: 'At least one number' },
  { regex: '[!@#$%^&*]', message: 'At least one special character' },
];
```

**Uso:**
```typescript
baseFieldsConfigs: {
  inputConfigs: {
    eInputModeField: EInputModeField.PASSWORD,
    regexRules: RULES_REGEX_PASSOWORD_FORM_CONFIGS,
  },
}
```

---

## 📐 Config Base Default (form-base-configs-default.ts)

```typescript
import { 
  Base_Model_4_Initial_Model_Form_Defaults_Fields_Configs,
  IDynamicFormContainerConfig 
} from '@Rodrigos-dev/ars-dynamic-form';

// Model 4 como default global
export const defaultAllFieldsConfigsUse = 
  Base_Model_4_Initial_Model_Form_Defaults_Fields_Configs.defaultAllFieldsConfigs;

export const itemContainerFieldsConfigUse = 
  Base_Model_4_Initial_Model_Form_Defaults_Fields_Configs.itemContainerFieldsConfigs;

export const FORM_CONTAINER_CONFIG_DEFAULT: IDynamicFormContainerConfig = {
  paddingRightForm: '0',
  paddingLeftForm: '0',
  paddingBottomForm: '0',
  paddingTopForm: '0',
  maxWidthForm: '100%',
  gapFieldsForm: '5px',
};
```

---

## 📋 Checklist ao Criar Formulário

- [ ] Criar pasta `forms-configs/` na page
- [ ] Criar arquivo `[nome]-form-config-fields.ts`
- [ ] Exportar função que retorna `IDynamicFormFieldsConfig[]`
- [ ] Importar `defaultAllFieldsConfigsUse` e `itemContainerFieldsConfigUse`
- [ ] Configurar `validations` com validators Angular
- [ ] Usar `ValidatorDocumentsAndMore` para documentos (CPF, CNPJ, etc.)
- [ ] Configurar `baseFieldsConfigs` conforme tipo do campo
- [ ] Adicionar `<mb-dynamic-form>` no template
- [ ] Implementar `onFormChange()` e `listenFormValidStatus()`
- [ ] Configurar `mbFormStorageName` se necessário
- [ ] Configurar `formContainerConfig` se necessário

---

## ⚠️ Gotchas Conhecidos

1. **Form é destruído e recriado** para rehidratação - usar `setTimeout` com flag
2. **`valueEqualWithFieldFormName`** compara valores automaticamente
3. **`regexRules`** renderiza checklist visual - lib controla validade
4. **`@ViewChild`** pode ser necessário para acesso direto ao FormGroup
5. **`effect()`** do Angular pode ser usado para rehidratação reativa

---

> Última atualização: 2026-08-13
> Projeto: basic-initial-core-full (Angular 20 + Ionic 8)

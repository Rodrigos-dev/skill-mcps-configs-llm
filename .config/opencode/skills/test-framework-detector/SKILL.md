---
name: test-framework-detector
description: Use quando precisar detectar automaticamente qual framework de testes está configurado no projeto (Jest, Vitest, etc.).
---

# Skill: Detector de Framework de Testes

## Descrição
Detecta automaticamente qual framework de testes está configurado no projeto Angular e direciona para a skill correta.

## Quando usar
- Antes de criar, corrigir ou revisar testes unitários
- Quando o usuário pede para rodar testes
- Quando existe dúvida sobre qual framework usar

## Fluxo de Detecção

### Passo 1: Verificar package.json

```bash
# Windows (PowerShell)
Select-String -Path package.json -Pattern "jest|vitest|mocha|jasmine"

# Linux/Mac
grep -E "(jest|vitest|mocha|jasmine)" package.json
```

**Prioridade de detecção:**
1. `"vitest"` nas devDependencies → **Vitest**
2. `"jest"` ou `"@angular/cli"` com jest config → **Jest**
3. `"jasmine"` + `"karma"` → **Karma/Jasmine**
4. Ambos vitest e jest → **Perguntar ao usuário**

### Passo 2: Verificar Arquivos de Configuração

```
Procurar na raiz do projeto:
├── vitest.config.ts / vitest.config.js → Vitest
├── jest.config.ts / jest.config.js → Jest
├── karma.conf.js → Karma/Jasmine
└── angular.json (verificar builder)
```

### Passo 3: Verificar angular.json

```json
{
  "projects": {
    "meu-app": {
      "architect": {
        "test": {
          "builder": "@angular-builders/jest:run" → Jest
          "builder": "@angular-builders/vitest:run" → Vitest
          "builder": "@angular-devkit/build-angular:karma" → Karma/Jasmine
        }
      }
    }
  }
}
```

### Passo 4: Fallback

Se nenhum for encontrado:
1. Perguntar ao usuário: "Qual framework de testes você deseja usar?"
2. Opções: Jest, Vitest, Karma/Jasmine
3. Usar a skill correspondente

## Regras de Direcionamento

| Framework Detectado | Skill a Usar |
|---------------------|--------------|
| Vitest | `unit-test-vitest` |
| Jest | `unit-test-jest` |
| Karma/Jasmine | `unit-test-jasmine` (quando existir) |
| Nenhum/Outro | Perguntar ao usuário |

## Comandos de Verificação

```bash
# Verificar se vitest está instalado (Windows)
npx vitest --version

# Verificar se jest está instalado (Windows)
npx jest --version

# Verificar configuração do projeto (Windows)
Get-Content angular.json | Select-String -Pattern '"test"' -Context 0,5

# Verificar package.json (Windows)
Get-Content package.json | Select-String -Pattern "jest|vitest"
```

## Exemplo de Detecção via package.json

```json
{
  "name": "meu-app",
  "devDependencies": {
    "jest": "^29.7.0",
    "@angular/cli": "^17.0.0"
  }
}
```

**Resultado:** Jest detectado (tem "jest" nas devDependencies)

```json
{
  "name": "meu-app",
  "devDependencies": {
    "vitest": "^1.6.0",
    "@analogjs/vite-plugin-angular": "^1.0.0"
  }
}
```

**Resultado:** Vitest detectado (tem "vitest" nas devDependencies)

## Saída Esperada

```
🔍 Framework de testes detectado: Vitest
📁 Configuração: vitest.config.ts
📦 Versão: 1.6.0

Usando skill: unit-test-vitest
```

ou

```
🔍 Framework de testes detectado: Jest
📁 Configuração: jest.config.ts
📦 Versão: 29.7.0

Usando skill: unit-test-jest
```

ou

```
⚠️ Nenhum framework de testes detectado

Qual framework você deseja usar?
1. Vitest (recomendado para projetos Vite)
2. Jest (recomendado para projetos Angular tradicionais)
3. Karma/Jasmine (padrão Angular antigo)
```
# 🤖 Skill-MCPS-Configs-LLM

> Repositório centralizado de configurações, skills e agents para múltiplos LLMs (OpenCode, Gemini, Continue, Claude, OpenClaude)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/Rodrigos-dev/skill-mcps-configs-llm.svg?style=social)](https://github.com/Rodrigos-dev/skill-mcps-configs-llm/stargazers)

---

## 📋 Visão Geral

Este repositório contém todas as configurações padronizadas para diferentes LLMs, garantindo sincronização automática e consistência entre todas as ferramentas de IA utilizadas no desenvolvimento.

### 🎯 Objetivo

- **Sincronização Centralizada**: Uma única fonte verdadeira para todas as configs
- **Replicação Automática**: Skills e agents replicados para todos os LLMs
- **Padronização**: Convenções e regras consistentes em todas as ferramentas
- **Backup Global**: Cópia de segurança em diretório separado

---

## 🏗️ Estrutura do Repositório

```
skill-mcps-configs-llm/
├── 📁 .config/opencode/          # Configuração principal (OpenCode)
│   ├── 📁 agents/                # Agents especializados
│   ├── 📁 rules/                 # Regras de segurança e convenções
│   ├── 📁 skills/                # Skills funcionais (16 skills)
│   └── 📄 opencode.md            # Config principal
│
├── 📁 .gemini/                   # Config Google Gemini
│   ├── 📁 agents/
│   ├── 📁 skills/
│   ├── 📁 .rules/
│   └── 📄 GEMINI.md
│
├── 📁 .continue/                 # Config Continue
│   ├── 📁 agents/
│   ├── 📁 skills/
│   ├── 📁 rules/
│   └── 📄 CONTINUE.md
│
├── 📁 .claude/                   # Config Claude
│   ├── 📁 agents/
│   ├── 📁 skills/
│   ├── 📁 rules/
│   └── 📄 CLAUDE.md
│
├── 📁 .openclaude/               # Config OpenClaude
│   ├── 📁 agents/
│   ├── 📁 skills/
│   ├── 📁 rules/
│   └── 📄 CLAUDE.md
│
├── 📄 .gitignore                 # Arquivos excluídos do versionamento
└── 📄 README.md                  # Este arquivo
```

---

## 🔧 Skills Disponíveis

### 🛠️ Desenvolvimento Angular

| Skill | Descrição | Uso |
|-------|-----------|-----|
| `angular-architect` | Arquitetura DDD, Clean Architecture, SOLID | Planejamento de estrutura |
| `angular-architecture-check` | Verificação de conformidade arquitetural | Audit de código |
| `angular-code-review` | Revisão de código e qualidade | Code review |
| `angular-component-creator` | Criação de componentes Angular | Novos componentes |
| `angular-conventions-checker` | Verificação de convenções | Padronização |
| `angular-master-component` | Componentes completos (TS+HTML+SCSS) | Implementação full |
| `angular-ui-developer` | Interfaces, HTML, SCSS, acessibilidade | UI/UX |
| `angular-ui-implementation` | Implementação de templates e estilos | Frontend |

### 📚 Utilitários

| Skill | Descrição | Uso |
|-------|-----------|-----|
| `git-commit-generate` | Geração de mensagens Conventional Commits | Versionamento |
| `homem-das-cavernas` | Modo direto e didático | Explicações rápidas |
| `onp-spec-driven` | Metodologia Spec-Driven Development | Planejamento SDD |
| `replicate-configs` | Replicação automática de configs | Sincronização |
| `session-init` | Inicialização de sessão | Setup inicial |
| `session-manager` | Gerenciamento de sessões | Controle de estado |
| `site-blog-creator` | Criação de sites e blogs | Projetos web |
| `technical-documentation` | Documentação técnica Angular | Docs |

---

## 👥 Agents

### Desenvolvimento

- **developer-orquestrador**: Tech Lead Mestre que orquestra especialistas
  - Auto-detecção de framework
  - Classificação dinâmica de tarefas
  - Uso de MCPs com autorização
  - Pipeline de execução completo

---

## 🔄 Sistema de Replicação

### Como Funciona

```javascript
// Ao criar ou alterar qualquer configuração:
skill({ name: "replicate-configs" })

// A skill replica automaticamente para:
// - .gemini/
// - .continue/
// - .claude/
// - .openclaude/
// - Backup global
```

### Fluxo de Replicação

```
1. Criar/alterar em .config/opencode/
2. Chamar skill replicate-configs
3. Sistema detecta automaticamente
4. Replica para todos os diretórios
5. Ajusta caminhos específicos
6. Confirma replicação ao usuário
```

---

## 📁 Diretórios de Destino

| Destino | Caminho | Tipo |
|---------|---------|------|
| **OpenCode** | `C:\Users\Acer\.config\opencode\` | Referência original |
| **Gemini** | `C:\Users\Acer\.gemini\` | LLM Google |
| **Continue** | `C:\Users\Acer\.continue\` | LLM Continue |
| **Claude** | `C:\Users\Acer\.claude\` | LLM Anthropic |
| **OpenClaude** | `C:\Users\Acer\.openclaude\` | LLM OpenClaude |
| **Backup** | `D:\...\configs global ias local em uso\` | Backup global |

---

## 🚀 Início Rápido

### 1. Clone o Repositório

```bash
git clone https://github.com/Rodrigos-dev/skill-mcps-configs-llm.git
```

### 2. Copie as Configurações

Copie a pasta `.config/opencode/` para seu diretório de configuração local.

### 3. Use as Skills

```javascript
// Exemplo: Criar um componente Angular
skill({ name: "angular-master-component" })

// Exemplo: Replicar configurações
skill({ name: "replicate-configs" })
```

---

## 📝 Convenções

### Nomenclatura

- **Interfaces**: Prefixo `I` (ex: `IUser`)
- **Enums**: Sufixo `Enum` (ex: `StatusEnum`)
- **Booleanos**: Prefixo `is`, `has`, `can`, `should`
- **Signals**: Sem `$` (diferente de Observables)
- **Arquivos**: kebab-case

### Arquitetura

- Organização por **Features** (nunca por tipo)
- Separação: Apresentação → Negócio → Infraestrutura
- Fluxo: Component → Facade → Service → Repository/API
- **NUNCA**: Component → API direto

### Angular Moderno

- Standalone Components
- `inject()` em vez de constructor
- Signals, `computed()`, `effect()`
- `@if`, `@for`, `@switch` (templates modernos)
- `takeUntilDestroyed()` para subscriptions

---

## 🛡️ Regras de Segurança

### Proteções Ativas

- ❌ **NUNCA**: `rm -rf`, `format`, `shutdown`
- ❌ **NUNCA**: Expor credenciais ou tokens
- ❌ **NUNCA**: Executar comandos destrutivos sem confirmação
- ✅ **SEMPRE**: Perguntar antes de alterações significativas
- ✅ **SEMPRE**: Usar `--force-with-lease` em vez de `--force`

### Credenciais

- NUNCA adicionar `.env` ou arquivos sensíveis
- Usar placeholders para dados fictícios
- Verificar `.gitignore` antes de commits

---

## 🤝 Contribuindo

### Fluxo

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/nova-feature`)
3. Commit suas alterações (`git commit -m 'Add nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

### Convenções de Commit

- `feat:` Nova funcionalidade
- `fix:` Correção de bug
- `docs:` Documentação
- `style:` Formatação (não afeta lógica)
- `refactor:` Refatoração de código
- `test:` Adição de testes
- `chore:` Tarefas de manutenção

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para detalhes.

---

## 👨‍💻 Autor

**Rodrigo** - [GitHub](https://github.com/Rodrigos-dev)

---

## 🙏 Agradecimentos

- Comunidade Angular
- Equipes dos LLMs (OpenCode, Gemini, Continue, Claude)
- Todos os contribuidores que ajudam a melhorar este projeto

---

<p align="center">
  Feito com ❤️ para a comunidade de desenvolvimento
</p>
---
name: git-commit-generate
description: Gera mensagens de commit seguindo convenção Conventional Commits
---

# Git Commit Generator

## Descrição

Skill para gerar mensagens de commit seguindo convenção Conventional Commits.

## Quando Usar

- Usuário pedir para gerar commit
- Usuário pedir para analisar mudanças e sugerir commit
- Após alterações de código antes de push

## Regras Críticas

- **NUNCA** executar comandos de escrita (git add, git commit, git push, git rm)
- **APENAS** executar comandos de leitura (git status, git diff, git log)
- **APENAS** gerar a mensagem para o usuário copiar e colar
- **SE** não houver arquivos para commitar, apenas avisar e aguardar

## Fluxo Obrigatório

1. **Ler regras** na pasta rules (global e/ou local) e seguir com seriedade
2. **Executar** `git status` para identificar arquivos alterados
3. **Executar** `git diff --cached` (staged) e `git diff` (unstaged)
4. **Verificar** se existem alterações
5. **Se não houver alterações**: enviar aviso "No files to commit" e parar
6. **Analisar** o tipo de alteração
7. **Gerar** mensagem de commit em inglês
8. **Apresentar** commit formatado para copiar e colar

## Detecção de Alterações

### Arquivos Staged (+ na IDE / git add)
- Verificar com `git diff --cached --name-status`

### Arquivos Unstaged (modificados mas não staged)
- Verificar com `git diff --name-status`

### Arquivos Novos (não rastreados)
- Verificar com `git status --porcelain`

## Tipos de Commit (Conventional Commits)

| Tipo | Descrição | Quando Usar |
|------|-----------|-------------|
| `feat` | Nova funcionalidade | Novo recurso, componente, rota |
| `fix` | Correção de bug | Correção de erro, comportamento inesperado |
| `chore` | Manutenção | Configuração, dependências, build |
| `refactor` | Refatoração | Reestruturar código sem mudar comportamento |
| `style` | Estilo | Formatação, whitespace, ponto e vírgula |
| `docs` | Documentação | README, comments, documentação |
| `test` | Testes | Adicionar ou corrigir testes |
| `perf` | Performance | Melhorias de performance |
| `ci` | CI/CD | Configuração de pipeline |
| `build` | Build | Sistema de build, bundler |
| `revert` | Reverter | Reverter commit anterior |

## Formato da Mensagem

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

### Regras de Formato

- **type**: obrigatório, minúsculo
- **scope**: opcional, entre parênteses, minúsculo
- **description**: obrigatório, inglês, imperativo, minúsculo, sem ponto final
- **body**: opcional, explicar o que e por quê (não como)
- **footer**: opcional, referenciar issues (ex: Closes #123)

## Exemplos

### Commits Simples
```
feat(auth): add login with Google OAuth
fix(api): handle null response from endpoint
chore(deps): update angular to v17
style(components): fix indentation in header
docs(readme): add installation instructions
```

### Commits com Body
```
feat(cart): implement quantity selector

Add +/- buttons to cart items for quantity management.
Updates inventory in real-time via WebSocket.

Closes #456
```

## Análise de Mudanças

Ao analisar o `git diff`, considerar:

1. **Arquivos alterados**: Quais arquivos mudaram?
2. **Tipo de mudança**: Feature, fix, refactor?
3. **Escopo**: Qual área do projeto? (auth, api, ui, etc.)
4. **Impacto**: Mudança grande ou pequena?
5. **Contexto**: O que o código faz agora?

## Saída

Mensagem de commit formatada em inglês para o usuário copiar e colar.

## Exemplo de Saída

```
feat(user-profile): add avatar upload functionality

- Add file input component with preview
- Implement image compression before upload
- Integrate with cloud storage API

Closes #789
```

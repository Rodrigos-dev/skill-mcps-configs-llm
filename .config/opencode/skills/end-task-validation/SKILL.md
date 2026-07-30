---
name: end-task-validation
description: Valida se todas as regras foram seguidas antes de entregar uma tarefa (replicação, segurança, convenções, economia de tokens)
---

# Skill: end-task-validation

## Quando Usar

Use esta skill **AO FINAL de cada tarefa** antes de entregar ao usuário.

## Checklist de Validação (OBRIGATÓRIO)

### 1. ✅ Replicação (SEMPRE verificar)

```
PERGUNTAR-SE:
- Criou ou alterou algum arquivo de configuração?
  → SIM: Chamar replicate-configs
  → NÃO: Pular

ARQUIVOS QUE EXIGEM REPLICAÇÃO:
- skills/*.md
- agents/*.md
- rules/*.md
- opencode.md
- memory.md
- opencode.json

DIRETÓRIOS DE DESTINO:
- C:\Users\Acer\.gemini\
- C:\Users\Acer\.continue\
- C:\Users\Acer\.claude\
- C:\Users\Acer\.openclaude\
- D:\2 - workspace\5.1 - IA estudos e em uso\6 - configs global ias local em uso\
```

### 2. ✅ Regras de Segurança

```
VERIFICAR:
- [ ] Nenhuma credencial exposta
- [ ] Nenhum token/senha em código
- [ ] Comandos destrutivos bloqueados
- [ ] Git push --force não utilizado
- [ ] Execução remota bloqueada
```

### 3. ✅ Convenções do Projeto

```
VERIFICAR:
- [ ] Nomenclatura: I para interfaces, E para enums
- [ ] Booleanos: is, has, can, should
- [ ] Arquivos: kebab-case
- [ ] Signals sem $
- [ ] Observables com $
```

### 4. ✅ Economia de Tokens

```
VERIFICAR:
- [ ] edit() usado ao invés de write() (quando <70% do arquivo)
- [ ] Não reescreveu arquivo inteiro por 1-2 linhas
- [ ] Leu apenas o necessário
- [ ] Mensagens concisas
```

### 5. ✅ Skills em Resposta

```
VERIFICAR:
- [ ] Skills em uso exibidas no topo da resposta
- [ ] Skills em uso exibidas a cada passo
```

## Formato de Validação

### ✅ Tudo OK

```
🔍 Validação Final:

✅ Replicação: [X] arquivos sincronizados
✅ Segurança: Nenhuma violação
✅ Convenções: Padronizado
✅ Tokens: Otimizado
✅ Skills: Exibidas

📦 Tarefa pronta para entrega!
```

### ⚠️ Problemas Encontrados

```
🔍 Validação Final:

⚠️ Problemas detectados:
1. [Descrição do problema]
2. [Descrição do problema]

🛠️ Ações necessárias:
1. [O que fazer]
2. [O que fazer]

❓ Corrigir antes de entregar?
```

## Fluxo de Uso

```
AO FINAL DE CADA TAREFA:

1. EXECUTAR checklist de validação
2. SE tudo OK → Entregar ao usuário
3. SE problemas → Corrigir ANTES de entregar
4. CONFIRMAR replicação se houve alteração de config
```

## Exceções (NÃO validar)

- Tarefas de leitura apenas (sem alteração)
- Consultas e perguntas (sem código)
- Adjustes em arquivos de sessão (sessions/)

## Regra de Ouro

**NUNCA entregar uma tarefa sem validar.**

Antes de apresentar resultado, pergunte-se:
"Segui TODAS as regras?"

Se a resposta for NÃO → corrija ANTES de entregar.

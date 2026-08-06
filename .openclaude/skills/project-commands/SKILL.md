# Skill: project-commands

## Descrição

Cataloga comandos de terminal que FUNCIONAM e NÃO FUNCIONAM neste ambiente (Windows PowerShell + OpenCode). Usada pelo orquestrador para evitar loops de comandos errados.

**FOCO:** Comandos que o AI executa para manipular arquivos, não apenas comandos do projeto.

**ATUALIZAR SEMPRE** que um novo comando for descoberto.

---

## ✅ Comandos que FUNCIONAM

### 📄 Leitura de Arquivos

```bash
# ✅ CORRETO: Usar tool Read (não Get-Content)
# O tool Read já formata com números de linha

# ❌ NÃO usar:
Get-Content "arquivo.ts"           # Evitar - use tool Read
type "arquivo.ts"                  # Evitar - use tool Read
cat "arquivo.ts"                   # NÃO existe no Windows
```

### 📝 Escrita de Arquivos

```bash
# ✅ CORRETO: Usar tool Write
# Sobrescreve arquivo inteiro

# ❌ NÃO usar:
Set-Content "arquivo" "conteudo"   # Perde formatação
Out-File "arquivo"                 # Perde encoding
echo "conteudo" > arquivo         # Perde formatação
```

### ✏️ Edição de Arquivos

```bash
# ✅ CORRETO: Usar tool Edit
# Substituição exata de strings

# ❌ NÃO usar:
(Get-Content "arquivo") -replace "antigo", "novo" | Set-Content "arquivo"  # Perde formatação
sed -i 's/antigo/novo/g' arquivo  # NÃO existe no PowerShell padrão
```

### 🔍 Busca em Arquivos

```bash
# ✅ CORRETO: Usar tool Grep
# Busca por regex em conteúdo

# ❌ NÃO usar:
Select-String -Path "arquivo" -Pattern "texto"  # Funciona mas Grep é melhor
findstr /s /i "texto" *.ts      # Lento, menos preciso
```

### 📁 Busca de Arquivos

```bash
# ✅ CORRETO: Usar tool Glob
# Busca por padrões (ex: **/*.ts)

# ❌ NÃO usar:
Get-ChildItem -Recurse -Filter "*.ts"  # Funciona mas Glob é mais rápido
dir /s *.ts                           # Lento, menos preciso
```

### 🖥️ Comandos Git

```bash
# ✅ CORRETOS:
git status
git diff
git diff --stat
git log --oneline -10
git add <arquivo>
git add .
git commit -m "tipo: descricao"
git push origin <branch>
git branch
git checkout <branch>

# ❌ PROIBIDOS (rules_inviolable.md):
git push --force                   # DESTRUTIVO
git push -f                        # DESTRUTIVO
```

### 📦 Comandos npm/Node

```bash
# ✅ CORRETOS:
npm run start
npm run build
npm run lint
npm run lint --fix
npm ci --legacy-peer-deps         # ⚠️ SEMPRE com --legacy-peer-deps
npm install --legacy-peer-deps    # ⚠️ SEMPRE com --legacy-peer-deps

# Testar arquivo específico (Vitest):
node "<path>/node_modules/vitest/vitest.mjs" run "<arquivo.spec.ts>"

# ❌ NÃO FUNCIONAM:
npx vitest run <arquivo>          # Falha por resolução de módulos
ng test                           # Usa Karma, não Vitest
npm ci                            # Falha por conflito de versões
```

### 📂 Operações de Diretório

```bash
# ✅ CORRETOS:
# Criar diretório
New-Item -ItemType Directory -Path "pasta/nova"

# Verificar se existe
Test-Path "pasta/arquivo"

# Deletar arquivo (com confirmação)
Remove-Item "arquivo" -Force

# Deletar diretório (com confirmação)
Remove-Item "pasta" -Recurse -Force

# Listar conteúdo
Get-ChildItem "pasta"

# ❌ PROIBIDOS:
rm -rf /                          # DESTRUTIVO
rm -rf ~                          # DESTRUTIVO
rm -rf *                          # DESTRUTIVO
rm -rf .                          # DESTRUTIVO
rd /s /q c:\                      # DESTRUTIVO (Windows)
del /f /s /q c:\                  # DESTRUTIVO (Windows)
```

---

## ❌ Comandos que NÃO FUNCIONAM

### Erros Comuns

```bash
# ❌ Usar npx vitest (falha por resolução)
npx vitest run arquivo.spec.ts
# ERRO: Cannot find module

# ❌ Usar ng test (usa Karma)
ng test
# ERRO: Karma não configurado

# ❌ Usar npm ci sem --legacy-peer-deps
npm ci
# ERRO: ERESOLVE conflito de versões

# ❌ Usar grep no Windows
grep "texto" arquivo.ts
# ERRO: comando não encontrado

# ❌ Usar cat no Windows
cat arquivo.ts
# ERRO: comando não encontrado

# ❌ Usar sed no Windows
sed -i 's/antigo/novo/g' arquivo.ts
# ERRO: comando não encontrado
```

---

## 🚨 COMANDOS PROIBIDOS

```bash
# ❌ NUNCA EXECUTAR (rules_inviolable.md):

# Sistema de arquivos
rm -rf /
rm -rf ~
rm -rf *
rm -rf .
rd /s /q c:\
del /f /s /q c:\

# Disco
dd if=
mkfs
format c:
format d:

# Sistema
shutdown
reboot
halt
poweroff

# Git
git push --force
git push -f

# Segurança
| bash
| sh
```

---

## 🔧 Padrões de Uso

### Editar arquivo (substituição específica)

```
1. Ler arquivo com tool Read
2. Localizar string exata
3. Usar tool Edit com oldString e newString
4. Verificar com tool Read
```

### Criar arquivo

```
1. Verificar se diretório existe (Test-Path)
2. Usar tool Write com conteúdo completo
3. Verificar com tool Read
```

### Deletar arquivo

```
1. Perguntar ao usuário (comando destrutivo)
2. Usar Remove-Item com -Force
3. Verificar com Test-Path
```

### Buscar em múltiplos arquivos

```
1. Usar tool Glob para encontrar arquivos
2. Usar tool Grep para buscar conteúdo
3. Ou usar bash com rg (ripgrep)
```

---

## 📋 Checklist antes de executar

- [ ] É um comando da lista "FUNCIONA"?
- [ ] Não é um comando da lista "NÃO FUNCIONA"?
- [ ] Não é um comando "PROIBIDO"?
- [ ] Path está correto (usar aspas)？
- [ ] Arquivo/pasta existe (Test-Path)?

---

## 🎯 Regra de Ouro

**SEMPRE usar as tools do sistema (Read, Write, Edit, Grep, Glob)**

**EVITAR comandos PowerShell diretamente** quando a tool existe.

Se não encontrar a tool certa:
1. Não execute comando PowerShell
2. Verifique se existe tool adequada
3. Se não existir, peça orientação

---

> Última atualização: 2026-08-06
> Ambiente: Windows PowerShell 5.1 + OpenCode

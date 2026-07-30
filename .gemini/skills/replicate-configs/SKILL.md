# Skill: replicate-configs

## Quando Usar

Use esta skill QUANDO:
- Criar uma nova skill, agent, rule ou configuração
- Alterar qualquer arquivo de configuração existente
- Solicitado explicitamente: "replicar", "sincronizar", "sync"

## Escopo de Replicação

**TODA nova configuração deve ser replicada para TODAS as LLMs:**

| Tipo de Item | Replicar para |
|--------------|---------------|
| **Skills** | `.gemini/skills/`, `.continue/skills/`, `.claude/skills/`, `.openclaude/skills/` |
| **Agents** | `.gemini/agents/`, `.continue/agents/`, `.claude/agents/`, `.openclaude/agents/` |
| **Rules** | `.gemini/.rules/`, `.continue/rules/`, `.claude/rules/`, `.openclaude/rules/` |
| **Config principal** | `GEMINI.md`, `CONTINUE.md`, `CLAUDE.md` (em cada diretório) |
| **Memória** | `memory/` ou `memorys/` em cada diretório |

## Diretórios de Destino (SEMPRE replicar para):

```
C:\Users\Acer\.gemini\
C:\Users\Acer\.continue\
C:\Users\Acer\.claude\
C:\Users\Acer\.openclaude\
C:\Users\Acer\.config\opencode\ (referência original)

D:\2 - workspace\5.1 - IA estudos e em uso\6 - configs global ias local em uso\ (BACKUP GLOBAL)
```

## Pasta de Backup Global

**ALÉM dos diretórios de configuração, SEMPRE replicar para:**

```
D:\2 - workspace\5.1 - IA estudos e em uso\6 - configs global ias local em uso\
├── .gemini\
├── .continue\
├── .claude\
├── .openclaude\
└── .config\
```

### Se a pasta não existir:
1. INFORMAR ao usuário: "Pasta de backup não encontrada: [caminho]"
2. PERGUNTAR: "Deseja criar a pasta de backup?"
3. AGUARDAR autorização antes de criar
4. SE autorizado → Criar estrutura e replicar
5. SE não autorizado → Pular replicação para backup, mas Continuar para os outros diretórios

## Fluxo de Replicação (OBRIGATÓRIO)

```
AO CRIAR ou ALTERAR qualquer config:

1. CRIAR/ALTERAR no diretório de origem (.config\opencode)
2. LISTAR todos os diretórios de destino
3. PARA CADA diretório destino:
   a. Verificar se a estrutura existe
   b. Criar se não existir
   c. Copiar arquivo com o mesmo conteúdo
   d. Ajustar caminhos específicos (se necessário)
4. CONFIRMAR replicação para todos
5. LOGAR: "Arquivo [nome] replicado para [X] diretórios"
```

## Ajustes de Caminho por LLM

Cada LLM pode ter caminhos ligeiramente diferentes:

| LLM | Caminho Rules | Caminho Skills | Caminho Memory |
|-----|---------------|----------------|----------------|
| opencode | `.config/opencode/rules/` | `.config/opencode/skills/` | `.config/opencode/memorys/` |
| gemini | `.gemini/.rules/` | `.gemini/skills/` | `.gemini/memory/` |
| continue | `.continue/rules/` | `.continue/skills/` | `.continue/memory/` |
| claude | `.claude/rules/` | `.claude/skills/` | `.claude/memory/` |
| openclaude | `.openclaude/rules/` | `.openclaude/skills/` | `.openclaude/memory/` |
| **BACKUP** | `[backup]/.config/opencode/rules/` | `[backup]/.config/opencode/skills/` | `[backup]/.config/opencode/memorys/` |

**Onde `[backup]` = `D:\2 - workspace\5.1 - IA estudos e em uso\6 - configs global ias local em uso\`**

## Exceções (NÃO replicar)

- Arquivos `.gitignore` (específicos de cada LLM)
- `node_modules/` (dependências locais)
- `sessions/` (sessões são independentes)
- `plugins/` (plugins específicos de cada LLM)

## Confirmação de Replicação

Sempre exibir ao usuário:

```
📋 Replicação Concluída:

✅ [nome-arquivo] replicado para:
  - .gemini ✓
  - .continue ✓
  - .claude ✓
  - .openclaude ✓
  - Backup global ✓

📝 Ajustes de caminho: [se houve]
```

## Regra de Ouro

**SEMPRE replique. NUNCA deixe uma LLM desatualizada.**

Antes de entregar qualquer alteração, pergunte-se:
"Todos os diretórios estão sincronizados?"

Se a resposta for NÃO → sincronize ANTES de entregar.

## Como Chamar Esta Skill

```javascript
// Para replicar uma configuração específica
skill({ name: "replicate-configs" })

// Exemplo de uso:
// 1. Criar skill: skills/nova-skill/SKILL.md
// 2. Chamar: skill({ name: "replicate-configs" })
// 3. A skill replica automaticamente para todos os diretórios
```

## Formato de Uso no Código

```
// Quando criar ou alterar qualquer config:
skill({ name: "replicate-configs" })

// A skill irá:
// 1. Detectar o que foi criado/alterado
// 2. Replicar para todos os diretórios de destino
// 3. Ajustar caminhos se necessário
// 4. Confirmar replicação ao usuário
```
---
name: technical-documentation
description: Use quando o usuário pedir para criar documentação técnica do projeto Angular seguindo o padrão HTML estabelecido.
---

# Technical Documentation Generator

## Descrição

Skill para gerar documentação técnica completa em HTML seguindo o padrão visual e estrutural do projeto.

## Quando Usar

- Criar nova documentação técnica
- Atualizar documentação existente
- Gerar documentação de novas features ou módulos
- Criar relatórios de arquitetura

## Fluxo Obrigatório

1. **Ler regras** (global e local)
2. **Ler documentação existente** em `.opencode/.docs/`
3. **Analisar estrutura atual** do projeto
4. **Identificar arquivos** (services, interfaces, enums, constants, utils, stores)
5. **Verificar mocks** de cada service
6. **Gerar HTML** seguindo o padrão estabelecido
7. **Salvar** em `.opencode/.docs/[DATA]/documentacao-tecnica.html`

---

## Estrutura do Projeto de Referência

```
.opencode/.docs/
└── [DATA]/
    └── documentacao-tecnica.html
```

---

## Padrão Visual (CSS Variables)

```css
:root {
    --primary: #00755c;
    --primary-light: #e8f5f1;
    --danger: #c5000f;
    --warning: #f59e0b;
    --success: #10b981;
    --info: #3b82f6;
    --gray-50: #f9fafb;
    --gray-100: #f3f4f6;
    --gray-200: #e5e7eb;
    --gray-300: #d1d5db;
    --gray-400: #9ca3af;
    --gray-500: #6b7280;
    --gray-600: #4b5563;
    --gray-700: #374151;
    --gray-800: #1f2937;
    --gray-900: #111827;
}
```

---

## Estrutura Obrigatória do HTML

### 1. Sidebar Fixa

```html
<aside class="sidebar">
    <div class="sidebar-header">
        <h1>[NOME DO PROJETO]</h1>
        <p>Documentação Técnica v[X.X]</p>
        <p>[DATA]</p>
    </div>
    <nav>
        <div class="section-title">Visão Geral</div>
        <a href="#overview">Projeto</a>
        <a href="#architecture">Arquitetura</a>
        <a href="#stats">Estatísticas</a>
        
        <div class="section-title">Core</div>
        <a href="#interceptors">Interceptadores (X)</a>
        <a href="#guards">Guards (X)</a>
        <a href="#pipeline">Pipeline HTTP</a>
        
        <div class="section-title">Domain</div>
        <a href="#services">Serviços (X domínios)</a>
        <a href="#stores">Stores (X)</a>
        <a href="#interfaces">Interfaces (X)</a>
        <a href="#enums">Enums (X)</a>
        <a href="#constants">Constantes (X)</a>
        <a href="#utils">Utilitários (X)</a>
        
        <div class="section-title">Features</div>
        <a href="#feature-[nome]">[Feature Name]</a>
        
        <div class="section-title">UI</div>
        <a href="#layout">Layout Base (X componentes)</a>
        <a href="#components">Componentes Shared</a>
        
        <div class="section-title">Análise</div>
        <a href="#coupling">Acoplamento</a>
        <a href="#scores">Scores</a>
        <a href="#improvements">Melhorias</a>
    </nav>
</aside>
```

### 2. Main Content

```html
<main class="main">
    <!-- HEADER -->
    <div class="header" id="overview">
        <h1>Documentação Técnica</h1>
        <p>[NOME DO PROJETO] — [FRAMEWORK] + [UI LIBRARY]</p>
        <div class="badges">
            <span class="badge badge-success">[FRAMEWORK VERSION]</span>
            <span class="badge badge-info">[UI VERSION]</span>
            <span class="badge badge-warning">[CAPACITOR/OTHER]</span>
            <span class="badge badge-success">[ARCHITECTURE]</span>
            <span class="badge badge-info">[STATE PATTERN]</span>
        </div>
    </div>

    <!-- PROJECT INFO -->
    <div class="project-info">
        <h2>Informações do Projeto</h2>
        <div class="project-grid">
            <div class="project-item">
                <div class="label">Tipo de Projeto</div>
                <div class="value">[TIPO]</div>
                <div class="sub">[DESCRIÇÃO]</div>
            </div>
            <div class="project-item">
                <div class="label">Nível do Projeto</div>
                <div class="value">[NÍVEL]</div>
                <div class="sub">[DESCRIÇÃO]</div>
            </div>
            <div class="project-item">
                <div class="label">Nota do Projeto</div>
                <div class="value">[NOTA] / 10</div>
                <div class="sub">[DESCRIÇÃO]</div>
            </div>
            <div class="project-item">
                <div class="label">Nível do Desenvolvedor</div>
                <div class="value">[NÍVEL]</div>
                <div class="sub">[DESCRIÇÃO]</div>
            </div>
        </div>
    </div>

    <!-- STATS -->
    <div class="grid" id="stats">
        <div class="stat-card">
            <div class="number">[NÚMERO]</div>
            <div class="label">[LABEL]</div>
        </div>
        <!-- Mais stat-cards -->
    </div>

    <!-- SEÇÕES SEGUINDO PADRÃO -->
    <!-- ... -->
</main>
```

---

## Seções Obrigatórias

### 1. Arquitetura

```html
<section id="architecture">
    <h2>Arquitetura</h2>
    <div class="architecture-diagram">
        <!-- Diagrama de fluxo -->
    </div>
    
    <h3>Convenções de Arquitetura</h3>
    <div class="card">
        <table>
            <tr><th>Camada</th><th>Localização</th><th>Responsabilidade</th></tr>
            <!-- Rows -->
        </table>
    </div>
    
    <h3>Convenções de Nomenclatura</h3>
    <div class="card">
        <table>
            <tr><th>Tipo</th><th>Padrão</th><th>Exemplo</th></tr>
            <!-- Rows -->
        </table>
    </div>
</section>
```

### 2. Serviços (com indicador de Mock)

```html
<section id="services">
    <h2>Serviços por Domínio</h2>
    <table>
        <tr>
            <th>Domínio</th>
            <th>Interface/Token</th>
            <th>Implementação</th>
            <th>Mock</th>
            <th>Mock Flag</th>
            <th>Status</th>
        </tr>
        <tr>
            <td><strong>[Domínio]</strong></td>
            <td><code>I[Domain]Service</code> / <code>[DOMAIN]_SERVICE</code></td>
            <td>[domain].service.ts</td>
            <td>[domain].mock.service.ts</td>
            <td>USE_[DOMAIN]_CONFIG_MOCK = <strong>[true/false]</strong></td>
            <td><span class="mock-badge mock-yes">Com Mock</span></td>
            <!-- OU -->
            <td><span class="mock-badge mock-no">Sem Mock</span></td>
        </tr>
    </table>
</section>
```

### 3. Interfaces (com indicador de Mock)

```html
<section id="interfaces">
    <h2>Interfaces</h2>
    <table>
        <tr><th>Arquivo</th><th>Interfaces Principais</th><th>Descrição</th><th>Mock</th></tr>
        <tr>
            <td><code>[domain]/[domain].interface.ts</code></td>
            <td>I[Interface1], I[Interface2]</td>
            <td>[Descrição]</td>
            <td><span class="mock-badge mock-no">Dados reais</span></td>
        </tr>
    </table>
</section>
```

### 4. Enums

```html
<section id="enums">
    <h2>Enums</h2>
    <table>
        <tr><th>Arquivo</th><th>Enum</th><th>Valores</th><th>Mock</th></tr>
        <tr>
            <td><code>[domain]/[domain].enum.ts</code></td>
            <td>[DomainEnum]</td>
            <td>VALUE1, VALUE2, VALUE3</td>
            <td><span class="mock-badge mock-no">N/A</span></td>
        </tr>
    </table>
</section>
```

### 5. Constantes

```html
<section id="constants">
    <h2>Constantes</h2>
    <table>
        <tr><th>Arquivo</th><th>Constante</th><th>Descrição</th><th>Mock</th></tr>
        <tr>
            <td><code>[domain]/[domain].constants.ts</code></td>
            <td>[CONSTANT_NAME]</td>
            <td>[Descrição]</td>
            <td><span class="mock-badge mock-no">N/A</span></td>
            <!-- OU -->
            <td><span class="mock-badge mock-yes">Mock Data</span></td>
        </tr>
    </table>
</section>
```

### 6. Utilitários

```html
<section id="utils">
    <h2>Utilitários</h2>
    <table>
        <tr><th>Arquivo</th><th>Função/Interface</th><th>Descrição</th><th>Mock</th></tr>
        <tr>
            <td><code>[domain]/[util].ts</code></td>
            <td>[functionName]()</td>
            <td>[Descrição]</td>
            <td><span class="mock-badge mock-no">Sem Mock</span></td>
        </tr>
    </table>
</section>
```

### 7. Features (com indicador de Mock)

```html
<section id="feature-[nome]">
    <h2>Feature: [Nome]</h2>
    <div class="card">
        <div class="card-header">
            <span class="card-title">[PageName]</span>
            <span class="card-path">features/[feature]/pages/[page]/</span>
        </div>
        <p>[Descrição da página]</p>
        <div class="card-tags">
            <span class="tag tag-decoupled">Desacoplado</span>
            <span class="tag" style="background:#d1fae5;color:#065f46">[Tag]</span>
            <span class="mock-badge mock-yes">[ServiceName] Mock</span>
            <!-- OU -->
            <span class="mock-badge mock-no">Sem Mock</span>
        </div>
    </div>
</section>
```

### 8. Layout (com indicador de Mock)

```html
<section id="layout">
    <h2>Sistema de Layout Base</h2>
    <table>
        <tr><th>Componente</th><th>Responsabilidade</th><th>Acoplamento</th><th>Mock</th></tr>
        <tr>
            <td><strong>[ComponentName]</strong></td>
            <td>[Descrição]</td>
            <td><span class="tag tag-decoupled">Desacoplado</span></td>
            <td><span class="mock-badge mock-no">Sem Mock</span></td>
        </tr>
    </table>
</section>
```

### 9. Scores

```html
<section id="scores">
    <h2>Scores de Qualidade</h2>
    <div class="score-bar">
        <span class="label">[Métrica]</span>
        <div class="bar"><div class="fill" style="width: [XX]%; background: var(--success/info/warning);"></div></div>
        <span class="label">[X.X]</span>
    </div>
    
    <div style="margin-top: 24px; padding: 16px; background: var(--primary-light); border-radius: 8px; text-align: center;">
        <strong style="font-size: 24px; color: var(--primary);">Score Geral: [X.X] / 10</strong>
        <p style="color: var(--gray-600); margin-top: 4px;">[Descrição]</p>
    </div>
</section>
```

---

## Tags de Mock

### Badge Mock (para services)

```html
<span class="mock-badge mock-yes">Com Mock</span>
<span class="mock-badge mock-no">Sem Mock</span>
<span class="mock-badge mock-global">Mock Global</span>
```

### Badge Mock (para constantes)

```html
<span class="mock-badge mock-yes">Mock Data</span>
<span class="mock-badge mock-no">N/A</span>
```

### Badge Mock (para interfaces)

```html
<span class="mock-badge mock-no">Dados reais</span>
```

---

## Classes CSS Obrigatórias

### Layout

```css
.sidebar { /* Sidebar fixa */ }
.sidebar-header { /* Cabeçalho sidebar */ }
.main { /* Conteúdo principal */ }
.header { /* Cabeçalho */ }
.project-info { /* Info do projeto */ }
.project-grid { /* Grid de info */ }
.project-item { /* Item de info */ }
```

### Cards

```css
.card { /* Card genérico */ }
.card-header { /* Cabeçalho card */ }
.card-title { /* Título card */ }
.card-path { /* Caminho do arquivo */ }
.card-tags { /* Tags do card */ }
```

### Tags

```css
.tag { /* Tag genérica */ }
.tag-coupled { /* Vermelho */ }
.tag-decoupled { /* Verde */ }
.tag-partial { /* Amarelo */ }
.tag-mock { /* Roxo */ }
.tag-no-mock { /* Cinza */ }
```

### Mock Badges

```css
.mock-badge { /* Badge genérico */ }
.mock-yes { /* Verde */ }
.mock-no { /* Cinza */ }
.mock-global { /* Amarelo */ }
```

### Tabelas

```css
table { /* Tabela */ }
th { /* Cabeçalho */ }
td { /* Célula */ }
tr:hover { /* Hover */ }
```

### Stats

```css
.stat-card { /* Card de estatística */ }
.stat-card .number { /* Número */ }
.stat-card .label { /* Label */ }
```

### Scores

```css
.score-bar { /* Barra de score */ }
.score-bar .bar { /* Barra de fundo */ }
.score-bar .fill { /* Preenchimento */ }
.score-bar .label { /* Label */ }
```

---

## Checklist de Validação

### Estrutura

- [ ] Sidebar fixa com navegação
- [ ] Header com badges
- [ ] Project Info com 4 itens
- [ ] Stats com cards
- [ ] Seções na ordem correta
- [ ] Footer com data

### Conteúdo

- [ ] Arquitetura documentada
- [ ] Convenções de nomenclatura
- [ ] Serviços com indicador de mock
- [ ] Interfaces documentadas
- [ ] Enums documentados
- [ ] Constantes documentadas
- [ ] Utilitários documentados
- [ ] Features documentadas
- [ ] Layout documentado
- [ ] Scores calculados
- [ ] Melhorias listadas

### Visual

- [ ] CSS Variables definidas
- [ ] Responsivo (sidebar esconde em mobile)
- [ ] Cores consistentes
- [ ] Tipografia legível
- [ ] Espaçamento adequado

### Mock Indicators

- [ ] Cada service tem indicador de mock
- [ ] Cada constante tem indicador (se aplicável)
- [ ] Cada feature tem indicador de mock
- [ ] Cada componente de layout tem indicador

---

## Saída Esperada

1 arquivo HTML seguindo o padrão:

- `documentacao-tecnica.html`

---

## Exemplo de Uso

**Usuário:** "Crie documentação técnica para o projeto"

**Agente:**
1. Lê documentação existente
2. Analisa estrutura do projeto
3. Identifica services e mocks
4. Gera HTML seguindo padrão
5. Salva em `.opencode/.docs/[DATA]/documentacao-tecnica.html`

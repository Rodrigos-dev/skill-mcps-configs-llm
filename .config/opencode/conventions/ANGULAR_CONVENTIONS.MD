# ANGULAR_CONVENTIONS.MD

# Convenções Angular do Projeto

Versão: 1.0

Este documento define os padrões obrigatórios para todos os agentes responsáveis pela implementação, manutenção e revisão do projeto Angular.

Estas regras possuem prioridade sobre decisões individuais dos agentes.

Os agentes devem seguir exatamente a ordem de decisão definida abaixo.

Sempre respeitar o arquivo de regras na pasta rules(local , e ou global), antes de iniciar qualquer
ação rever as regras para sempre respeitar as regras mais atuais

---

# 1. Ordem de Decisão (OBRIGATÓRIA)

Antes de escrever qualquer linha de código siga exatamente esta sequência.

# Regra de Evolução

Ao modificar um código existente:

- Não alterar estilo arquitetural.
- Não renomear arquivos sem necessidade.
- Não mover arquivos apenas por preferência.
- Não modernizar apenas parte de uma Feature.
- Toda melhoria deve manter a consistência com o restante do projeto.

## 1º Passo

Analisar completamente o projeto.

Identificar:

- Estrutura de pastas
- Arquitetura
- Convenções de nomenclatura
- Organização das Features
- Estratégia de Estado
- Estrutura HTML
- Organização SCSS
- Componentes reutilizáveis
- Serviços existentes
- Facades existentes
- Padrões de DI
- Estratégia de Testes

Nunca assumir arquitetura sem analisar o projeto.

---

## 2º Passo

Caso exista um padrão consolidado, seguir exatamente o padrão encontrado.

Nunca criar uma arquitetura paralela.

Nunca misturar padrões.

Nunca modernizar apenas parte do projeto.

A consistência é mais importante que preferências pessoais.

---

## 3º Passo

Caso o projeto NÃO possua um padrão definido, utilizar rigorosamente todas as regras deste documento.

---

## 4º Passo

Caso exista conflito entre este documento e o projeto existente:

O projeto existente SEMPRE possui prioridade.

---

# 2. Objetivos

Todo código produzido deve ser:

- Legível
- Escalável
- Testável
- Coeso
- Baixo acoplamento
- Fácil manutenção
- Performance elevada
- Consistente

Todo código deve parecer escrito por uma única equipe.

---

# 3. Filosofia

Sempre priorizar:

Clareza > Complexidade

Legibilidade > Inteligência

Consistência > Preferência

Arquitetura > Velocidade

Qualidade > Quantidade

---

# 4. Arquitetura

Sempre utilizar princípios de:

- DDD
- Clean Architecture
- Clean Code
- SOLID
- Feature First
- Separation of Concerns
- Single Responsibility
- Dependency Inversion
- Composition over Inheritance

---

# 5. DDD

Sempre pensar em domínio.

Nunca pensar primeiro em telas.

As Features representam capacidades do sistema.

Exemplo:

Errado

ClientesPage

ProdutosPage

PedidosPage

Correto

Customer

Product

Order

Authentication

Checkout

Delivery

Payment

---

# 6. Organização

Sempre organizar por Feature.

Nunca por tipo de arquivo.

Errado

components/

pages/

services/

models/

Correto

features/

authentication/

customers/

orders/

products/

shared/

core/

---

# 7. Responsabilidades

Cada classe deve possuir apenas uma responsabilidade.

Cada componente deve possuir apenas uma responsabilidade.

Cada Service deve possuir apenas uma responsabilidade.

Cada Facade deve possuir apenas uma responsabilidade.

---

# 8. Componentes

Sempre separar:

Apresentação

Negócio

Infraestrutura

Nunca misturar.

---

# 9. Smart Components

Responsáveis por:

- comunicação
- estado
- navegação
- chamadas para Facades

Nunca conter HTML complexo.

---

# 10. Dumb Components

Responsáveis apenas por:

- renderização
- eventos
- inputs
- outputs

Nunca acessar APIs.

Nunca acessar Services.

Nunca conhecer regras de negócio.

---

# 11. Services

Services possuem responsabilidade de comunicação.

Nunca controlar interface.

Nunca possuir HTML.

Nunca controlar navegação.

---

# 12. Facades

Toda regra de negócio deve preferencialmente passar por uma Facade.

Componentes não devem conhecer APIs diretamente.

Fluxo ideal:

Component

↓

Facade

↓

Service

↓

Repository/API

---

# 13. Estado

Preferência:

Signals

↓

Computed

↓

Effect

↓

Observable

↓

BehaviorSubject

Observable deve ser utilizado apenas quando realmente necessário.

---

# 14. Reutilização

Antes de criar qualquer componente verificar:

Já existe?

Pode ser reutilizado?

Pode ser estendido?

Evitar duplicação.

Perguntar se deve criar um novo na feature ou usar o ja existente nunca acoplar as features

---

# 15. DRY

Nunca repetir código.

Caso exista repetição:

Extrair.

Nunca acoplar as features

Codigo já existente deve er perguntado se vamos extrair ou criar mesmo dupolicando na outra feature

---

# 16. KISS

Sempre escolher a solução mais simples.

Nunca criar arquitetura complexa sem necessidade.

---

# 17. YAGNI

Nunca implementar funcionalidades futuras.

Implementar apenas o necessário.

---

# 18. SOLID

Todos os princípios devem ser respeitados.

S

Uma responsabilidade.

O

Aberto para extensão.

Fechado para modificação.

L

Substituição.

I

Interfaces pequenas.

D

Inversão de dependências.

---

# 19. Clean Code

Sempre:

Nomes claros.

Métodos pequenos.

Classes pequenas.

Responsabilidades claras.

Poucos níveis de indentação.

Poucos parâmetros.

---

# 20. Complexidade

Evitar:

if aninhado

switch gigante

ternários aninhados

loops complexos

Sempre preferir:

early return

extração de métodos

extração de componentes

extração de funções

---

# 21. Legibilidade

O código deve ser compreendido sem comentários.

Comentários apenas quando agregarem contexto.

Nunca comentar código óbvio.

Emojis são proibidos

---

# 22. Performance

Performance deve fazer parte da arquitetura.

Nunca ser adicionada posteriormente.

---

# 23. Escalabilidade

Toda implementação deve suportar crescimento.

Evitar soluções temporárias.

---

# 24. Dependências

Adicionar bibliotecas apenas quando realmente necessárias.

Sempre preferir recursos nativos do Angular.

---

# 25. Atualizações

Sempre utilizar a abordagem mais moderna suportada pela versão do projeto.

Nunca introduzir APIs depreciadas.

---

# 26. Revisão

Antes de concluir qualquer tarefa validar:

Arquitetura

DDD

SOLID

Clean Code

Responsabilidades

Performance

Legibilidade

Manutenção

Consistência

---

# ANGULAR_CONVENTIONS.MD

# Convenções Angular do Projeto

Versão: 1.0

Este documento define os padrões obrigatórios para todos os agentes responsáveis pela implementação, manutenção e revisão do projeto Angular.

Estas regras possuem prioridade sobre decisões individuais dos agentes.

Os agentes devem seguir exatamente a ordem de decisão definida abaixo.

---

# 1. Ordem de Decisão (OBRIGATÓRIA)

Antes de escrever qualquer linha de código siga exatamente esta sequência.

## 1º Passo

Analisar completamente o projeto.

Identificar:

- Estrutura de pastas
- Arquitetura
- Convenções de nomenclatura
- Organização das Features
- Estratégia de Estado
- Estrutura HTML
- Organização SCSS
- Componentes reutilizáveis
- Serviços existentes
- Facades existentes
- Padrões de DI
- Estratégia de Testes

Nunca assumir arquitetura sem analisar o projeto.

---

## 2º Passo

Caso exista um padrão consolidado, seguir exatamente o padrão encontrado.

Nunca criar uma arquitetura paralela.

Nunca misturar padrões.

Nunca modernizar apenas parte do projeto.

A consistência é mais importante que preferências pessoais.

---

## 3º Passo

Caso o projeto NÃO possua um padrão definido, utilizar rigorosamente todas as regras deste documento.

---

## 4º Passo

Caso exista conflito entre este documento e o projeto existente:

O projeto existente SEMPRE possui prioridade.

---

# 2. Objetivos

Todo código produzido deve ser:

- Legível
- Escalável
- Testável
- Coeso
- Baixo acoplamento
- Fácil manutenção
- Performance elevada
- Consistente

Todo código deve parecer escrito por uma única equipe.

---

# 3. Filosofia

Sempre priorizar:

Clareza > Complexidade

Legibilidade > Inteligência

Consistência > Preferência

Arquitetura > Velocidade

Qualidade > Quantidade

---

# 4. Arquitetura

Sempre utilizar princípios de:

- DDD
- Clean Architecture
- Clean Code
- SOLID
- Feature First
- Separation of Concerns
- Single Responsibility
- Dependency Inversion
- Composition over Inheritance

---

# 5. DDD

Sempre pensar em domínio.

Nunca pensar primeiro em telas.

As Features representam capacidades do sistema.

Exemplo:

Errado

ClientesPage

ProdutosPage

PedidosPage

Correto

Customer

Product

Order

Authentication

Checkout

Delivery

Payment

---

# 6. Organização

Sempre organizar por Feature.

Nunca por tipo de arquivo.

Errado

components/

pages/

services/

models/

Correto

features/

authentication/

customers/

orders/

products/

shared/

core/

---

# 7. Responsabilidades

Cada classe deve possuir apenas uma responsabilidade.

Cada componente deve possuir apenas uma responsabilidade.

Cada Service deve possuir apenas uma responsabilidade.

Cada Facade deve possuir apenas uma responsabilidade.

---

# 8. Componentes

Sempre separar:

Apresentação

Negócio

Infraestrutura

Nunca misturar.

---

# 9. Smart Components

Responsáveis por:

- comunicação
- estado
- navegação
- chamadas para Facades

Nunca conter HTML complexo.

---

# 10. Dumb Components

Responsáveis apenas por:

- renderização
- eventos
- inputs
- outputs

Nunca acessar APIs.

Nunca acessar Services.

Nunca conhecer regras de negócio.

---

# 11. Services

Services possuem responsabilidade de comunicação.

Nunca controlar interface.

Nunca possuir HTML.

Nunca controlar navegação.

---

# 12. Facades

Toda regra de negócio deve preferencialmente passar por uma Facade.

Componentes não devem conhecer APIs diretamente.

Fluxo ideal:

Component

↓

Facade

↓

Service

↓

Repository/API

---

# 13. Estado

Preferência:

Signals

↓

Computed

↓

Effect

↓

Observable

↓

BehaviorSubject

Observable deve ser utilizado apenas quando realmente necessário.

---

# 14. Reutilização

Antes de criar qualquer componente verificar:

Já existe?

Pode ser reutilizado?

Pode ser estendido?

Evitar duplicação.

---

# 15. DRY

Nunca repetir código.

Caso exista repetição:

Extrair.

---

# 16. KISS

Sempre escolher a solução mais simples.

Nunca criar arquitetura complexa sem necessidade.

---

# 17. YAGNI

Nunca implementar funcionalidades futuras.

Implementar apenas o necessário.

---

# 18. SOLID

Todos os princípios devem ser respeitados.

S

Uma responsabilidade.

O

Aberto para extensão.

Fechado para modificação.

L

Substituição.

I

Interfaces pequenas.

D

Inversão de dependências.

---

# 19. Clean Code

Sempre:

Nomes claros.

Métodos pequenos.

Classes pequenas.

Responsabilidades claras.

Poucos níveis de indentação.

Poucos parâmetros.

---

# 20. Complexidade

Evitar:

if aninhado

switch gigante

ternários aninhados

loops complexos

Sempre preferir:

early return

extração de métodos

extração de componentes

extração de funções

---

# 21. Legibilidade

O código deve ser compreendido sem comentários.

Comentários apenas quando agregarem contexto.

Nunca comentar código óbvio.

---

# 22. Performance

Performance deve fazer parte da arquitetura.

Nunca ser adicionada posteriormente.

---

# 23. Escalabilidade

Toda implementação deve suportar crescimento.

Evitar soluções temporárias.

---

# 24. Dependências

Adicionar bibliotecas apenas quando realmente necessárias.

Sempre preferir recursos nativos do Angular.

---

# 25. Atualizações

Sempre utilizar a abordagem mais moderna suportada pela versão do projeto.

Nunca introduzir APIs depreciadas.

---

# 26. Revisão

Antes de concluir qualquer tarefa validar:

Arquitetura

DDD

SOLID

Clean Code

Responsabilidades

Performance

Legibilidade

Manutenção

Consistência

---

---

# 81. HTML

Todo HTML deve ser:

- Semântico
- Acessível
- Legível
- Responsivo
- Reutilizável

Evitar HTML apenas visual.

Sempre representar corretamente o significado do conteúdo.

---

# 82. HTML Semântico

Sempre preferir elementos semânticos.

Utilizar:

header

main

section

article

aside

footer

nav

figure

figcaption

form

fieldset

legend

address

time

dialog

details

summary

---

# 83. Divs

Não utilizar div por padrão.

Antes de criar uma div perguntar:

Existe um elemento semântico melhor?

Utilizar div apenas quando não existir alternativa adequada.

---

# 84. Estrutura Base

Toda página deve preferencialmente seguir:

header

main

section

footer

---

# 85. Títulos

Sempre respeitar hierarquia.

Exemplo:

h1

h2

h3

h4

Nunca pular níveis sem necessidade.

---

# 86. Formulários

Sempre utilizar:

form

label

fieldset

legend

button

Nunca depender apenas de placeholders.

---

# 87. Labels

Todo campo deve possuir label.

Mesmo quando visualmente oculto.

---

Formularios

Caso exista lib de formulario instalado ou indicada a usar usar a Lib disponivel nunca usando outra forma

caso exista o MD da lib ler o MD dela caso nao exista ver documentacao local, e ou seguir o padrao de uso dela no projeto

---

# 88. Botões

Sempre utilizar:

button

Nunca utilizar:

div clicável

span clicável

p clicável

---

# 89. Links

Sempre utilizar:

a

quando houver navegação.

Nunca utilizar button para navegar.

---

# 90. Imagens

Toda imagem deve possuir:

alt

Exemplo:

alt="Foto do produto"

Nunca:

alt="imagem"

alt="foto"

---

# 91. SVG

Preferir SVG para ícones.

Evitar imagens PNG para ícones simples.

---

# 92. Tabelas

Utilizar table apenas para dados tabulares.

Nunca utilizar table para layout.

---

# 93. Acessibilidade

Todo desenvolvimento deve considerar acessibilidade desde o início.

Nunca tratar acessibilidade como etapa final.

---

# 94. ARIA

Utilizar:

aria-label

aria-labelledby

aria-describedby

aria-hidden

role

quando necessário.

Nunca adicionar ARIA sem necessidade.

---

# 95. Navegação por Teclado

Toda interface deve ser utilizável apenas com teclado.

---

# 96. Focus

Todo elemento interativo deve possuir foco visível.

Nunca remover outline sem substituir adequadamente.

---

# 97. Contraste

Sempre respeitar níveis mínimos de contraste.

---

# 98. Leitores de Tela

Sempre considerar screen readers.

Todo fluxo importante deve ser navegável.

---

# 99. Angular Templates

Templates devem ser simples.

Evitar lógica complexa.

---

# 100. Lógica no Template

Evitar:

condições complexas

cálculos

transformações

funções

---

# 101. Métodos no HTML

Nunca fazer:

getTotal()

getUsers()

calculatePrice()

diretamente no template.

---

# 102. Preferência

Utilizar:

Signal

Computed

Readonly Properties

ViewModel

---

# 103. Controle de Fluxo

Sempre utilizar:

@if

@for

@switch

quando suportado pela versão do projeto.

---

# 104. Track

Sempre utilizar track em loops.

Exemplo:

@for(item of items(); track item.id)

---

# 105. Renderização

Evitar renderizações desnecessárias.

---

# 106. ViewModel

Preferir ViewModels preparados no TypeScript.

Evitar lógica espalhada no HTML.

---

# 107. CSS

Todo CSS deve ser:

Simples

Legível

Responsivo

Escalável

---

# 108. SCSS

Utilizar SCSS de forma simples.

Não transformar SCSS em linguagem de programação.

---

# 109. Organização do SCSS

Ordem recomendada:

Host

Container

Layout

Componentes

Estados

Media Queries

---

# 110. Nesting

Utilizar nesting com moderação.

Máximo recomendado:

3 níveis.

---

# 111. Profundidade

Evitar:

.container {
.wrapper {
.content {
.card {
.title {
}
}
}
}
}

---

# 112. Seletores

Preferir seletores simples.

Evitar seletores extremamente específicos.

---

# 113. IDs

Evitar utilização de IDs para estilização.

---

# 114. !important

Proibido.

Utilizar apenas em casos excepcionais.

---

# 115. Inline Style

Evitar.

Sempre utilizar SCSS.

---

# 116. Mobile First

Todo layout deve ser desenvolvido Mobile First.

---

# 116.1 Responseividade

Sempre responsivo, para mobile , tablet , desktop, wide

---

# 117. Breakpoints

Estrutura recomendada:

Mobile

Tablet

Desktop

Wide

---

# 118. Unidades

Preferir:

rem

em

%

vw

vh

clamp()

---

# 119. Evitar

px excessivos.

---

# 120. Espaçamento

Utilizar escalas consistentes.

Exemplo:

4

8

12

16

24

32

40

48

64

---

# 121. Layout

Preferir:

Flexbox

Grid

---

# 122. Flexbox

Utilizar para layouts unidimensionais.

---

# 123. Grid

Utilizar para layouts bidimensionais.

---

# 124. Gap

Sempre preferir gap.

Evitar margin para espaçamentos internos.

---

# 125. Position

Evitar:

position absolute

position fixed

sem necessidade.

---

# 126. Overflow

Controlar conscientemente.

Nunca esconder problemas com:

overflow: hidden

---

# 127. Responsividade

Não criar versões separadas.

Criar layouts adaptáveis.

---

# 128. Imagens Responsivas

Utilizar:

max-width: 100%

height: auto

---

# 129. Aspect Ratio

Preferir:

aspect-ratio

ao invés de hacks antigos.

---

# 130. Cores

Preferir variáveis.

Nunca espalhar cores hardcoded.

---

# 131. Variáveis

Utilizar:

CSS Variables

como primeira escolha.

---

# 132. Temas

Preparar componentes para suportar temas.

---

# 133. Animações

Utilizar apenas quando agregarem valor.

---

# 134. Transições

Preferir:

transform

opacity

---

# 135. Evitar

animar:

width

height

top

left

---

# 136. Performance CSS

Evitar:

seletores complexos

reflows desnecessários

animações pesadas

---

# 137. Skeleton Loading

Preferir skeletons ao invés de spinners em carregamentos longos.

---

# 138. Estados da Interface

Todo componente deve prever:

loading

success

empty

error

---

# 139. UX

Sempre informar:

carregamento

erro

sucesso

processamento

---

# 140. Feedback

Nunca deixar usuário sem feedback.

---

# 141. Empty States

Toda listagem deve prever estado vazio.

---

# 142. Error States

Toda operação deve prever falhas.

---

# 143. Loading States

Toda operação assíncrona deve prever carregamento.

---

# 144. Componentização

Se um bloco visual se repetir:

Extrair componente.

---

# 145. Reutilização

Priorizar componentes reutilizáveis.

Evitar duplicação de HTML.

---

# 146. Consistência Visual

Todos os componentes devem seguir o Design System do projeto.

Caso não exista:

Criar padrões consistentes.

---

# 147. Design System

Sempre reutilizar:

cores

tipografia

espaçamentos

componentes

tokens

---

# 148. Performance Frontend

Reduzir:

re-renderizações

DOM desnecessário

watchers

subscriptions

---

# 149. Angular Signals + UI

Sempre preferir Signals para atualização de interface.

---

# 150. Regra Final

HTML deve ser:

Semântico.

Acessível.

Responsivo.

Legível.

CSS deve ser:

Simples.

Escalável.

Mobile First.

Angular Templates devem ser:

Declarativos.

Limpos.

Sem lógica de negócio.

---

# 151. Testabilidade

Todo código deve ser desenvolvido pensando em testes.

Evitar dependências ocultas.

Evitar acoplamento.

Sempre favorecer injeção de dependências.

Nunca criar código impossível de testar.

---

# 152. Testes

Sempre que solicitado gerar testes consistentes.

Priorizar:

- comportamento
- regras de negócio
- fluxos críticos

Evitar testes frágeis.

---

# 153. Mock

Sempre utilizar mocks simples.

Nunca duplicar mocks.

Sempre reutilizar.

---

# 154. Separação

Testes nunca devem alterar código de produção.

---

# 155. Code Review

Todo código deve passar pelas seguintes verificações.

---

# Arquitetura

✔ segue o padrão do projeto

✔ respeita o ANGULAR_CONVENTIONS.MD

✔ respeita DDD

✔ respeita SOLID

✔ respeita Clean Architecture

✔ respeita Feature First

✔ respeita Separation of Concerns

---

# Angular

✔ Standalone quando suportado

✔ inject()

✔ Signals

✔ computed()

✔ effect()

✔ takeUntilDestroyed()

✔ Async Pipe

✔ Lazy Loading

✔ Functional APIs

---

# Estado

✔ Signal quando possível

✔ Observable apenas quando necessário

✔ Sem subscribe desnecessário

✔ Sem BehaviorSubject sem necessidade

---

# Componentes

✔ Responsabilidade única

✔ Sem regra de negócio

✔ Sem chamadas HTTP

✔ Inputs pequenos

✔ Outputs claros

✔ Componentes reutilizáveis

---

# Facades

✔ Centralizam regras

✔ Componentes desacoplados

✔ Services desacoplados

---

# Services

✔ Comunicação

✔ Regras específicas

✔ Sem manipular interface

---

# TypeScript

✔ Sem any

✔ Tipagem correta

✔ Readonly

✔ Interfaces

✔ Enums

✔ Generics

✔ Null Safety

---

# Nomeação

✔ Interfaces iniciam com I

Exemplo

IUser

ILogin

IAddress

✔ Enums iniciam com E

Exemplo

EStatus

ERole

EPermission

✔ Booleanos

isLoading

hasPermission

canEdit

shouldReload

✔ Observables

users$

✔ Signals

users

✔ Collections

Sempre plural

---

# HTML

✔ HTML semântico

✔ Acessibilidade

✔ Labels

✔ Alt

✔ Button

✔ Main

✔ Header

✔ Footer

✔ Nav

✔ Section

✔ Article

✔ Figure

✔ Form

✔ Fieldset

✔ Legend

✔ Sem div desnecessária

---

# CSS

✔ Mobile First

✔ Flex

✔ Grid

✔ Gap

✔ Clamp

✔ Variáveis CSS

✔ Sem !important

✔ Sem Float

✔ Sem Margin Hack

✔ Sem Position Absolute desnecessário

✔ Responsividade limpa

---

# Performance

✔ Sem funções no template

✔ Sem subscribe dentro de subscribe

✔ Sem ChangeDetectorRef desnecessário

✔ Sem DetectChanges

✔ Sem Loops desnecessários

✔ Computed quando possível

✔ Track obrigatório em @for

---

# Clean Code

✔ Métodos pequenos

✔ Classes pequenas

✔ Poucos parâmetros

✔ Poucos níveis de indentação

✔ Código legível

✔ Código consistente

---

# Anti Patterns

Nunca fazer

Component → HttpClient

Component → API

Component → Repository

Component gigante

Service gigante

Facade gigante

Switch gigante

If gigante

Subscribe dentro de Subscribe

Any

Duplicação

Código morto

Comentários desnecessários

Funções enormes

Arquivos enormes

Lógica no Template

CSS duplicado

HTML não semântico

Mixins gigantes

SCSS complexo

Arquitetura paralela

---

# Refatoração

Sempre procurar

Duplicação

Complexidade

Acoplamento

Baixa coesão

Métodos grandes

Classes grandes

Componentes grandes

Services grandes

Facade grande

HTML repetido

SCSS repetido

---

# Antes de finalizar qualquer tarefa

Responder mentalmente

O código segue o padrão existente do projeto?

Caso não exista padrão:

Segue exatamente o ANGULAR_CONVENTIONS.MD?

Existe duplicação?

Existe forma mais simples?

Existe forma mais legível?

Existe forma mais performática?

Existe risco de manutenção?

Existe risco de acoplamento?

Existe risco de Memory Leak?

Existe risco de regressão?

Todos os nomes seguem as convenções?

HTML é semântico?

CSS é responsivo?

Acessibilidade foi considerada?

Signals foram utilizados quando possível?

---

# Fluxo obrigatório de decisão

Sempre seguir exatamente esta sequência.

1.

Analisar completamente o projeto.

↓

2.

Existe padrão?

SIM

↓

Seguir exatamente o padrão encontrado.

NÃO

↓

Aplicar integralmente este documento.

↓

3.

Planejar a solução.

↓

4.

Implementar.

↓

5.

Revisar.

↓

6.

Refatorar.

↓

7.

Validar.

↓

8.

Entregar.

---

# Princípio Fundamental

Consistência possui prioridade sobre preferência.

O projeto existente possui prioridade sobre qualquer convenção.

Na ausência de um padrão definido, este documento torna-se a única fonte de verdade para decisões arquiteturais, organização do código, nomenclatura, HTML, CSS, SCSS, TypeScript e Angular.

Todos os agentes devem seguir rigorosamente estas convenções antes de gerar qualquer implementação, refatoração ou revisão de código.

---

Precisa de estado local?
↓
Signal

Precisa derivar estado?
↓
Computed

Precisa efeito colateral?
↓
Effect

Precisa stream contínua?
↓
Observable

Precisa componente reutilizável?
↓
Shared

Possui regra de negócio?
↓
Facade

Possui comunicação externa?
↓
Service

Possui apenas apresentação?
↓
Component

Existe padrão no projeto?
↓
Seguir projeto

Não existe?
↓
Seguir ANGULAR_CONVENTIONS.MD

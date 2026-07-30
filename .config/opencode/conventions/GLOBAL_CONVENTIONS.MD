# GLOBAL_CONVENTIONS.MD

# Convenções Globais do Projeto

Versão: 1.0

Este documento define os padrões obrigatórios para todos os agentes responsáveis pela implementação, manutenção e revisão do projeto.

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
- Componentes reutilizáveis
- Serviços existentes
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

# 8. Reutilização

Antes de criar qualquer componente verificar:

Já existe?

Pode ser reutilizado?

Pode ser estendido?

Evitar duplicação.

Perguntar se deve criar um novo na feature ou usar o ja existente nunca acoplar as features

---

# 9. DRY

Nunca repetir código.

Caso exista repetição:

Extrair.

Nunca acoplar as features

Codigo já existente deve er perguntado se vamos extrair ou criar mesmo dupolicando na outra feature

---

# 10. KISS

Sempre escolher a solução mais simples.

Nunca criar arquitetura complexa sem necessidade.

---

# 11. YAGNI

Nunca implementar funcionalidades futuras.

Implementar apenas o necessário.

---

# 12. SOLID

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

# 13. Clean Code

Sempre:

Nomes claros.

Métodos pequenos.

Classes pequenas.

Responsabilidades claras.

Poucos níveis de indentação.

Poucos parâmetros.

---

# 14. Complexidade

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

# 15. Legibilidade

O código deve ser compreendido sem comentários.

Comentários apenas quando agregarem contexto.

Nunca comentar código óbvio.

Emojis são proibidos

---

# 16. Performance

Performance deve fazer parte da arquitetura.

Nunca ser adicionada posteriormente.

---

# 17. Escalabilidade

Toda implementação deve suportar crescimento.

Evitar soluções temporárias.

---

# 18. Dependências

Adicionar bibliotecas apenas quando realmente necessárias.

---

# 19. Atualizações

Sempre utilizar a abordagem mais moderna suportada pela versão do projeto.

Nunca introduzir APIs depreciadas.

---

# 20. Revisão

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

# 21. Regra de Evolução

Ao modificar um código existente:

- Não alterar estilo arquitetural.
- Não renomear arquivos sem necessidade.
- Não mover arquivos apenas por preferência.
- Não modernizar apenas parte de uma Feature.
- Toda melhoria deve manter a consistência com o restante do projeto.

---

# 22. Testabilidade

Todo código deve ser desenvolvido pensando em testes.

Evitar dependências ocultas.

Evitar acoplamento.

Sempre favorecer injeção de dependências.

Nunca criar código impossível de testar.

---

# 23. Testes

Sempre que solicitado gerar testes consistentes.

Priorizar:

- comportamento
- regras de negócio
- fluxos críticos

Evitar testes frágeis.

---

# 24. Mock

Sempre utilizar mocks simples.

Nunca duplicar mocks.

Sempre reutilizar.

---

# 25. Separação

Testes nunca devem alterar código de produção.

---

# 26. Code Review

Todo código deve passar pelas seguintes verificações.

---

# Arquitetura

✔ segue o padrão do projeto

✔ respeita o CONVENTIONS.md

✔ respeita DDD

✔ respeita SOLID

✔ respeita Clean Architecture

✔ respeita Feature First

✔ respeita Separation of Concerns

---

# 27. Regra Final

Código deve ser:

Limpo.

Consistente.

Testável.

Manutenível.

Escalável.

---

# CONVENTIONS.md

# Convenções Globais do Projeto

Versão: 1.0

Este documento define os padrões obrigatórios para todos os agentes responsáveis pela implementação, manutenção e revisão do projeto.

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

# 8. Reutilização

Antes de criar qualquer componente verificar:

Já existe?

Pode ser reutilizado?

Pode ser estendido?

Evitar duplicação.

---

# 9. DRY

Nunca repetir código.

Caso exista repetição:

Extrair.

---

# 10. KISS

Sempre escolher a solução mais simples.

Nunca criar arquitetura complexa sem necessidade.

---

# 11. YAGNI

Nunca implementar funcionalidades futuras.

Implementar apenas o necessário.

---

# 12. SOLID

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

# 13. Clean Code

Sempre:

Nomes claros.

Métodos pequenos.

Classes pequenas.

Responsabilidades claras.

Poucos níveis de indentação.

Poucos parâmetros.

---

# 14. Complexidade

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

# 15. Legibilidade

O código deve ser compreendido sem comentários.

Comentários apenas quando agregarem contexto.

Nunca comentar código óbvio.

---

# 16. Performance

Performance deve fazer parte da arquitetura.

Nunca ser adicionada posteriormente.

---

# 17. Escalabilidade

Toda implementação deve suportar crescimento.

Evitar soluções temporárias.

---

# 18. Dependências

Adicionar bibliotecas apenas quando realmente necessárias.

---

# 19. Atualizações

Sempre utilizar a abordagem mais moderna suportada pela versão do projeto.

Nunca introduzir APIs depreciadas.

---

# 20. Revisão

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

# 21. Regra de Evolução

Ao modificar um código existente:

- Não alterar estilo arquitetural.
- Não renomear arquivos sem necessidade.
- Não mover arquivos apenas por preferência.
- Não modernizar apenas parte de uma Feature.
- Toda melhoria deve manter a consistência com o restante do projeto.

---

# 22. Testabilidade

Todo código deve ser desenvolvido pensando em testes.

Evitar dependências ocultas.

Evitar acoplamento.

Sempre favorecer injeção de dependências.

Nunca criar código impossível de testar.

---

# 23. Testes

Sempre que solicitado gerar testes consistentes.

Priorizar:

- comportamento
- regras de negócio
- fluxos críticos

Evitar testes frágeis.

---

# 24. Mock

Sempre utilizar mocks simples.

Nunca duplicar mocks.

Sempre reutilizar.

---

# 25. Separação

Testes nunca devem alterar código de produção.

---

# 26. Code Review

Todo código deve passar pelas seguintes verificações.

---

# Arquitetura

✔ segue o padrão do projeto

✔ respeita o CONVENTIONS.md

✔ respeita DDD

✔ respeita SOLID

✔ respeita Clean Architecture

✔ respeita Feature First

✔ respeita Separation of Concerns

---

# 27. Regra Final

Código deve ser:

Limpo.

Consistente.

Testável.

Manutenível.

Escalável.

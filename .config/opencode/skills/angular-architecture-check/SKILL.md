---
name: angular-architecture-check
description: Use quando o usuário pedir para verificar e validar a arquitetura Angular de um projeto, analisar estrutura, identificar padrões ou validar conformidade.
---

# Angular Architecture Check

## Descrição

Skill para verificar e validar a arquitetura Angular de um projeto.

## Quando Usar

- Ao iniciar uma nova tarefa
- Antes de criar novos componentes
- Para validar estrutura existente

## Fluxo Obrigatório

1. **Ler ANGULAR_CONVENTIONS.MD** (se existir)
2. **Analisar estrutura** do projeto
3. **Identificar padrões** existentes
4. **Verificar organização** por Features
5. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

## Checklist

### Estrutura

- [ ] Organizado por Features (não por tipo)
- [ ] Cada Feature independente
- [ ] Separation of Concerns

### Padrões

- [ ] DDD (Domain-Driven Design)
- [ ] Clean Architecture
- [ ] SOLID
- [ ] Feature First

### Componentes

- [ ] Smart Components (coordenação)
- [ ] Dumb Components (apresentação)
- [ ] Responsabilidade única

### Estado

- [ ] Signals > Observable
- [ ] Computed para derivados
- [ ] Effect para side effects

### Comunicação

- [ ] Page → Facade → Service → API
- [ ] Nunca Component → API direto

## Saída Esperada

Relatório com:

- Padrão identificado
- Conformidade com convenções
- Sugestões de melhoria (se houver)

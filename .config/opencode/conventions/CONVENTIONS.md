# CONVENTIONS.md

# Roteador de Convenções

Versão: 1.0

Este arquivo é o roteador central de convenções do projeto.

Para qual convenção devo me referenciar?

---

# Fluxo de Decisão

1. **Primeiro**: Ler GLOBAL_CONVENTIONS.MD (convenções gerais)
2. **Depois**: Ler a convenção específica do framework/tecnologia
3. **Por fim**: Seguir as regras de conflito

---

# Convenções Disponíveis

## Angular
- Arquivo: `ANGULAR_CONVENTIONS.MD`
- Usar quando: Projetos Angular (components, services, facades, signals, etc.)

## NestJS (futuro)
- Arquivo: `NEST_CONVENTIONS.MD`
- Usar quando: Projetos NestJS (controllers, providers, modules, etc.)

## Python (futuro)
- Arquivo: `PYTHON_CONVENTIONS.MD`
- Usar quando: Projetos Python (classes, funções, etc.)

---

# Regras de Conflito

1. **GLOBAL_CONVENTIONS.MD** é a base para TODOS os projetos
2. **Convenção específica** complementa e detalha a base
3. **Caso conflito**: O projeto existente SEMPRE possui prioridade
4. **Caso não exista padrão**: Seguir rigorosamente este documento

---

# Ordem de Leitura Obrigatória

```
1. CONVENTIONS.md (este arquivo)
   ↓
2. GLOBAL_CONVENTIONS.MD
   ↓
3. [ANGULAR_CONVENTIONS.MD | NEST_CONVENTIONS.MD | PYTHON_CONVENTIONS.MD]
   ↓
4. Regras do projeto existente
```

---

# Instruções para Agents e Skills

## Ao iniciar qualquer tarefa:

1. Ler este arquivo primeiro
2. Identificar o framework/tecnologia do projeto
3. Ler a convenção específica correspondente
4. Ler as convenções globais
5. Verificar se existe padrão no projeto
6. Seguir a ordem de decisão estabelecida

## Prioridade:

1. Projeto existente (sempre)
2. Convenção específica (ANGULAR, NEST, PYTHON, etc.)
3. Convenções globais
4. Este roteador

---

# Adicionando Novas Convenções

Para adicionar uma nova convenção (ex: NestJS, Python, etc.):

1. Criar o arquivo `NOVA_CONVENCAO_CONVENTIONS.MD` nesta pasta
2. Adicionar a referência neste roteador
3. Atualizar os agents e skills para reconhecer a nova convenção

---

# Validação

Antes de finalizar qualquer tarefa, validar:

- [ ] GLOBAL_CONVENTIONS.MD foi lido?
- [ ] Convenção específica foi lida?
- [ ] Projeto existente foi analisado?
- [ ] Padrão do projeto foi respeitado?
- [ ] Não há conflitos de convenções?
- [ ] Código está consistente com o projeto?

---

# NOTA IMPORTANTE

Este arquivo é apenas um roteador.

As convenções REAIS estão nos arquivos:
- GLOBAL_CONVENTIONS.MD
- ANGULAR_CONVENTIONS.MD
- NEST_CONVENTIONS.MD (futuro)
- PYTHON_CONVENTIONS.MD (futuro)

NÃO executar código baseado apenas neste arquivo.

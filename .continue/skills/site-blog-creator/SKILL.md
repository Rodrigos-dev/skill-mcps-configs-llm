---
name: site-blog-creator
description: Use quando o usuário pedir para criar sites, blogs, landing pages, portfólios ou sistemas de cadastro simples com arquitetura limpa (Clean Code, DDD, SOLID).
---

# Site Blog Creator - Master Level

## Descrição

Skill para criar sites, blogs e landing pages com arquitetura limpa, seguindo Clean Code, DDD, SOLID e Design Patterns.

## Quando Usar

- Sites institucionais
- Blogs estáticos
- Landing pages
- Portfólios
- Sistemas de cadastro simples
- Galerias de imagens

## Características

- Zero instalação (sem npm, sem build)
- Arquitetura limpa e escalável
- Dados locais em JSON
- Imagens/vídeos em Base64/Blob
- Código de produção

---

## Fluxo Obrigatório

1. **Ler regras na pasta rules(global e ou local)** e seguir com muita seriedade,

---

## Princípios Arquiteturais

### Clean Code

- Nomes claros e descritivos
- Funções pequenas (máx 20 linhas)
- Responsabilidade única
- Código autoexplicativo

### DDD (Domain-Driven Design)

- Separação por domínios
- Entidades e Value Objects
- Repositórios para acesso a dados
- Services para lógica de negócio

### SOLID

- **S**: Responsibility única
- **O**: Aberto para extensão
- **L**: Substituição de Liskov
- **I**: Interfaces pequenas
- **D**: Inversão de dependência

### Design Patterns

- Module Pattern (encapsulamento)
- Observer (eventos)
- Factory (criação de objetos)
- Repository (acesso a dados)

---

## Estrutura de Pastas (DDD)

```
projeto/
  index.html
  assets/
    css/
      globals/
        reset.css
        variables.css
        typography.css
      components/
        header.css
        footer.css
        card.css
        form.css
      pages/
        home.css
        blog.css
    js/
      core/
        app.js              ← bootstrap da aplicação
        config.js           ← configurações globais
        router.js           ← roteamento simples
      domain/
        entities/
          post.entity.js    ← entidade Post
          usuario.entity.js ← entidade Usuario
          imagem.entity.js  ← entidade Imagem
        value-objects/
          id.vo.js          ← Value Object ID
          titulo.vo.js      ← Value Object Título
          descricao.vo.js   ← Value Object Descrição
          imagem.vo.js      ← Value Object Imagem
        repositories/
          post.repository.js
          usuario.repository.js
        services/
          post.service.js
          usuario.service.js
          imagem.service.js
      infrastructure/
        storage/
          local-storage.adapter.js
          json-storage.adapter.js
        converters/
          base64.converter.js
          blob.converter.js
        http/
          fetch.client.js
      ui/
        components/
          card.component.js
          form.component.js
          modal.component.js
        utils/
          dom.helper.js
          validator.js
  pages/
    home/
      home.html
      home.js
      home.init.js
    blog/
      blog.html
      blog.js
      blog.init.js
    cadastro/
      cadastro.html
      cadastro.js
      cadastro.init.js
  data/
    posts.json
    usuarios.json
```

---

## Camadas (Clean Architecture)

### 1. Domain (Domínio)

Entidades, Value Objects, Interfaces de Repositórios.

### 2. Infrastructure (Infraestrutura)

Implementações concretas: Storage, HTTP, Converters.

### 3. UI (Apresentação)

Componentes, Helpers, Utils.

### 4. Application (Aplicação)

Orquestração: Services, Controllers.

---

## Domain Layer

### Entidades

#### Post Entity

```javascript
// domain/entities/post.entity.js

/**
 * @typedef {Object} PostProps
 * @property {string} id
 * @property {string} titulo
 * @property {string} descricao
 * @property {Imagem|null} imagem
 * @property {Date} dataCriacao
 * @property {Date} dataAtualizacao
 */

export class Post {
  #props;

  /**
   * @param {PostProps} props
   */
  constructor(props) {
    this.#props = {
      id: props.id,
      titulo: props.titulo,
      descricao: props.descricao,
      imagem: props.imagem || null,
      dataCriacao: props.dataCriacao || new Date(),
      dataAtualizacao: props.dataAtualizacao || new Date(),
    };
    Object.freeze(this);
  }

  get id() {
    return this.#props.id;
  }
  get titulo() {
    return this.#props.titulo;
  }
  get descricao() {
    return this.#props.descricao;
  }
  get imagem() {
    return this.#props.imagem;
  }
  get dataCriacao() {
    return this.#props.dataCriacao;
  }
  get dataAtualizacao() {
    return this.#props.dataAtualizacao;
  }

  /**
   * @param {Partial<PostProps>} dados
   * @returns {Post}
   */
  atualizar(dados) {
    return new Post({
      ...this.#props,
      ...dados,
      dataAtualizacao: new Date(),
    });
  }

  /**
   * @returns {Object}
   */
  toJSON() {
    return { ...this.#props };
  }

  /**
   * @param {Object} json
   * @returns {Post}
   */
  static fromJSON(json) {
    return new Post({
      ...json,
      dataCriacao: new Date(json.dataCriacao),
      dataAtualizacao: new Date(json.dataAtualizacao),
    });
  }
}
```

#### Value Objects

```javascript
// domain/value-objects/id.vo.js

export class Id {
  #valor;

  constructor(valor) {
    if (!valor) throw new Error('ID é obrigatório');
    this.#valor = valor;
    Object.freeze(this);
  }

  get valor() {
    return this.#valor;
  }

  static criar() {
    return new Id(crypto.randomUUID());
  }

  igual(outro) {
    return this.#valor === outro.valor;
  }
}
```

```javascript
// domain/value-objects/titulo.vo.js

export class Titulo {
  #valor;
  #tamanhoMinimo = 3;
  #tamanhoMaximo = 100;

  constructor(valor) {
    if (!valor) throw new Error('Título é obrigatório');
    if (valor.length < this.#tamanhoMinimo) {
      throw new Error(`Título deve ter mínimo ${this.#tamanhoMinimo} caracteres`);
    }
    if (valor.length > this.#tamanhoMaximo) {
      throw new Error(`Título deve ter máximo ${this.#tamanhoMaximo} caracteres`);
    }
    this.#valor = valor.trim();
    Object.freeze(this);
  }

  get valor() {
    return this.#valor;
  }
}
```

```javascript
// domain/value-objects/imagem.vo.js

export class Imagem {
  #dados;
  #tipo;

  /**
   * @param {string} dados - Base64 ou URL
   * @param {string} tipo - 'base64' | 'url' | 'blob'
   */
  constructor(dados, tipo) {
    if (!dados) throw new Error('Dados da imagem são obrigatórios');
    if (!['base64', 'url', 'blob'].includes(tipo)) {
      throw new Error('Tipo inválido');
    }
    this.#dados = dados;
    this.#tipo = tipo;
    Object.freeze(this);
  }

  get dados() {
    return this.#dados;
  }
  get tipo() {
    return this.#tipo;
  }

  get ehBase64() {
    return this.#tipo === 'base64';
  }
  get ehUrl() {
    return this.#tipo === 'url';
  }
  get ehBlob() {
    return this.#tipo === 'blob';
  }

  static deBase64(dados) {
    return new Imagem(dados, 'base64');
  }

  static deUrl(url) {
    return new Imagem(url, 'url');
  }
}
```

---

## Infrastructure Layer

### Storage Adapter

```javascript
// infrastructure/storage/local-storage.adapter.js

/**
 * @template T
 * @implements {IStorageAdapter<T>}
 */
export class LocalStorageAdapter {
  #prefix;

  /**
   * @param {string} prefix
   */
  constructor(prefix = 'app') {
    this.#prefix = prefix;
  }

  /**
   * @param {string} chave
   * @returns {T|null}
   */
  obter(chave) {
    try {
      const dados = localStorage.getItem(this.#chaveCompleta(chave));
      return dados ? JSON.parse(dados) : null;
    } catch (erro) {
      console.error(`Erro ao obter ${chave}:`, erro);
      return null;
    }
  }

  /**
   * @param {string} chave
   * @param {T} valor
   */
  salvar(chave, valor) {
    try {
      const dados = JSON.stringify(valor);
      localStorage.setItem(this.#chaveCompleta(chave), dados);
    } catch (erro) {
      console.error(`Erro ao salvar ${chave}:`, erro);
      throw erro;
    }
  }

  /**
   * @param {string} chave
   */
  remover(chave) {
    localStorage.removeItem(this.#chaveCompleta(chave));
  }

  /**
   * @returns {string[]}
   */
  chaves() {
    const chaves = [];
    for (let i = 0; i < localStorage.length; i++) {
      const chave = localStorage.key(i);
      if (chave.startsWith(this.#prefix)) {
        chaves.push(chave.replace(`${this.#prefix}_`, ''));
      }
    }
    return chaves;
  }

  /**
   * @param {string} chave
   * @returns {string}
   */
  #chaveCompleta(chave) {
    return `${this.#prefix}_${chave}`;
  }
}
```

### Repository

```javascript
// domain/repositories/post.repository.js

/**
 * @template T
 * @typedef {Object} IRepository
 * @property {function(): Promise<T[]>} buscarTodos
 * @property {function(string): Promise<T|null>} buscarPorId
 * @property {function(T): Promise<T>} salvar
 * @property {function(string, Partial<T>): Promise<T|null>} atualizar
 * @property {function(string): Promise<boolean>} deletar
 */

export class PostRepository {
  #storage;
  #chave = 'posts';

  /**
   * @param {IStorageAdapter} storage
   */
  constructor(storage) {
    this.#storage = storage;
  }

  /**
   * @returns {Promise<Post[]>}
   */
  async buscarTodos() {
    const dados = this.#storage.obter(this.#chave) || [];
    return dados.map(dado => Post.fromJSON(dado));
  }

  /**
   * @param {string} id
   * @returns {Promise<Post|null>}
   */
  async buscarPorId(id) {
    const dados = this.#storage.obter(this.#chave) || [];
    const encontrado = dados.find(item => item.id === id);
    return encontrado ? Post.fromJSON(encontrado) : null;
  }

  /**
   * @param {Post} post
   * @returns {Promise<Post>}
   */
  async salvar(post) {
    const dados = this.#storage.obter(this.#chave) || [];
    dados.push(post.toJSON());
    this.#storage.salvar(this.#chave, dados);
    return post;
  }

  /**
   * @param {string} id
   * @param {Partial<Post>} dadosAtualizados
   * @returns {Promise<Post|null>}
   */
  async atualizar(id, dadosAtualizados) {
    const dados = this.#storage.obter(this.#chave) || [];
    const index = dados.findIndex(item => item.id === id);

    if (index === -1) return null;

    const antigo = Post.fromJSON(dados[index]);
    const atualizado = antigo.atualizar(dadosAtualizados);

    dados[index] = atualizado.toJSON();
    this.#storage.salvar(this.#chave, dados);

    return atualizado;
  }

  /**
   * @param {string} id
   * @returns {Promise<boolean>}
   */
  async deletar(id) {
    const dados = this.#storage.obter(this.#chave) || [];
    const filtrados = dados.filter(item => item.id !== id);
    this.#storage.salvar(this.#chave, filtrados);
    return true;
  }
}
```

### Services

```javascript
// domain/services/post.service.js

export class PostService {
  #repository;

  /**
   * @param {PostRepository} repository
   */
  constructor(repository) {
    this.#repository = repository;
  }

  /**
   * @returns {Promise<Post[]>}
   */
  async listarTodos() {
    return this.#repository.buscarTodos();
  }

  /**
   * @param {string} id
   * @returns {Promise<Post>}
   */
  async buscarPorId(id) {
    const post = await this.#repository.buscarPorId(id);
    if (!post) throw new Error('Post não encontrado');
    return post;
  }

  /**
   * @param {Object} dados
   * @returns {Promise<Post>}
   */
  async criar(dados) {
    const id = Id.criar();
    const titulo = new Titulo(dados.titulo);
    const descricao = dados.descricao?.trim() || '';

    let imagem = null;
    if (dados.imagemDados) {
      imagem = Imagem.deBase64(dados.imagemDados);
    }

    const post = new Post({
      id: id.valor,
      titulo: titulo.valor,
      descricao,
      imagem,
    });

    return this.#repository.salvar(post);
  }

  /**
   * @param {string} id
   * @param {Object} dados
   * @returns {Promise<Post>}
   */
  async atualizar(id, dados) {
    const dadosParaAtualizar = {};

    if (dados.titulo) {
      dadosParaAtualizar.titulo = new Titulo(dados.titulo).valor;
    }

    if (dados.descricao !== undefined) {
      dadosParaAtualizar.descricao = dados.descricao.trim();
    }

    if (dados.imagemDados) {
      dadosParaAtualizar.imagem = Imagem.deBase64(dados.imagemDados);
    }

    const atualizado = await this.#repository.atualizar(id, dadosParaAtualizar);
    if (!atualizado) throw new Error('Post não encontrado');
    return atualizado;
  }

  /**
   * @param {string} id
   * @returns {Promise<boolean>}
   */
  async deletar(id) {
    return this.#repository.deletar(id);
  }

  /**
   * @param {string} termo
   * @returns {Promise<Post[]>}
   */
  async buscar(termo) {
    const todos = await this.#repository.buscarTodos();
    const termoLower = termo.toLowerCase();

    return todos.filter(
      post =>
        post.titulo.toLowerCase().includes(termoLower) ||
        post.descricao.toLowerCase().includes(termoLower),
    );
  }
}
```

### Converters

```javascript
// infrastructure/converters/base64.converter.js

export class Base64Converter {
  /**
   * @param {File} arquivo
   * @returns {Promise<string>}
   */
  static async converter(arquivo) {
    return new Promise((resolve, reject) => {
      if (!arquivo) {
        reject(new Error('Arquivo é obrigatório'));
        return;
      }

      const reader = new FileReader();
      reader.onload = () => resolve(reader.result);
      reader.onerror = () => reject(new Error('Erro ao converter arquivo'));
      reader.readAsDataURL(arquivo);
    });
  }

  /**
   * @param {File} arquivo
   * @param {number} tamanhoMaximoMB - Tamanho máximo em MB
   * @returns {Promise<string>}
   */
  static async converterComValidacao(arquivo, tamanhoMaximoMB = 5) {
    const tamanhoBytes = tamanhoMaximoMB * 1024 * 1024;

    if (arquivo.size > tamanhoBytes) {
      throw new Error(`Arquivo excede ${tamanhoMaximoMB}MB`);
    }

    return this.converter(arquivo);
  }

  /**
   * @param {string} base64
   * @returns {boolean}
   */
  static ehValido(base64) {
    return /^data:image\/\w+;base64,/.test(base64);
  }

  /**
   * @param {string} base64
   * @returns {string}
   */
  static extrairTipo(base64) {
    const match = base64.match(/^data:(\w+\/\w+);/);
    return match ? match[1] : 'unknown';
  }
}
```

---

## UI Layer

### Components

```javascript
// ui/components/card.component.js

export class CardComponent {
  #post;
  #onClicar;

  /**
   * @param {Post} post
   * @param {function} onClicar
   */
  constructor(post, onClicar) {
    this.#post = post;
    this.#onClicar = onClicar;
  }

  /**
   * @returns {HTMLElement}
   */
  renderizar() {
    const card = document.createElement('article');
    card.className = 'card';
    card.setAttribute('data-id', this.#post.id);

    const imagemSrc = this.#post.imagem?.dados || 'https://via.placeholder.com/300x200';
    const imagemAlt = this.#post.titulo;

    card.innerHTML = `
      <img 
        class="card__imagem" 
        src="${imagemSrc}" 
        alt="${imagemAlt}"
        loading="lazy"
      >
      <div class="card__conteudo">
        <h3 class="card__titulo">${this.#post.titulo}</h3>
        <p class="card__descricao">${this.#post.descricao}</p>
        <time class="card__data" datetime="${this.#post.dataCriacao.toISOString()}">
          ${this.#formatarData(this.#post.dataCriacao)}
        </time>
      </div>
    `;

    if (this.#onClicar) {
      card.addEventListener('click', () => this.#onClicar(this.#post));
      card.classList.add('card--clicavel');
    }

    return card;
  }

  /**
   * @param {Date} data
   * @returns {string}
   */
  #formatarData(data) {
    return data.toLocaleDateString('pt-BR', {
      day: '2-digit',
      month: '2-digit',
      year: 'numeric',
    });
  }
}
```

```javascript
// ui/components/form.component.js

export class FormComponent {
  #configuracao;
  #onSubmit;

  /**
   * @param {Object} configuracao
   * @param {function} onSubmit
   */
  constructor(configuracao, onSubmit) {
    this.#configuracao = configuracao;
    this.#onSubmit = onSubmit;
  }

  /**
   * @returns {HTMLElement}
   */
  renderizar() {
    const form = document.createElement('form');
    form.className = 'form';
    form.id = this.#configuracao.id;

    this.#configuracao.campos.forEach(campo => {
      const elemento = this.#criarCampo(campo);
      form.appendChild(elemento);
    });

    const botaoSubmit = document.createElement('button');
    botaoSubmit.type = 'submit';
    botaoSubmit.className = 'form__botao';
    botaoSubmit.textContent = this.#configuracao.textoBotao || 'Enviar';
    form.appendChild(botaoSubmit);

    form.addEventListener('submit', e => this.#handleSubmit(e));

    return form;
  }

  /**
   * @param {Object} campo
   * @returns {HTMLElement}
   */
  #criarCampo(campo) {
    const wrapper = document.createElement('div');
    wrapper.className = 'form__campo';

    const label = document.createElement('label');
    label.className = 'form__label';
    label.textContent = campo.label;
    label.setAttribute('for', campo.nome);
    wrapper.appendChild(label);

    let elemento;

    switch (campo.tipo) {
      case 'textarea':
        elemento = document.createElement('textarea');
        break;
      case 'file':
        elemento = document.createElement('input');
        elemento.accept = campo.accept || 'image/*';
        break;
      default:
        elemento = document.createElement('input');
        elemento.type = campo.tipo || 'text';
    }

    elemento.id = campo.nome;
    elemento.name = campo.nome;
    elemento.className = 'form__input';

    if (campo.placeholder) {
      elemento.placeholder = campo.placeholder;
    }

    if (campo.obrigatorio) {
      elemento.required = true;
    }

    wrapper.appendChild(elemento);

    const erro = document.createElement('span');
    erro.className = 'form__erro';
    erro.id = `${campo.nome}-erro`;
    wrapper.appendChild(erro);

    return wrapper;
  }

  /**
   * @param {Event} e
   */
  async #handleSubmit(e) {
    e.preventDefault();

    const form = e.target;
    const dados = new FormData(form);
    const objetoDados = {};

    for (const [chave, valor] of dados.entries()) {
      objetoDados[chave] = valor;
    }

    const inputImagem = form.querySelector('input[type="file"]');
    if (inputImagem && inputImagem.files.length > 0) {
      objetoDados.imagemDados = await Base64Converter.converter(inputImagem.files[0]);
    }

    if (this.#onSubmit) {
      this.#onSubmit(objetoDados);
    }
  }

  limpar() {
    const form = document.getElementById(this.#configuracao.id);
    if (form) form.reset();
  }
}
```

### DOM Helper

```javascript
// ui/utils/dom.helper.js

export class DomHelper {
  /**
   * @param {string} seletor
   * @param {HTMLElement} pai
   * @returns {HTMLElement|null}
   */
  static buscar(seletor, pai = document) {
    return pai.querySelector(seletor);
  }

  /**
   * @param {string} seletor
   * @param {HTMLElement} pai
   * @returns {HTMLElement[]}
   */
  static buscarTodos(seletor, pai = document) {
    return Array.from(pai.querySelectorAll(seletor));
  }

  /**
   * @param {string} seletor
   * @param {HTMLElement} pai
   * @returns {HTMLElement}
   */
  static buscarOuCriar(seletor, pai = document) {
    let elemento = this.buscar(seletor, pai);
    if (!elemento) {
      elemento = document.createElement('div');
      elemento.id = seletor.replace('#', '');
      pai.appendChild(elemento);
    }
    return elemento;
  }

  /**
   * @param {HTMLElement} elemento
   * @param {string} conteudo
   */
  static definirConteudo(elemento, conteudo) {
    if (elemento) elemento.innerHTML = conteudo;
  }

  /**
   * @param {HTMLElement} elemento
   * @param {boolean} condicao
   * @param {string} classe
   */
  static toggleClasse(elemento, condicao, classe) {
    if (elemento) {
      elemento.classList.toggle(classe, condicao);
    }
  }

  /**
   * @param {HTMLElement} elemento
   * @param {string} mensagem
   */
  static mostrarErro(elemento, mensagem) {
    if (elemento) {
      elemento.textContent = mensagem;
      elemento.classList.add('form__erro--visivel');
    }
  }

  /**
   * @param {HTMLElement} elemento
   */
  static limparErro(elemento) {
    if (elemento) {
      elemento.textContent = '';
      elemento.classList.remove('form__erro--visivel');
    }
  }
}
```

---

## Application Layer

### Bootstrap

```javascript
// core/app.js

export class App {
  #config;
  #rotas;

  /**
   * @param {Object} config
   */
  constructor(config) {
    this.#config = config;
    this.#rotas = new Map();
  }

  /**
   * @param {string} caminho
   * @param {Function} handler
   */
  registrarRota(caminho, handler) {
    this.#rotas.set(caminho, handler);
  }

  iniciar() {
    document.addEventListener('DOMContentLoaded', () => {
      this.#inicializar();
    });
  }

  #inicializar() {
    const caminho = this.#obterCaminho();
    const handler = this.#rotas.get(caminho);

    if (handler) {
      const services = this.#criarServices();
      handler(services);
    } else {
      console.warn(`Rota não encontrada: ${caminho}`);
    }
  }

  /**
   * @returns {string}
   */
  #obterCaminho() {
    const path = window.location.pathname;
    const segments = path.split('/').filter(Boolean);
    return segments[segments.length - 1] || 'index.html';
  }

  /**
   * @returns {Object}
   */
  #criarServices() {
    const storage = new LocalStorageAdapter(this.#config.appName);
    const postRepository = new PostRepository(storage);
    const postService = new PostService(postRepository);

    return { postService };
  }
}
```

### Config

```javascript
// core/config.js

export const Config = Object.freeze({
  appName: 'meu_site',

  storage: {
    prefix: 'app',
    tamanhoMaximoImagem: 5, // MB
  },

  rotas: {
    home: 'home.html',
    blog: 'blog.html',
    cadastro: 'cadastro.html',
  },
});
```

### Page Initialization

```javascript
// pages/home/home.init.js

import { App } from '../../assets/js/core/app.js';
import { Config } from '../../assets/js/core/config.js';

const app = new App(Config);

app.registrarRota('home.html', async services => {
  const { postService } = services;

  const container = DomHelper.buscar('#lista-itens');
  const formConfig = {
    id: 'form-cadastro',
    campos: [
      { nome: 'titulo', label: 'Título', tipo: 'text', obrigatorio: true },
      { nome: 'descricao', label: 'Descrição', tipo: 'textarea' },
      { nome: 'imagem', label: 'Imagem', tipo: 'file', accept: 'image/*' },
    ],
    textoBotao: 'Cadastrar',
  };

  const form = new FormComponent(formConfig, async dados => {
    await postService.criar(dados);
    form.limpar();
    await carregarItens();
  });

  const formContainer = DomHelper.buscar('#form-container');
  formContainer.appendChild(form.renderizar());

  async function carregarItens() {
    const posts = await postService.listarTodos();
    container.innerHTML = '';

    posts.forEach(post => {
      const card = new CardComponent(post, p => {
        console.log('Post clicado:', p);
      });
      container.appendChild(card.renderizar());
    });
  }

  await carregarItens();
});

app.iniciar();
```

---

## Checklist de Qualidade

### Clean Code

- [ ] Nomes descritivos (camelCase, PascalCase)
- [ ] Funções pequenas (máx 20 linhas)
- [ ] Sem código duplicado
- [ ] Código autoexplicativo

### DDD

- [ ] Entidades imutáveis
- [ ] Value Objects com validação
- [ ] Repositórios para acesso a dados
- [ ] Services para lógica de negócio

### SOLID

- [ ] Responsibility única
- [ ] Aberto para extensão
- [ ] Inversão de dependência

### Design Patterns

- [ ] Module Pattern
- [ ] Repository Pattern
- [ ] Factory Pattern
- [ ] Observer (eventos)

### Arquitetura

- [ ] Separação de camadas
- [ ] Domain isolado
- [ ] Infrastructure concreta
- [ ] UI desacoplada

### Performance

- [ ] Lazy loading em imagens
- [ ] Dados cacheados
- [ ] Mínimo DOM manipulation

### Acessibilidade

- [ ] Labels associados
- [ ] ARIA labels
- [ ] Navegação por teclado
- [ ] Contrast ratio adequado

---

## Saída

Projeto com arquitetura profissional, escalável e manutenível.

# Midnight Vinyl

### Autor: Samuel Videlski Andrade de Lima 

O **Midnight Vinyl** é uma aplicação web para descoberta e criação de playlists personalizadas.

A aplicação permite que o usuário crie uma conta e informe artistas, músicas ou estilos musicais que gosta. A partir dessas informações, o sistema consulta uma API pública de música e gera uma playlist com artistas e músicas semelhantes às preferências informadas.

Após gerar uma playlist, o usuário pode salvá-la e posteriormente acessá-la através da **Library**, onde ficam armazenadas as playlists criadas.

O projeto possui uma interface inspirada na estética de uma coleção de discos de vinil, utilizando uma identidade visual escura com destaque em verde neon.

---

## 📚 Documentação do Projeto

* 📄 [Product Requirements Document (PRD)](docs/prd.md) - Requisitos, objetivos, atores e histórias de usuário.
* 🛠️ [Architecture](docs/architecture.md) - Arquitetura da aplicação, estrutura de dados, APIs e organização do projeto.
* 🎨 [Design System](docs/design-system.md) - Cores, tipografia, componentes e identidade visual.

---

## 🎨 Design

A interface do **Midnight Vinyl** foi desenvolvida com uma identidade visual inspirada em música, discos de vinil e ambientes noturnos.

### Características visuais

* Fundo predominantemente escuro.
* Verde neon como cor principal de destaque.
* Tipografia moderna.
* Cards e elementos com aparência minimalista.
* Interface responsiva para dispositivos móveis e desktops.
* Elementos visuais inspirados em capas de álbuns e equipamentos musicais.

### Principais telas

* Landing Page
* Cadastro
* Login
* Crate Digger
* Resultado da Playlist
* Library

---

## 🌐 Site em Produção

> Adicionar posteriormente o endereço do site publicado.

---

## 💻 Tecnologias e Dependências

### Frontend

* HTML5
* CSS3
* Sass / SCSS
* JavaScript
* jQuery

### Framework CSS

* MaterializeCSS

### APIs

* JSON Server - Utilizado como API REST para persistência dos dados da aplicação.
* API pública de música - Utilizada para pesquisa e recomendação de artistas e músicas.

### Ferramentas

* Node.js
* NPM
* Git
* GitHub
* ESLint
* Prettier

---

## 🎯 Objetivo da Aplicação

O objetivo principal do **Midnight Vinyl** é permitir que o usuário descubra novas músicas e artistas a partir de seus próprios gostos musicais.

O fluxo principal da aplicação é:

```text
Usuário
   ↓
Cadastro / Login
   ↓
Crate Digger
   ↓
Artista / Música / Vibe
   ↓
API Pública de Música
   ↓
Recomendações
   ↓
Playlist
   ↓
Salvar Playlist
   ↓
Library


---

✨ Funcionalidades

👤 Conta

Cadastro de usuário.

Login.

Logout.

Controle de sessão utilizando Web Storage.


🎵 Crate Digger

Inserção de artistas.

Inserção de músicas.

Inserção de estilos ou vibes.

Consulta à API pública de música.

Geração de recomendações.


💿 Playlist

Exibição das músicas recomendadas.

Exibição do artista de cada música.

Exibição da duração.

Exibição da capa da playlist.

Possibilidade de salvar a playlist.

Possibilidade de descartar a playlist atual e realizar uma nova busca.


📚 Library

Visualização das playlists salvas.

Acesso aos detalhes de uma playlist.

Associação das playlists ao usuário que as criou.

Exclusão de playlists.



---

📋 Checklist | Indicadores de Desempenho (ID) dos Resultados de Aprendizagem (RA)

RA1 — CSS Frameworks, Layout e Responsividade

[ ] ID01 — Protótipo mobile e desktop.

[ ] ID02 — Utilização de framework CSS responsivo.

[ ] ID03 — Utilização de Flexbox e Grid com CSS.

[ ] ID04 — Utilização de componentes do framework.

[ ] ID05 — Utilização de unidades relativas.

[ ] ID06 — Implementação de Design System.

[ ] ID07 — Utilização de Sass/SCSS.

[ ] ID08 — Tipografia responsiva.

[ ] ID09 — Imagens responsivas.

[ ] ID10 — Otimização moderna de imagens.


RA2 — Formulários

[ ] ID11 — Validação nativa de formulários HTML.

[ ] ID12 — Utilização de expressões regulares.

[ ] ID13 — Utilização de elementos de seleção.

[ ] ID14 — Utilização de Web Storage.


RA3 — Ferramentas e Boas Práticas

[ ] ID15 — Utilização de Node.js e NPM.

[ ] ID16 — Utilização de Git, GitHub e .gitignore.

[ ] ID17 — README com documentação do projeto.

[ ] ID18 — Estrutura modular da aplicação.

[ ] ID19 — Utilização de ESLint e Prettier.


RA4 — Bibliotecas JavaScript

[ ] ID20 — Utilização de jQuery.

[ ] ID21 — Utilização de plugin jQuery.


RA5 — APIs e Requisições Assíncronas

[ ] ID22 — Persistência utilizando JSON Server.

[ ] ID23 — Consulta e exibição de dados utilizando JSON Server.

[ ] ID24 — Consumo de API pública com tratamento de erros.



---

🚀 Manual de Execução

1. Clonar o repositório

git clone [URL_DO_REPOSITORIO]

Entrar na pasta do projeto:

cd midnight-vinyl

2. Instalar as dependências

npm install

3. Executar o JSON Server

npm run json:server

4. Executar o Sass

npm run sass

5. Executar o projeto

Abrir o projeto utilizando uma extensão como Live Server ou outro servidor HTTP local.


---

📁 Estrutura do Projeto

midnight-vinyl/
│
├── docs/
│   ├── prd.md
│   ├── architecture.md
│   └── design-system.md
│
├── src/
│   ├── css/
│   ├── scss/
│   ├── js/
│   │   ├── main.js
│   │   ├── auth.js
│   │   ├── crate-digger.js
│   │   ├── playlist.js
│   │   ├── library.js
│   │   ├── api.js
│   │   ├── storage.js
│   │   ├── validation.js
│   │   └── utils.js
│   │
│   ├── pages/
│   └── assets/
│       ├── images/
│       └── icons/
│
├── db.json
├── routes.json
├── index.html
├── package.json
├── .gitignore
└── README.md


---

📱 Telas da Aplicação

Landing Page

Apresenta o conceito do Midnight Vinyl e direciona o usuário para o cadastro ou login.

Sign Up

Permite que novos usuários criem uma conta.

Login

Permite que usuários existentes acessem suas contas.

Crate Digger

Área principal de descoberta musical.

O usuário pode informar:

Artista
Música
Vibe
Estilo musical

A aplicação utiliza essas informações para buscar recomendações.

Playlist

Exibe a playlist gerada pelo sistema, contendo:

Capa.

Nome da playlist.

Lista de músicas.

Artistas.

Duração.

Opção de salvar.

Opção de descartar e gerar outra playlist.


Library

Exibe todas as playlists salvas pelo usuário.


---

🔐 Segurança e Dados

As informações de sessão utilizadas pelo frontend serão armazenadas através do Web Storage.

Senhas não devem ser armazenadas diretamente no localStorage.

A aplicação deve manter a separação entre os dados de cada usuário, garantindo que um usuário visualize apenas suas próprias playlists.

> A autenticação implementada neste projeto possui finalidade acadêmica e não deve ser considerada um sistema de autenticação seguro para produção.




---

🔄 Fluxo de Utilização

┌──────────────────────┐
│     Landing Page     │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    Cadastro/Login    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     Crate Digger     │
│                      │
│ Artista / Música /   │
│       Vibe           │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     API de Música    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ Playlist Recomendada │
└──────────┬───────────┘
           │
       ┌───┴────┐
       │        │
       ▼        ▼
    Salvar   Descartar
       │        │
       ▼        └──────► Nova busca
┌──────────────────────┐
│       Library        │
└──────────────────────┘


---

🛠️ Status do Projeto

Projeto acadêmico em desenvolvimento.

As funcionalidades e tecnologias poderão ser atualizadas conforme a implementação e os requisitos da disciplina.


---

Link do protótipo: https://stitch.withgoogle.com/projects/4603697728120764018

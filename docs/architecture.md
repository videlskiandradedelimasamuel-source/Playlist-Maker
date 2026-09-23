# 🛠️ Especificação Técnica (Architecture) - Midnight Vinyl

## 1. Visão Geral da Arquitetura

O **Midnight Vinyl** será desenvolvido como uma aplicação web frontend utilizando HTML, CSS e JavaScript.

A aplicação será estruturada de forma modular, separando responsabilidades relacionadas à autenticação, comunicação com APIs, gerenciamento de playlists, armazenamento de sessão e validação de formulários.

A arquitetura será composta por:

```text
┌───────────────────────────────┐
│           Frontend            │
│ HTML + BulmaCSS + JS    │
└───────────────┬───────────────┘
                │
        ┌───────┴────────┐
        │                │
        ▼                ▼
┌───────────────┐  ┌─────────────────┐
│  JSON Server  │  │  API Pública    │
│               │  │    de Música    │
│ Usuários      │  │                 │
│ Playlists     │  │ Artistas        │
└───────────────┘  │ Músicas         │
                   │ Recomendações   │
                   └─────────────────┘


---

2. Tecnologias

2.1 Frontend

HTML5

CSS3

JavaScript

jQuery

Sass / SCSS

MaterializeCSS


2.2 Backend Simulado

JSON Server


O JSON Server será utilizado para disponibilizar uma API REST local para persistência dos dados.

2.3 API Externa

Será utilizada uma API pública relacionada a música para obtenção de dados de artistas e músicas e geração das recomendações.

A API escolhida deverá permitir consultas relacionadas às preferências informadas pelo usuário.

2.4 Ferramentas

Node.js

NPM

Git

GitHub

ESLint

Prettier



---

3. Arquitetura de Camadas

A aplicação será organizada em três principais camadas:

Apresentação

Responsável pela interface e interação com o usuário.

HTML
MaterializeCSS
SCSS
DOM

Aplicação

Responsável pela lógica da aplicação.

JavaScript
jQuery
Validações
Autenticação
Processamento das recomendações
Gerenciamento das playlists

Dados

Responsável pela comunicação com fontes externas.

JSON Server
API Pública de Música
Web Storage


---

4. Modelo de Dados

O sistema possuirá inicialmente duas entidades principais:

USUARIO 1 ─────────── N PLAYLIST

Um usuário pode possuir várias playlists, enquanto cada playlist pertence a apenas um usuário.


---

4.1 Entidade USUARIO

Campo	Tipo	Descrição

id	string	Identificador único do usuário
email	string	E-mail utilizado para login
senha	string	Senha do usuário



---

4.2 Entidade PLAYLIST

Campo	Tipo	Descrição

id	string	Identificador único da playlist
usuarioId	string	ID do usuário proprietário
titulo	string	Nome da playlist
capa	string	URL da imagem da capa
dataCriacao	string	Data de criação
duracao	string	Duração total
musicas	array	Lista de músicas da playlist



---

4.3 Estrutura de uma música

Cada item armazenado dentro de musicas poderá possuir:

Campo	Tipo	Descrição

id	string	Identificador da música
titulo	string	Nome da música
artista	string	Nome do artista
duracao	string	Duração da música
capa	string	URL da capa



---

5. Modelo Entidade-Relacionamento

erDiagram
    USUARIO ||--o{ PLAYLIST : cria

    USUARIO {
        string id PK
        string email
        string senha
    }

    PLAYLIST {
        string id PK
        string usuarioId FK
        string titulo
        string capa
        string dataCriacao
        string duracao
        array musicas
    }


---

6. Estrutura do JSON Server

O arquivo db.json deverá possuir uma estrutura semelhante a:

{
  "usuarios": [
    {
      "id": "1",
      "email": "usuario@email.com",
      "senha": "senha"
    }
  ],
  "playlists": [
    {
      "id": "1",
      "usuarioId": "1",
      "titulo": "Midnight Discoveries",
      "capa": "assets/images/playlist.jpg",
      "dataCriacao": "2026-09-14",
      "duracao": "1h 12min",
      "musicas": [
        {
          "id": "101",
          "titulo": "Exemplo Song",
          "artista": "Example Artist",
          "duracao": "3:42",
          "capa": "https://example.com/cover.jpg"
        }
      ]
    }
  ]
}


---

7. API do JSON Server

Usuários

GET

GET /usuarios

Retorna os usuários cadastrados.

POST

POST /usuarios

Cria um novo usuário.

GET

GET /usuarios/:id

Retorna um usuário específico.


---

Playlists

GET

GET /playlists

Retorna as playlists armazenadas.

GET por usuário

GET /playlists?usuarioId=1

Retorna somente as playlists pertencentes ao usuário.

GET específica

GET /playlists/:id

Retorna uma playlist específica.

POST

POST /playlists

Cria uma nova playlist.

PATCH

PATCH /playlists/:id

Atualiza uma playlist.

DELETE

DELETE /playlists/:id

Exclui uma playlist.


---

8. API Pública de Música

A aplicação utilizará uma API pública para obter informações musicais.

O fluxo de consulta será:

Usuário informa preferência
            ↓
JavaScript recebe o valor
            ↓
Requisição assíncrona
            ↓
API Pública de Música
            ↓
Resposta JSON
            ↓
Processamento dos dados
            ↓
Playlist de recomendações

Os dados retornados pela API deverão ser convertidos para o formato utilizado pela aplicação.

Exemplo:

{
  "id": "123",
  "titulo": "Song Name",
  "artista": "Artist Name",
  "duracao": "3:45",
  "capa": "https://example.com/image.jpg"
}


---

9. Geração das Recomendações

O usuário poderá informar:

Nome de artista.

Nome de música.

Estilo musical.

Vibe ou termo relacionado à música.


Após o envio:

Entrada do usuário
        ↓
Validação
        ↓
Consulta à API
        ↓
Resultados encontrados?
    ↙             ↘
  NÃO              SIM
   ↓                ↓
Mensagem        Processamento
de erro             ↓
                Remoção de
                duplicados
                     ↓
                Seleção das
                recomendações
                     ↓
                  Playlist

A quantidade de músicas retornadas deverá ser limitada para manter a interface organizada.


---

10. Autenticação

A autenticação será implementada de forma simplificada para fins acadêmicos.

Cadastro

Formulário
    ↓
Validação
    ↓
POST /usuarios
    ↓
Usuário criado

Login

E-mail + senha
      ↓
GET /usuarios
      ↓
Comparação das credenciais
      ↓
Usuário encontrado?
   ↙          ↘
 NÃO          SIM
  ↓            ↓
Erro       Criar sessão
               ↓
           localStorage
               ↓
         Página principal


---

11. Web Storage

O localStorage será utilizado para controlar a sessão do usuário.

Exemplo:

localStorage.setItem(
    "usuarioLogado",
    JSON.stringify({
        id: "1",
        email: "usuario@email.com"
    })
);

Para recuperar a sessão:

const usuario = JSON.parse(
    localStorage.getItem("usuarioLogado")
);

A senha não deverá ser armazenada no localStorage.


---

12. Proteção de Rotas

Páginas que dependem de autenticação deverão verificar a existência de uma sessão válida.

Acessar página protegida
          ↓
Existe sessão?
      ↙       ↘
    NÃO        SIM
     ↓          ↓
 Login       Permitir

Exemplos de páginas protegidas:

Crate Digger

Playlist

Library



---

13. Estrutura de Pastas

midnight-vinyl/
│
├── docs/
│   ├── prd.md
│   ├── architecture.md
│   └── design-system.md
│
├── src/
│   ├── css/
│   │   └── main.css
│   │
│   ├── scss/
│   │   ├── abstracts/
│   │   │   ├── _variables.scss
│   │   │   └── _mixins.scss
│   │   │
│   │   ├── components/
│   │   │   ├── _buttons.scss
│   │   │   ├── _cards.scss
│   │   │   ├── _forms.scss
│   │   │   └── _navbar.scss
│   │   │
│   │   ├── pages/
│   │   │   ├── _home.scss
│   │   │   ├── _auth.scss
│   │   │   ├── _crate-digger.scss
│   │   │   ├── _playlist.scss
│   │   │   └── _library.scss
│   │   │
│   │   └── main.scss
│   │
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
│   │   ├── login.html
│   │   ├── signup.html
│   │   ├── crate-digger.html
│   │   ├── playlist.html
│   │   └── library.html
│   │
│   └── assets/
│       ├── images/
│       └── icons/
│
├── db.json
├── routes.json
├── package.json
├── .gitignore
└── README.md


---

14. Organização dos Módulos JavaScript

main.js

Responsável pela inicialização geral da aplicação.

Funções:

Inicialização dos componentes.

Eventos globais.

Verificação da página atual.



---

auth.js

Responsável por:

Cadastro.

Login.

Logout.

Verificação de usuário.

Redirecionamento após autenticação.



---

crate-digger.js

Responsável por:

Capturar a entrada do usuário.

Validar a busca.

Chamar a API pública.

Processar os resultados.

Gerar a playlist.



---

playlist.js

Responsável por:

Renderizar a playlist.

Salvar a playlist.

Descartar a playlist.

Exibir estados de carregamento e erro.



---

library.js

Responsável por:

Buscar playlists do usuário.

Renderizar a Library.

Abrir playlists.

Excluir playlists.



---

api.js

Centraliza as requisições externas.

Exemplos:

buscarMusicas()
buscarArtistas()
buscarRecomendacoes()
buscarPlaylists()
salvarPlaylist()
excluirPlaylist()


---

storage.js

Centraliza operações relacionadas ao Web Storage.

Exemplos:

salvarSessao()
obterSessao()
removerSessao()
usuarioEstaLogado()


---

validation.js

Responsável pelas validações dos formulários.


---

utils.js

Conterá funções auxiliares reutilizáveis.

Exemplos:

formatarDuracao()
formatarData()
removerDuplicados()
redirecionar()


---

15. Sass / SCSS

O Sass será utilizado para organizar os estilos e facilitar a manutenção do Design System.

Estrutura:

scss/
├── abstracts/
├── components/
├── pages/
└── main.scss

As variáveis visuais deverão ser centralizadas.

Exemplo:

$background: #0D0D0D;
$surface: #151515;
$card: #191919;
$primary: #39FF78;
$text-primary: #FFFFFF;
$text-secondary: #8B8B8B;


---

16. Design System

Cores

Nome	Valor	Uso

Background	#0D0D0D	Fundo principal
Surface	#151515	Áreas secundárias
Card	#191919	Cards e componentes
Primary	#39FF78	Botões e destaques
Text Primary	#FFFFFF	Textos principais
Text Secondary	#8B8B8B	Textos secundários


Tipografia

A tipografia deverá priorizar:

Legibilidade.

Hierarquia visual.

Contraste.

Escalabilidade em diferentes tamanhos de tela.


Os títulos deverão possuir maior peso e tamanho, enquanto textos auxiliares utilizarão tamanhos menores e cores secundárias.


---

17. Responsividade

A aplicação seguirá uma abordagem mobile-first.

Serão utilizados:

Flexbox.

CSS Grid.

Media Queries.

Unidades relativas.

Componentes responsivos do MaterializeCSS.

Tipografia fluida.


Estrutura geral:

Mobile
  ↓
Tablet
  ↓
Desktop

Os layouts deverão se adaptar sem perda de funcionalidade.


---

18. Imagens

As imagens utilizadas na aplicação deverão ser otimizadas sempre que possível.

Serão consideradas técnicas como:

WebP.

srcset.

Elemento <picture>.

Lazy loading.

Dimensões responsivas.


Exemplo:

<img
    src="cover.webp"
    srcset="
        cover-small.webp 480w,
        cover-medium.webp 768w,
        cover-large.webp 1200w
    "
    loading="lazy"
    alt="Capa da playlist"
>


---

19. Formulários e Validação

Os formulários deverão utilizar recursos nativos do HTML.

Exemplo:

<input
    type="email"
    name="email"
    required
>

Também poderão ser utilizadas expressões regulares para validações específicas.

Exemplo:

const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

A biblioteca jQuery será utilizada na manipulação dos formulários e um plugin jQuery poderá ser utilizado para complementar a validação.


---

20. Requisições Assíncronas

As requisições deverão ser realizadas de forma assíncrona utilizando JavaScript.

Exemplo:

async function buscarMusicas(termo) {
    try {
        const response = await fetch(url);

        if (!response.ok) {
            throw new Error("Erro ao consultar a API");
        }

        return await response.json();

    } catch (error) {
        console.error(error);
        throw error;
    }
}

A interface deverá apresentar diferentes estados:

Idle
 ↓
Loading
 ↓
Success

Em caso de falha:

Loading
 ↓
Error

Caso nenhum resultado seja encontrado:

Loading
 ↓
Empty


---

21. Tratamento de Erros

A aplicação deverá tratar erros relacionados a:

API indisponível.

Falha de conexão.

Dados inválidos.

Usuário inexistente.

Credenciais incorretas.

Playlist inexistente.

Erro ao salvar.

Erro ao excluir.


As mensagens deverão ser apresentadas de forma clara ao usuário.


---

22. Componentes MaterializeCSS

O MaterializeCSS poderá ser utilizado para componentes como:

Navbar.

Buttons.

Cards.

Inputs.

Forms.

Modal.

Toast.

Grid.

Responsividade.


Os componentes deverão ser adaptados para manter a identidade visual do Midnight Vinyl.


---

23. jQuery

O jQuery será utilizado para manipulação do DOM e eventos.

Exemplo:

$("#search-button").on("click", function () {
    iniciarBusca();
});

Também poderá ser utilizado para integração com plugins jQuery.


---

24. Scripts NPM

O package.json deverá possuir scripts semelhantes a:

{
  "scripts": {
    "json:server": "json-server --watch db.json",
    "sass": "sass --watch src/scss/main.scss:src/css/main.css",
    "lint": "eslint .",
    "format": "prettier --write ."
  }
}


---

25. Git e GitHub

O projeto será versionado utilizando Git.

Sugestão de branches:

main
develop
feature/auth
feature/crate-digger
feature/playlist
feature/library
feature/api
feature/responsive

Commits deverão utilizar mensagens claras e relacionadas à alteração realizada.

Exemplos:

feat: add user registration
feat: implement playlist generation
fix: handle music api errors
style: improve library responsiveness
docs: update architecture


---

26. ESLint e Prettier

O ESLint será utilizado para identificar problemas no código JavaScript.

O Prettier será utilizado para padronizar a formatação dos arquivos.

Objetivos:

Código consistente.

Melhor legibilidade.

Redução de erros.

Padronização entre os arquivos.



---

27. Fluxo Completo da Aplicação

┌──────────────┐
                         │    Usuário   │
                         └──────┬───────┘
                                │
                                ▼
                     ┌────────────────────┐
                     │    Landing Page    │
                     └─────────┬──────────┘
                               │
                         Login / Cadastro
                               │
                               ▼
                     ┌────────────────────┐
                     │   Autenticação     │
                     └─────────┬──────────┘
                               │
                               ▼
                     ┌────────────────────┐
                     │   Crate Digger     │
                     └─────────┬──────────┘
                               │
                               ▼
                     ┌────────────────────┐
                     │ API Pública Música │
                     └─────────┬──────────┘
                               │
                               ▼
                     ┌────────────────────┐
                     │ Recomendações      │
                     └─────────┬──────────┘
                               │
                               ▼
                     ┌────────────────────┐
                     │ Playlist Gerada    │
                     └──────┬───────┬─────┘
                            │       │
                         Salvar  Descartar
                            │       │
                            ▼       └──────► Crate Digger
                     ┌───────────────┐
                     │  JSON Server  │
                     └───────┬───────┘
                             │
                             ▼
                     ┌───────────────┐
                     │    Library    │
                     └───────────────┘


---

28. Segurança

Como se trata de um projeto acadêmico utilizando JSON Server, a autenticação possui finalidade demonstrativa.

Recomendações:

Não armazenar senhas no localStorage.

Não expor chaves de APIs no frontend quando isso não for permitido pelo serviço.

Validar entradas do usuário.

Não confiar exclusivamente em validações realizadas no cliente.

Verificar a propriedade das playlists antes de permitir operações relacionadas a elas.


Em uma aplicação de produção, seria necessário utilizar um backend real com autenticação segura, armazenamento protegido de senhas e controle de autorização.


---

29. Requisitos Técnicos Relacionados aos IDs

ID	Implementação

ID01	Protótipos mobile e desktop
ID02	MaterializeCSS
ID03	Flexbox e CSS Grid
ID04	Componentes MaterializeCSS
ID05	Unidades relativas
ID06	Design System
ID07	Sass/SCSS
ID08	Tipografia responsiva
ID09	Imagens responsivas
ID10	WebP, srcset, picture e lazy loading
ID11	Validação nativa HTML
ID12	Expressões regulares
ID13	Selects e outros elementos de seleção
ID14	localStorage
ID15	Node.js e NPM
ID16	Git, GitHub e .gitignore
ID17	README
ID18	Arquitetura modular
ID19	ESLint e Prettier
ID20	jQuery
ID21	Plugin jQuery
ID22	JSON Server
ID23	Consulta e exibição de dados do JSON Server
ID24	API pública e tratamento de erros



---

30. Conclusão

A arquitetura do Midnight Vinyl foi planejada para separar interface, lógica de aplicação e acesso aos dados.

A utilização de módulos JavaScript, Sass, MaterializeCSS, JSON Server e uma API pública de música permite atender aos requisitos técnicos do projeto enquanto mantém a aplicação organizada e preparada para futuras funcionalidades.

A estrutura também permite que novas funcionalidades sejam adicionadas posteriormente, como compartilhamento de playlists, integração com serviços de streaming e recursos sociais.

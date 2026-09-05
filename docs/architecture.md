architecture.md
🏗️ 1. Especificações Técnicas (Tech Spec) - Midnight Vinyl
Este documento descreve a arquitetura técnica, modelo de dados, tecnologias e organização do código utilizados no desenvolvimento da plataforma Midnight Vinyl.

O sistema será desenvolvido como uma aplicação web responsiva, utilizando HTML5, JavaScript ES6+, Bulma, Sass/SCSS e jQuery, com persistência simulada através de uma API fake, além do consumo de uma API pública de músicas.

2. Arquitetura da Aplicação
A aplicação seguirá uma arquitetura modular baseada em camadas.

┌───────────────────────────────────────────┐
│                INTERFACE                  │
│       HTML + Bulma + SCSS + JS            │
├───────────────────────────────────────────┤
│             COMPONENTES UI                │
│ Navbar | Cards | Forms | Modal | Listas  │
├───────────────────────────────────────────┤
│              SERVICES                     │
│ AuthService | MusicService | PlaylistService│
├───────────────────────────────────────────┤
│              APIs                         │
│ API Fake / JSON Server + API Pública      │
├───────────────────────────────────────────┤
│              PERSISTÊNCIA                 │
│ JSON Server + localStorage/sessionStorage │
└───────────────────────────────────────────┘

Fluxo principal
Usuário
   ↓
Interface HTML
   ↓
Eventos JavaScript / jQuery
   ↓
Validação
   ↓
Service
   ↓
API
   ↓
Tratamento dos dados
   ↓
Renderização dinâmica
   ↓
Interface

3. Tecnologias e Versões
As principais tecnologias utilizadas serão:

HTML5
CSS3
JavaScript ES6+
Bulma
Sass/SCSS
jQuery
jQuery Validation
Node.js
NPM
JSON Server
Figma
Google Stitch
Git/GitHub
ESLint
Prettier
Framework CSS
O framework CSS escolhido será o Bulma, substituindo Bootstrap.

O Bulma será utilizado principalmente para:

grid;
columns;
buttons;
forms;
cards;
navbar;
modal;
responsividade;
helpers de espaçamento e alinhamento.
CSS/SCSS próprio será utilizado para adaptar o Bulma à identidade visual do Midnight Vinyl.

4. Modelo de Dados
O modelo representa os principais objetos manipulados pela aplicação.

erDiagram

    USUARIO {
        string id PK
        string nome
        string email
        string senha
        string criado_em
    }

    REFERENCIA {
        string id PK
        string usuario_id FK
        string tipo
        string valor
    }

    PLAYLIST {
        string id PK
        string usuario_id FK
        string nome
        string descricao
        int quantidade_musicas
        string duracao_total
        string criada_em
    }

    MUSICA {
        string id PK
        string playlist_id FK
        string titulo
        string artista
        string album
        string imagem
        string duracao
        string external_id
    }

    USUARIO ||--o{ REFERENCIA : "informa"
    USUARIO ||--o{ PLAYLIST : "cria"
    PLAYLIST ||--o{ MUSICA : "possui"

5. Dicionário de Dados
👤 Coleção: usuarios
Responsável por armazenar os usuários cadastrados.

id
Identificador único do usuário.

nome
Nome informado durante o cadastro.

email
E-mail utilizado para autenticação.

Deve ser único.

senha
Senha utilizada para autenticação.

A aplicação deverá evitar armazenar a senha em texto puro em uma implementação real. Para fins acadêmicos e da API fake, a estrutura poderá simular a autenticação.

criado_em
Data e horário de criação da conta.

🎵 Coleção: referencias
Armazena as referências fornecidas pelo usuário no Crate Digger.

id
Identificador da referência.

usuario_id
ID do usuário responsável pela referência.

tipo
Tipo da referência:

artista
musica
genero
vibe

valor
Texto informado pelo usuário.

Exemplo:

{
    "tipo": "artista",
    "valor": "The Weeknd"
}

📀 Coleção: playlists
Armazena as playlists geradas e salvas.

id
Identificador único da playlist.

usuario_id
Usuário que criou a playlist.

nome
Nome da playlist.

descricao
Descrição ou contexto da playlist.

quantidade_musicas
Quantidade de músicas existentes.

duracao_total
Duração total das músicas.

criada_em
Data de criação.

🎧 Coleção: musicas
Armazena as músicas pertencentes a cada playlist.

id
Identificador interno.

playlist_id
ID da playlist à qual a música pertence.

titulo
Título da música.

artista
Nome do artista.

album
Álbum relacionado.

imagem
URL da capa do álbum.

duracao
Duração da música.

external_id
Identificador da música retornado pela API pública.

6. Exemplo de db.json
A API fake poderá utilizar uma estrutura semelhante a:

{
  "usuarios": [
    {
      "id": "usr001",
      "nome": "Vinyl User",
      "email": "user@email.com",
      "senha": "********",
      "criado_em": "2026-09-05T20:00:00"
    }
  ],

  "referencias": [
    {
      "id": "ref001",
      "usuario_id": "usr001",
      "tipo": "artista",
      "valor": "The Weeknd"
    }
  ],

  "playlists": [
    {
      "id": "pl001",
      "usuario_id": "usr001",
      "nome": "Late Night Synthwave",
      "descricao": "Curated for late-night listening sessions.",
      "quantidade_musicas": 20,
      "duracao_total": "1h 24min",
      "criada_em": "2026-09-05T20:10:00"
    }
  ],

  "musicas": [
    {
      "id": "mus001",
      "playlist_id": "pl001",
      "titulo": "Blinding Lights",
      "artista": "The Weeknd",
      "album": "After Hours",
      "imagem": "/assets/images/blinding-lights.webp",
      "duracao": "3:20",
      "external_id": "external-001"
    }
  ]
}

7. APIs
7.1 API Fake
O projeto utilizará JSON Server para simular um backend.

Será responsável por:

POST   /usuarios
GET    /usuarios
GET    /usuarios?email=
POST   /referencias
GET    /referencias
POST   /playlists
GET    /playlists
GET    /playlists?usuario_id=
DELETE /playlists/:id
POST   /musicas
GET    /musicas?playlist_id=

Responsabilidades
A API fake será utilizada para atender aos requisitos:

ID 22 – requisições assíncronas para API fake;
ID 23 – exibição de dados obtidos através da API fake.
8. API Pública de Música
O sistema deverá consumir uma API pública real para buscar informações musicais.

A integração será encapsulada dentro de:

services/
└── musicService.js

Exemplo de responsabilidade:

searchMusic(query)

O serviço receberá:

The Weeknd

e retornará informações como:

Título
Artista
Álbum
Imagem
Duração
Identificador externo

Essa integração atende ao:

ID 24 – Realiza requisições assíncronas para APIs públicas reais.

9. Geração da Playlist
A geração da playlist será realizada pelo playlistService.

Fluxo:

Usuário informa referências
        ↓
Validação
        ↓
MusicService
        ↓
API pública
        ↓
Resultados encontrados
        ↓
Filtro de músicas
        ↓
Remoção de duplicadas
        ↓
Montagem da playlist
        ↓
Renderização

A primeira versão não utilizará Machine Learning.

A similaridade poderá ser simulada através de:

artista relacionado;
gênero;
termos de busca;
referências fornecidas;
resultados retornados pela API.
Isso mantém o projeto dentro do escopo acadêmico sem exigir implementação de um sistema complexo de recomendação.

10. Estrutura de Diretórios
A aplicação deverá ser organizada de maneira modular.

midnight-vinyl/
│
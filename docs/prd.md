# 📄 Product Requirements Document (PRD) - Midnight Vinyl

## 1. Visão Geral e Objetivo

O **Midnight Vinyl** é uma aplicação web de criação e descoberta de playlists personalizadas.

O objetivo da aplicação é permitir que usuários criem uma conta, informem artistas, músicas ou estilos musicais de seu interesse e recebam uma playlist com recomendações relacionadas às suas preferências.

A aplicação utiliza uma API pública de música para obter informações sobre artistas e músicas. As playlists criadas podem ser salvas e posteriormente acessadas através da página **Library**.

O projeto tem como foco a aplicação prática de conceitos de desenvolvimento web, responsividade, formulários, JavaScript, bibliotecas, consumo de APIs e persistência de dados.

---

## 2. Atores do Sistema

### 2.1 Visitante

Usuário que acessa a aplicação sem estar autenticado.

Pode:

- Visualizar a Landing Page.
- Conhecer a proposta do Midnight Vinyl.
- Criar uma conta.
- Realizar login.

Não pode:

- Criar playlists.
- Salvar playlists.
- Acessar a Library.

### 2.2 Usuário

Usuário autenticado na aplicação.

Pode:

- Acessar o Crate Digger.
- Informar artistas, músicas ou estilos musicais.
- Gerar playlists.
- Visualizar playlists geradas.
- Salvar playlists.
- Acessar suas playlists salvas na Library.
- Excluir playlists.

### 2.3 API Pública de Música

Serviço externo utilizado para:

- Pesquisar artistas.
- Pesquisar músicas.
- Obter informações relacionadas a artistas e músicas.
- Fornecer dados utilizados na geração das recomendações.

### 2.4 JSON Server

API local utilizada para persistir os dados da aplicação.

Responsável por armazenar:

- Usuários.
- Playlists.

---

## 3. Histórias de Usuário e Escopo

## Épico 1 — Cadastro e Autenticação

### US01 — Criar conta

**Como** visitante,

**quero** criar uma conta utilizando meu e-mail e senha,

**para** poder utilizar os recursos de criação e armazenamento de playlists.

#### Critérios de Aceitação

- O usuário deve informar um e-mail.
- O usuário deve informar uma senha.
- Os campos devem possuir validação.
- O e-mail deve possuir formato válido.
- O cadastro não deve permitir campos vazios.
- O usuário deve receber uma indicação de sucesso ou erro.
- O usuário cadastrado deve ser armazenado no JSON Server.

---

### US02 — Realizar login

**Como** usuário cadastrado,

**quero** realizar login,

**para** acessar minhas playlists e utilizar o Crate Digger.

#### Critérios de Aceitação

- O usuário deve informar e-mail e senha.
- Os dados devem ser comparados com os usuários cadastrados.
- Credenciais inválidas devem gerar uma mensagem de erro.
- Um login válido deve criar uma sessão.
- A sessão deve ser armazenada utilizando Web Storage.
- Após o login, o usuário deve ser direcionado para a área principal da aplicação.

---

### US03 — Realizar logout

**Como** usuário autenticado,

**quero** sair da minha conta,

**para** encerrar minha sessão.

#### Critérios de Aceitação

- O usuário deve possuir uma opção de logout.
- A sessão armazenada no Web Storage deve ser removida.
- O usuário deve ser redirecionado para uma página pública.

---

## Épico 2 — Crate Digger

### US04 — Informar preferências musicais

**Como** usuário,

**quero** informar artistas, músicas ou estilos musicais que gosto,

**para** receber recomendações relacionadas aos meus interesses.

#### Critérios de Aceitação

- O usuário deve possuir um campo para inserir sua preferência.
- O campo não pode ser enviado vazio.
- O sistema deve aceitar artistas, músicas e estilos.
- O usuário deve poder iniciar a busca através do botão ou tecla Enter.
- O sistema deve apresentar um estado de carregamento durante a busca.

---

### US05 — Pesquisar informações musicais

**Como** usuário,

**quero** pesquisar minhas preferências musicais,

**para** encontrar músicas e artistas relacionados.

#### Critérios de Aceitação

- A aplicação deve realizar uma requisição assíncrona para uma API pública.
- A pesquisa deve utilizar o conteúdo informado pelo usuário.
- Os dados retornados devem ser processados pelo JavaScript.
- Erros de comunicação devem ser tratados.
- Caso nenhum resultado seja encontrado, o sistema deve informar o usuário.

---

### US06 — Gerar playlist

**Como** usuário,

**quero** receber uma playlist baseada nas minhas preferências,

**para** descobrir novas músicas.

#### Critérios de Aceitação

- O sistema deve utilizar os resultados da API pública.
- A playlist deve possuir múltiplas músicas.
- Cada música deve apresentar pelo menos título e artista.
- Quando disponível, devem ser exibidas informações como duração e capa.
- A playlist não deve conter músicas duplicadas.
- O usuário deve ser direcionado para a tela de resultado.

---

## Épico 3 — Playlist

### US07 — Visualizar playlist gerada

**Como** usuário,

**quero** visualizar as músicas recomendadas,

**para** decidir se quero salvar a playlist.

#### Critérios de Aceitação

- A tela deve apresentar o nome da playlist.
- A tela deve apresentar a capa.
- As músicas devem ser exibidas em uma lista.
- O artista deve ser exibido junto à música.
- A duração deve ser exibida quando disponível.
- Deve existir uma opção para salvar a playlist.
- Deve existir uma opção para descartar a playlist.

---

### US08 — Salvar playlist

**Como** usuário,

**quero** salvar uma playlist gerada,

**para** acessá-la posteriormente.

#### Critérios de Aceitação

- O usuário deve estar autenticado.
- A playlist deve ser enviada ao JSON Server.
- A playlist deve possuir identificação própria.
- A playlist deve ser associada ao usuário que a criou.
- O sistema deve informar o resultado da operação.

---

### US09 — Descartar playlist

**Como** usuário,

**quero** descartar uma playlist gerada,

**para** realizar uma nova busca.

#### Critérios de Aceitação

- A playlist atual não deve ser salva.
- O usuário deve poder retornar ao Crate Digger.
- Os dados da busca anterior não devem impedir uma nova busca.

---

## Épico 4 — Library

### US10 — Visualizar playlists salvas

**Como** usuário,

**quero** visualizar minhas playlists salvas,

**para** encontrar playlists que criei anteriormente.

#### Critérios de Aceitação

- A Library deve exibir apenas playlists pertencentes ao usuário autenticado.
- As playlists devem ser obtidas através do JSON Server.
- Cada playlist deve apresentar informações básicas.
- Caso o usuário não possua playlists, deve ser exibida uma mensagem apropriada.

---

### US11 — Abrir uma playlist

**Como** usuário,

**quero** abrir uma playlist salva,

**para** visualizar suas músicas novamente.

#### Critérios de Aceitação

- O usuário deve conseguir selecionar uma playlist.
- Os dados devem ser carregados do JSON Server.
- As músicas pertencentes à playlist devem ser exibidas.

---

### US12 — Excluir playlist

**Como** usuário,

**quero** excluir uma playlist salva,

**para** remover playlists que não desejo mais manter.

#### Critérios de Aceitação

- O usuário deve conseguir iniciar a exclusão.
- O sistema deve solicitar confirmação.
- A playlist deve ser removida do JSON Server.
- A Library deve ser atualizada após a exclusão.

---

## Épico 5 — Interface e Responsividade

### US13 — Utilizar a aplicação em diferentes dispositivos

**Como** usuário,

**quero** utilizar o Midnight Vinyl em computadores e dispositivos móveis,

**para** acessar minhas playlists independentemente do tamanho da tela.

#### Critérios de Aceitação

- A aplicação deve possuir layout responsivo.
- As páginas devem funcionar em telas pequenas e grandes.
- Os componentes devem se adaptar ao espaço disponível.
- Os textos devem permanecer legíveis.
- Os elementos interativos devem possuir tamanho adequado para dispositivos móveis.

---

# 4. Regras de Negócio

### RN01 — Autenticação

Somente usuários autenticados podem criar e salvar playlists.

### RN02 — Identificação do usuário

Cada usuário deve possuir um identificador único.

### RN03 — Associação de playlists

Toda playlist salva deve estar associada ao usuário que a criou.

### RN04 — Privacidade das playlists

Um usuário não deve visualizar playlists pertencentes a outro usuário através da Library.

### RN05 — Busca obrigatória

Não deve ser possível iniciar uma busca sem informar uma preferência musical.

### RN06 — Recomendações

As músicas recomendadas devem ser baseadas nas informações fornecidas pelo usuário.

### RN07 — Músicas duplicadas

Uma playlist não deve possuir a mesma música mais de uma vez.

### RN08 — Falha da API

Caso a API pública esteja indisponível ou retorne um erro, a aplicação deve informar o usuário e evitar o carregamento de dados inválidos.

### RN09 — Sessão

A sessão do usuário deve ser controlada através do Web Storage.

### RN10 — Exclusão

Quando uma playlist for excluída, ela não deve mais aparecer na Library do usuário.

---

# 5. Requisitos Funcionais

### RF01

O sistema deve permitir o cadastro de usuários.

### RF02

O sistema deve permitir login e logout.

### RF03

O sistema deve validar os dados dos formulários.

### RF04

O sistema deve armazenar os usuários através do JSON Server.

### RF05

O sistema deve permitir a inserção de artistas, músicas ou estilos musicais.

### RF06

O sistema deve realizar requisições assíncronas para uma API pública de música.

### RF07

O sistema deve processar os resultados recebidos da API.

### RF08

O sistema deve gerar uma playlist baseada nos resultados obtidos.

### RF09

O sistema deve permitir salvar uma playlist.

### RF10

O sistema deve permitir consultar playlists anteriormente salvas.

### RF11

O sistema deve permitir excluir playlists.

### RF12

O sistema deve apresentar mensagens de carregamento, sucesso, vazio e erro.

---

# 6. Requisitos Não Funcionais

### RNF01 — Responsividade

A aplicação deve funcionar adequadamente em dispositivos móveis, tablets e desktops.

### RNF02 — Usabilidade

A interface deve possuir navegação simples e consistente.

### RNF03 — Performance

As requisições à API devem ser realizadas de forma assíncrona para evitar o bloqueio da interface.

### RNF04 — Manutenibilidade

O código JavaScript deve ser dividido em módulos de acordo com suas responsabilidades.

### RNF05 — Compatibilidade

A aplicação deve funcionar nos principais navegadores modernos.

### RNF06 — Identidade visual

Todas as telas devem seguir o Design System definido para o Midnight Vinyl.

---

# 7. Escopo do MVP

O MVP do Midnight Vinyl será composto pelas seguintes funcionalidades:

- Cadastro.
- Login.
- Logout.
- Crate Digger.
- Pesquisa através de API pública.
- Geração de playlist.
- Visualização da playlist.
- Salvamento da playlist.
- Library.
- Visualização de playlists salvas.
- Exclusão de playlists.
- Layout responsivo.
- Persistência através do JSON Server.

---

# 8. Fora do Escopo do MVP

Não fazem parte do escopo inicial:

- Sistema social entre usuários.
- Compartilhamento público de playlists.
- Sistema de seguidores.
- Comentários.
- Curtidas.
- Algoritmo próprio de recomendação baseado em Machine Learning.
- Streaming de músicas.
- Sistema de pagamentos.
- Integração obrigatória com serviços de streaming.

A opção **"Save to Spotify"** presente na interface poderá ser implementada posteriormente como uma funcionalidade adicional, caso seja necessária uma integração real com a plataforma e seu sistema de autenticação.

---

# 9. Fluxo Principal

```text
1. Usuário acessa a Landing Page
              ↓
2. Usuário cria uma conta ou realiza login
              ↓
3. Usuário acessa o Crate Digger
              ↓
4. Usuário informa artista, música ou vibe
              ↓
5. Aplicação consulta a API pública
              ↓
6. Sistema processa os resultados
              ↓
7. Playlist é gerada
              ↓
8. Usuário visualiza a playlist
              ↓
        ┌─────┴─────┐
        ↓           ↓
      Salvar      Descartar
        ↓           ↓
     Library    Nova busca


---

10. Critérios Gerais de Aceitação

O projeto será considerado funcional quando:

Um visitante conseguir criar uma conta.

Um usuário conseguir realizar login.

O usuário conseguir informar uma preferência musical.

A aplicação conseguir consultar uma API pública.

A aplicação conseguir gerar uma playlist.

O usuário conseguir salvar a playlist.

A playlist salva aparecer na Library.

O usuário conseguir abrir e excluir suas playlists.

A aplicação tratar erros de requisição.

A aplicação funcionar de forma responsiva.

Os dados persistidos pelo JSON Server permanecerem disponíveis após o encerramento da aplicação.
Objetivos principais
Permitir que visitantes conheçam a proposta do Midnight Vinyl.
Permitir criação e autenticação de usuários.
Permitir que usuários informem artistas e músicas de referência.
Gerar playlists personalizadas a partir dessas referências.
Exibir músicas, artistas, duração e demais informações da playlist.
Permitir salvar playlists criadas.
Permitir visualizar playlists anteriormente criadas.
Consumir APIs públicas relacionadas a músicas e artistas.
Utilizar uma API fake para persistência e simulação do backend.
Criar uma interface responsiva para desktop e dispositivos móveis.
2. Atores do Sistema
🎧 Visitante
Usuário não autenticado que acessa o Midnight Vinyl.

Pode:

visualizar a página inicial;
conhecer a proposta da plataforma;
visualizar informações sobre o Crate Digger;
acessar as páginas de cadastro e login.
Não pode:

gerar playlists personalizadas;
salvar playlists;
acessar sua biblioteca de playlists.
👤 Usuário cadastrado
Usuário que possui uma conta no Midnight Vinyl.

Pode:

realizar login;
utilizar o Crate Digger;
informar artistas e músicas;
gerar playlists;
visualizar recomendações;
salvar playlists;
visualizar suas playlists salvas;
excluir playlists salvas.
🎵 Crate Digger
Funcionalidade principal da plataforma responsável por receber referências musicais fornecidas pelo usuário e gerar recomendações.

O usuário poderá informar:

nome de artista;
nome de música;
gênero;
estilo;
referência musical.
O sistema utilizará os dados informados para buscar e montar uma seleção de músicas relacionadas.

🗄️ Sistema
Responsável por:

autenticar usuários;
validar formulários;
consultar APIs;
processar as referências musicais;
gerar playlists;
persistir dados;
recuperar playlists;
exibir mensagens de erro e sucesso.
3. Histórias de Usuário e Escopo
🎼 Épico 1: Apresentação da Plataforma
US01 – Apresentação do Midnight Vinyl
Como um visitante, quero visualizar a página inicial do Midnight Vinyl, para entender rapidamente a proposta da plataforma e descobrir como ela pode me ajudar a encontrar novas músicas.

Critérios de Aceitação:

 A página deve apresentar o nome Midnight Vinyl.
 Deve existir uma seção explicando o conceito do Crate Digger.
 Deve existir uma chamada principal para criação de conta.
 A página deve apresentar visual dark consistente com a identidade do projeto.
 A página deve possuir navegação para as principais áreas do sistema.
 A página deve funcionar em desktop e mobile.
US02 – Acesso às funcionalidades
Como um visitante, quero visualizar as principais funcionalidades da plataforma, para decidir se desejo criar uma conta.

Critérios de Aceitação:

 A landing page deve apresentar o Crate Digger.
 Deve apresentar a funcionalidade de Sonic Profiling.
 Deve apresentar a proposta do Masterplate.
 Deve existir CTA para cadastro.
 Os elementos devem possuir comportamento responsivo.
🔐 Épico 2: Cadastro e Autenticação
US03 – Cadastro de usuário
Como um visitante, quero criar uma conta utilizando meu nome, e-mail e senha, para acessar as funcionalidades personalizadas do Midnight Vinyl.

Critérios de Aceitação:

 Nome deve ser obrigatório.
 E-mail deve ser obrigatório.
 O e-mail deve possuir formato válido.
 Senha deve ser obrigatória.
 A senha deve possuir no mínimo 8 caracteres.
 O formulário deve apresentar mensagens de erro.
 O formulário deve apresentar mensagem de sucesso após cadastro.
 O usuário cadastrado deve ser persistido na API fake.
US04 – Validação do cadastro
Como um usuário, quero receber mensagens claras quando preencher meus dados incorretamente, para corrigir os campos antes de criar minha conta.

Critérios de Aceitação:

 Campos obrigatórios devem ser identificados.
 E-mails inválidos devem ser rejeitados.
 Senhas menores que 8 caracteres devem ser rejeitadas.
 O sistema deve verificar se o e-mail já está cadastrado.
 Validações customizadas devem utilizar REGEX quando necessário.
 As mensagens devem ser exibidas próximas aos campos.
US05 – Login
Como um usuário cadastrado, quero informar meu e-mail e senha, para acessar minha conta.

Critérios de Aceitação:

 E-mail deve ser obrigatório.
 Senha deve ser obrigatória.
 O sistema deve verificar os dados cadastrados.
 Login inválido deve apresentar mensagem de erro.
 Login válido deve direcionar o usuário para o Crate Digger.
 A sessão do usuário deve ser armazenada utilizando sessionStorage ou localStorage.
US06 – Encerramento da sessão
Como um usuário autenticado, quero sair da minha conta, para impedir que outras pessoas utilizem minha sessão.

Critérios de Aceitação:

 Deve existir uma opção de logout.
 Os dados da sessão devem ser removidos do Web Storage.
 O usuário deve ser redirecionado para uma página pública.
🔎 Épico 3: Crate Digger
US07 – Inserção de referências musicais
Como um usuário autenticado, quero informar artistas, músicas ou estilos que gosto, para receber recomendações relacionadas.

Critérios de Aceitação:

 Deve existir um campo de entrada para referências.
 O usuário deve poder adicionar mais de uma referência.
 O campo deve aceitar artistas.
 O campo deve aceitar músicas.
 O campo deve aceitar estilos ou gêneros.
 O usuário deve poder remover referências adicionadas.
 Deve existir um botão para iniciar a busca.
US08 – Busca de referências musicais
Como um usuário, quero que o sistema pesquise minhas referências musicais, para encontrar informações sobre artistas e músicas relacionadas.

Critérios de Aceitação:

 O sistema deve realizar requisições assíncronas.
 Os dados devem ser obtidos de uma API pública de música.
 O sistema deve tratar respostas vazias.
 O sistema deve tratar erros de conexão.
 Deve existir indicação visual durante o carregamento.
US09 – Geração da playlist
Como um usuário, quero receber uma playlist baseada nas minhas referências, para descobrir músicas semelhantes às que já gosto.

Critérios de Aceitação:

 A playlist deve possuir um nome.
 Deve possuir uma lista de músicas.
 Cada música deve apresentar título e artista.
 Quando disponível, deve apresentar duração.
 O resultado deve ser apresentado em formato de lista.
 O sistema deve impedir a geração quando nenhuma referência for informada.
 O usuário deve receber uma mensagem caso não existam recomendações.
🎚️ Épico 4: Resultado e Masterplate
US10 – Visualização da playlist
Como um usuário, quero visualizar as músicas recomendadas em uma interface organizada, para analisar minha nova playlist.

Critérios de Aceitação:

 A playlist deve apresentar suas músicas numeradas.
 Deve apresentar título.
 Deve apresentar artista.
 Deve apresentar duração quando disponível.
 Deve apresentar a quantidade total de músicas.
 Deve apresentar a duração total.
 A interface deve ser responsiva.
US11 – Salvar playlist
Como um usuário, quero salvar uma playlist gerada, para poder acessá-la novamente posteriormente.

Critérios de Aceitação:

 Deve existir um botão "Salvar Playlist".
 A playlist deve ser vinculada ao usuário autenticado.
 O sistema deve persistir a playlist na API fake.
 O usuário deve receber confirmação após salvar.
 Uma mesma playlist não deve ser salva acidentalmente várias vezes.
US12 – Descartar playlist
Como um usuário, quero descartar uma playlist que não gostei, para poder iniciar uma nova busca.

Critérios de Aceitação:

 Deve existir uma opção para descartar a playlist.
 A playlist descartada não deve ser adicionada à biblioteca.
 O usuário deve poder retornar ao Crate Digger.
📚 Épico 5: Biblioteca de Playlists
US13 – Visualizar playlists criadas
Como um usuário, quero visualizar todas as playlists que salvei, para acessar novamente minhas descobertas musicais.

Critérios de Aceitação:

 Deve existir uma página de biblioteca.
 Apenas playlists pertencentes ao usuário devem ser exibidas.
 As playlists devem ser apresentadas em cards ou lista.
 Cada playlist deve apresentar nome.
 Deve apresentar quantidade de músicas.
 Deve apresentar duração.
 Deve existir uma ação para abrir a playlist.
US14 – Visualizar playlist salva
Como um usuário, quero abrir uma playlist salva, para visualizar novamente suas músicas.

Critérios de Aceitação:

 A playlist deve apresentar suas músicas.
 Deve apresentar artista e título.
 Deve apresentar duração quando disponível.
 Deve existir uma opção para retornar à biblioteca.
US15 – Excluir playlist
Como um usuário, quero excluir uma playlist salva, para manter minha biblioteca organizada.

Critérios de Aceitação:

 Deve existir uma ação de exclusão.
 O sistema deve solicitar confirmação antes da exclusão.
 A playlist deve ser removida da API fake.
 A biblioteca deve ser atualizada após a exclusão.
🌐 Épico 6: Integração com APIs
US16 – Consumo de API pública
Como usuário, quero que o Midnight Vinyl utilize informações reais sobre músicas e artistas, para receber recomendações mais relevantes.

Critérios de Aceitação:

 O sistema deve consumir pelo menos uma API pública real.
 A requisição deve ser realizada de forma assíncrona.
 Os dados retornados devem ser manipulados pelo JavaScript.
 Erros da API devem ser tratados.
 Resultados devem ser apresentados dinamicamente na interface.
US17 – Persistência através de API fake
Como usuário, quero que minhas playlists sejam armazenadas, para poder acessá-las posteriormente.

Critérios de Aceitação:

 O sistema deve utilizar uma API fake, como JSON Server.
 Usuários devem ser persistidos.
 Playlists devem ser persistidas.
 Deve ser possível consultar playlists.
 Deve ser possível excluir playlists.
 As operações devem utilizar requisições assíncronas.
🎨 Épico 7: Interface e Responsividade
US18 – Interface responsiva
Como usuário, quero utilizar o Midnight Vinyl em diferentes tamanhos de tela, para acessar a plataforma pelo computador ou celular.

Critérios de Aceitação:

 A aplicação deve possuir layout desktop.
 A aplicação deve possuir layout mobile.
 Os componentes devem se adaptar à largura da tela.
 Cards devem reorganizar seu conteúdo.
 Imagens devem se adaptar ao container.
 A navegação deve funcionar em telas pequenas.
US19 – Design System
Como usuário, quero encontrar uma interface visualmente consistente em todas as páginas, para ter uma experiência de navegação coesa.

Critérios de Aceitação:

 A aplicação deve utilizar uma paleta consistente.
 A cor verde neon deve representar ações principais.
 A interface deve utilizar tema predominantemente escuro.
 Botões devem seguir padrões visuais consistentes.
 Inputs devem seguir o mesmo padrão.
 Cards devem possuir padrão visual reutilizável.
 A tipografia deve ser consistente.
4. Requisitos Não Funcionais
RNF01 – Responsividade
A aplicação deve funcionar em:

dispositivos mobile;
tablets;
desktops.
RNF02 – Performance
As imagens devem ser otimizadas utilizando formatos modernos, preferencialmente WebP, além de técnicas como picture, srcset e object-fit.

RNF03 – Usabilidade
A interface deve fornecer feedback visual para:

carregamento;
sucesso;
erro;
validação;
operações de salvamento;
exclusão.
RNF04 – Manutenibilidade
O projeto deve possuir estrutura modular, separando:

páginas;
componentes;
estilos;
scripts;
serviços;
dados;
validações.
RNF05 – Padronização
O projeto deverá utilizar:

ESLint;
Prettier;
Git;
.gitignore;
README.md.
RNF06 – Framework CSS
A estilização da aplicação deverá utilizar Bulma, complementada por CSS/SCSS próprio quando necessário.

5. Escopo do Projeto
Dentro do escopo
Landing Page.
Cadastro.
Login.
Logout.
Crate Digger.
Busca de músicas/artistas.
Geração de playlist.
Visualização da playlist.
Salvamento de playlist.
Biblioteca de playlists.
Exclusão de playlist.
API fake.
API pública de música.
Web Storage.
Validação de formulários.
Responsividade.
Design System.
Fora do escopo inicial
Streaming das músicas.
Hospedagem de arquivos de áudio.
Sistema de assinatura paga.
Aplicativo mobile nativo.
Algoritmo de recomendação baseado em Machine Learning.
Integração obrigatória com conta Spotify para reprodução.

prd.md
Documentação do Projeto: Midnight Vinyl
1. Visão Geral e Objetivo
O Midnight Vinyl é uma plataforma web de criação e descoberta de playlists musicais. O objetivo é proporcionar uma experiência de curadoria musical voltada para usuários que desejam descobrir novas músicas e artistas a partir de seus próprios gostos musicais.

O usuário poderá criar uma conta, informar artistas, músicas, estilos ou referências musicais que gosta e utilizar o Crate Digger para gerar uma playlist personalizada com músicas e artistas semelhantes.

A plataforma também permitirá que o usuário visualize as playlists geradas, salve suas favoritas e posteriormente consulte seu histórico de playlists através de uma área dedicada à sua biblioteca.

A proposta visual do Midnight Vinyl utiliza uma estética dark, minimalista e inspirada em estúdios musicais, com destaque para a cor verde neon, tipografia moderna, cards, imagens relacionadas à produção musical e uma interface focada na experiência de descoberta.

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
---
layout: post
title:  "Twitter"
categories: poo
exclude: true
---

![](/assets/03_twitter/figura.png)

Vamos implementar o modelo do twitter. Os usuários se cadastram e podem seguir outros usuários do sistema. Ao twittar, a mensagem vai para timeline de todas as pessoas que a seguem.

## Habilidades

- Nessa atividade o mesmo objeto usuário estará armazenado no manager de usuários, como também nas listas de seguidores e seguidos do próprio usuário. 
- Também o objeto twitter estará tanto na lista de minhasMensagens do usuário que postou como na timeline de seus seguidores. Dado que é o mesmo objeto mensagem, ao alterar seu twitter original, todos os seguidores verão a mensagem alterada. 
- Cada objeto Twitter ganha um id único através de uma variável estática nextTwId na class User. 
- Também User utiliza um contador de mensagem não lidas para mostrar apenas as novas mensagens.

## Funcionalidades
- **[2.0 P]** Parte 1 
    - Adicionar usuário passando username.
    - Mostrar os usuários cadastrados.

```
addUser goku
addUser sara
addUser tina
showUsers
  [ goku luis tina ]
```
---
- **[2.0 P]** Parte 2
    - Seguir um outro usuário cadastrado
    - Mostrar a lista de seguidores
    - Mostrar a lista de seguidos

```
seguir goku luis
seguir goku tina
seguir sara tina
seguidos goku
  [ sara tina ]
seguidores tina
  [ goku sara ]
seguidores goku
  [ ]
```
---
- **[4.0 P]** Parte 3
    - twittar uma mensagem com várias palavras
    - mostrar a timeline
    - mostrar suas próprias mensagens

```
twittar sara hoje estou triste
twittar tina ganhei chocolate
twittar sara partiu ru!
twittar tina chocolate

timeline goku
  timeline goku
  3 tina: chocolate ruim
  2 sara: partiu ru!
  1 tina: ganhei chocolate
  0 sara: hoje estou triste

timeline sara
  timeline sara
  3 tina: chocolate ruim
  1 tina: ganhei chocolate
  
myMsgs sara
  myMsgs sara
  2 sara: partiu ru!
  0 sara: hoje estou triste
```
---
- **[1.0 P]** Parte 4
  - Mostrar apenas as mensagens não lidas
  - Alterar o texto de uma mensagem que já foi twittada

```
unread sara
  unread sara

twittar tina eu
twittar tina amo
twittar tina chocolate

unread sara
  unread sara
  6 tina: chocolate
  5 tina: amo
  4 tina: eu

unread sara
  unread sara
```
---
- **[1.0 P]** Parte 5
    - Editar uma mensagem que já foi publicada

```
editar tina 5 odeio muito

timeline sara
  timeline sara
  6 tina: chocolate
  5 tina: odeio muito
  4 tina: eu
  3 tina: chocolate ruim
  1 tina: ganhei chocolate
```

## Orientações
- Classe Twitter
    - É uma classe que vai guardar as mensagens postadas pelos usuários. Crie o construtor e o método toString mostrando todos os atributos da classe. 
    - Observe que apenas temos o método setMsg, pois será o único atribuito sujeito a modificações após a criação do twitter.
- Classe User
    - Aqui acontece toda a mágica.
    - Crie um atributo static nextTwId iniciado em 0. Cada novo twitter criado deve receber um novo id. Incremente a variável para cada id criado.
    - Para seguir, adicione o outro usuário na sua lista de seguidos e se adicione na lista de seguidores do User other. Passe o this como parâmetro para se adicionar à lista de seguidores do other.
    - No método twitter, adicione o objeto twitter criado na sua lista de myMsgs. O mesmo objeto adicione na timeline de cada um dos seus seguidores.
    - Quando for adicionar os twitter tanto na sua lista de mensagens, quanto na timeline dos seus seguidores adicione na frente da lista. A estrutura ideal para guardar esses objetos é uma lista ligada. No typescript use o médodo unshift da lista. No c++ utilize o push_front de list. Em java utilize o addFirst do LinkedList.
    - Como é o mesmo objeto compartilhado entre as listas, ao alterar o texto no objeto do emissor, todos as outras referências também estarão apontando para o objeto alterado.
    - Sempre que twittar uma mensagem, incremente o contador de mensagens não lidas do seguidor. Assim, ele saberá quantas mensagens novas deve mostrar. Ao mostrar as mensagens novas, zere o contador unreadCount.
    - Adicione todos os métodos get apresentados no diagrama.
- Classe Manager
    - O manager aqui é bem básico. 
    - Sugiro que lance excessões caso o get não encontre um user com esse username.

## Diagrama de Classes
- Gets, Sets e toString omitidos.

![](/assets/03_twitter/diagrama.png)
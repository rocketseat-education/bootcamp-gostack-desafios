<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios.png" />

<h3 align="center">
  Desafio 02: Conceitos do NodeJS
</h3>

<p align="center">“Não espere para plantar, apenas tenha paciência para colher”!</blockquote>

<p align="center">
  <img alt="GitHub language count" src="https://img.shields.io/github/languages/count/rocketseat/bootcamp-gostack-desafios?color=%2304D361">

  <a href="https://rocketseat.com.br">
    <img alt="Made by Rocketseat" src="https://img.shields.io/badge/made%20by-Rocketseat-%2304D361">
  </a>

  <img alt="License" src="https://img.shields.io/badge/license-MIT-%2304D361">

  <a href="https://github.com/Rocketseat/bootcamp-gostack-desafios/stargazers">
    <img alt="Stargazers" src="https://img.shields.io/github/stars/rocketseat/bootcamp-gostack-desafios?style=social">
  </a>
</p>

<p align="center">
  <a href="#rocket-sobre-o-desafio">Sobre o desafio</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#calendar-entrega">Entrega</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-licença">Licença</a>
</p>

## :rocket: Sobre o desafio

Nesse desafio, você deve criar uma aplicação para treinar o que você aprendeu até agora no NodeJS!

Essa será uma aplicação para armazenar repositórios do github, que irá permitir a criação, listagem, atualização e remoção dos repositórios, e além disso permitir que os repositórios possam receber "likes".

### Template da aplicação

Para te ajudar nesse desafio, criamos para você um modelo que você pode clonar através do npm.js.

O Template pode ser clonado utilizando o comando `comando aqui`.

Agora navegue até a pasta criada e abre no VSCODE, e você terá algo parecido com isso:

<p align="center">
  <img  src="./assets/nodejs-example.png">
</p>

### Rotas da aplicação

Agora que você já está com o template clonado, e pronto para continuar, você deve abrir o arquivo app.js, e completar onde não possui código com o código para atingir os objetivos de cada rota.

- **`POST /repositories`**: A rota deve receber `title`, `url` e `techs` dentro do corpo da requisição, sendo a URL o link para o github desse repositório. Ao cadastrar um novo projeto, ele deve ser armazenado dentro de um objeto no seguinte formato: `{ id: "uuid", title: 'Desafio NodeJS', techs: ["NodeJS", "..."], likes: 0 }`; Certifique-se que o ID seja um UUID, e de sempre iniciar os likes como 0.

- **`GET /repositories`**: Rota que lista todos os repositórios;

- **`PUT /repositories/:id`**: A rota deve alterar apenas o `título`, a `url` e as `techs` do repositório que possua o `id` igual ao `id` presente nos parâmetros da rota;

- **`DELETE /repositories/:id`**: A rota deve deletar o repositório com o `id` presente nos parâmetros da rota;

- **`POST /repositories/:id/like`**: A rota deve aumentar o número de likes do repositório específico escolhido através do `id` presente nos parâmetros da rota, a cada chamada dessa rota, o número de likes deve ser aumentado em 1;

### Testes automatizados

Para te ajudar a saber se você está no caminho certo, no projeto que você já clonou deixamos alguns testes automatizados.

Os testes sempre vão ficar dentro de uma pasta chamada `__tests__` dentro da pasta `src`.

Dentro da pasta de testes, para cada arquivo testado na sua aplicação, existe um arquivo com o mesmo nome, com a extensão `.spec.js`.

Para começar a utilizar os testes, execute o comando `yarn test` no seu terminal, e ele irá te retornar o resultado dos testes das rotas.

Isso deve te retornar vários erros logo após clonar o projeto, como esse:

<p align="center">
  <img src="./assets/tests-example.png">
</p>

Esse erro significa que a princípio o teste não recebeu nenhum retorno das rotas, então é agora que é a hora de codar, experimente ir adicionando seus códigos para cumprir os requisitos do desafio. :rocket:

**Dica 1**: Nem sempre você precisa usar apenas os testes para saber se tudo está funcionando, você pode sempre executar o `yarn dev` e testar sua aplicação utilizando o insomnia caso prefira.

**Dica 2**: Esses testes serão os mesmos testes que irão corrigir seu desafio e dará sua nota, então recomendamos que os siga a risca e tenha certeza que todos passem para receber nota máxima!

### Entendendo os erros dos testes

Agora que você já sabe como rodar os testes, você também deve entender a interpretá-los. Vamos começar analisando a seguinte imagem:

<p align="center">
  <img src="./assets/understanding-tests.png">
</p>

Logo acima da imagem, temos em vermelho um título que específica qual teste deu errado. Nesse caso o teste que falhou é o teste **`should be able to give a like to the repository`**, do módulo de **Likes**.

Para entender o que deu de errado, posso olhar exatamente esse trecho:

<p align="center">
  <img src="./assets/expect-test.png">
</p>

Disso podemos entender que o teste esperava receber o valor `likes: 1`, mas recebeu `likes: 0`.

Sabendo disso, see eu for até o meu código, vou ver que de fato na minha função de aumentar o número de likes eu nunca incrementei esse valor, então os likes do repositório encontrado sempre serão retornados como 0.

<p align="center">
  <img src="./assets/code-example.png">
</p>

### Específicação dos testes

Em cada teste, tem uma breve descrição no que sua aplicação deve cumprir para que o teste passe.

Para esse desafio temos os seguintes testes:

- **`should be able to create a new repository`**: Para que esse teste passe, sua aplicação deve permitir que um repositório seja criado, e retorne um json com o projeto criado.

- **`should be able to list the repositories`**: Para que esse teste passe, sua aplicação deve permitir que seja retornado um array com todos os repositórios que foram criados até o momento.

- **`should be able to update repository`**: Para que esse teste passe, sua aplicação deve permitir que sejam alterados apenas os campos `url`, `title` e `techs`.

- **`should not be able to update a repository that does not exist`**: Para que esse teste passe, você deve validar na sua rota de update se o id do repositório enviado pela url existe ou não. Caso não exista, retornar um erro com status `400`.

- **`should not be able to update repository likes manually`**: Para que esse teste passe, você não deve permitir que sua rota de update altere diretamente os likes desse repositório, mantendo o mesmo número de likes que o repositório já possuia antes da atualização. Isso porque o único lugar que deve atualizar essa informação é a rota de responsável por aumentar o número de likes.

- **`should be able to delete the repository`**: Para que esse teste passe, você deve perimtir que a sua rota de delete excluia um projeto, e ao fazer a exclusão, ele retorne uma resposta vazia, com status `204`.

- **`should not be able to delete a repository that does not exist`**: Para que esse teste passe, você deve validar na sua rota de delete se o id do repositório enviado pela url existe ou não. Caso não exista, retornar um erro com status `400`.

- **`should be able to give a like to the repository`**: Para que esse teste passe, sua aplicação deve permitir que um repositório com o id informado possa receber likes. O valor de likes deve ser incrementado em 1 a cada requisição.

- **`should not be able to like a repository that does not exist`**: Para que esse teste passe, você deve validar na sua rota de like se o id do repositório enviado pela url existe ou não. Caso não exista, retornar um erro com status `400`.

## :calendar: Entrega

Esse desafio deve ser entregue a partir da plataforma Skylab. Após concluir o desafio, fazer um post no Linkedin e postar o código no Github é uma boa forma de demonstrar seus conhecimentos e esforços para evoluir na sua carreira para oportunidades futuras.

## :memo: Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE.md) para mais detalhes.

---

Feito com 💜 by Rocketseat :wave: [Entre na nossa comunidade!](https://discordapp.com/invite/gCRAFhc)

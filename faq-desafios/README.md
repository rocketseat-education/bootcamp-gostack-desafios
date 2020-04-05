<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios.png" />
<h2 align="center">
  FAQ referente aos desafios
</h2>

## Dúvidas

- [O que são os testes automatizados?](#o-que-são-os-testes-automatizados)
- [Como interpretar os erros nos testes?](#como-interpretar-os-erros-nos-testes)

### O que são os testes automatizados?

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

**Dica 2**: Esses testes serão os mesmos testes que e irão corrigir seu desafio e darão sua nota, então recomendamos que os siga a risca e tenha certeza que todos passem para receber nota máxima!

### Como interpretar os erros nos testes?

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

Sabendo disso, nesse exemplo, se formos até o código, vamos ver que de fato a função de aumentar o número de likes nunca incrementou esse valor, então os likes do repositório encontrado sempre serão retornados como 0.

<p align="center">
  <img src="./assets/code-example.png">
</p>

## :memo: Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE.md) para mais detalhes.

---

Feito com 💜 by Rocketseat :wave: [Entre na nossa comunidade!](https://discordapp.com/invite/gCRAFhc)

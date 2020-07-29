<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios.png" />

<h3 align="center">
  Desafio 09: Relacionamentos com banco de dados no Node.js
</h3>

<blockquote align="center">“Mude você e todo o resto mudará naturalmente”!</blockquote>

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

Nesse desafio, você vai estar criando uma nova aplicação para aprender novas coisas e treinar o que você aprendeu até agora no Node.js junto ao TypeScript, incluindo o uso de banco de dados com o TypeORM, e relacionamentos ManyToMany!

Essa será uma aplicação que deve permitir a criação de clientes, produtos e pedidos, onde o cliente pode gerar novos pedidos de compra de certos produtos, como um pequeno e-commerce.

### 1º PASSO - Utilizar template da aplicação

Para te ajudar nesse desafio, criamos para você um modelo que você deve utilizar como um template do Github.

O template está disponível na seguinte url: **[Acessar Template](https://github.com/Rocketseat/gostack-template-typeorm-relations)**

**DICA**: Caso não saiba utilizar repositórios do Github como template, temos um guia em **[nosso FAQ](https://github.com/Rocketseat/bootcamp-gostack-desafios/tree/master/faq-desafios).**

---

Agora que você já está com o template clonado e pronto para continuar, navegue até a pasta criada e abra no Visual Studio Code. Você deverá verificar os arquivos da pasta `src` e completar onde não possui código com o código para atingir os objetivos deste desafio.

⚠️ Lembre-se de executar o comando `yarn` no seu terminal para instalar todas as dependências.

---

### 2º PASSO - Configurar o banco de dados

Crie um banco de dados PostgreSQL com o nome `gostack_desafio09` para que você possa realizar testes das rotas com o **INSOMNIA**.

Para rodar os testes o nome do banco de dados deve ser `gostack_desafio09_tests`.

---

### 3º PASSO - Configurar injeções de dependência

Navegue até o arquivo `index.ts` da pasta `src/shared/container` e faça o registro das injeções de dependência para serem utilizadas posteriormente.

---

### 4º PASSO - Criar e configurar migrations

Migration `CreateCustomers` cria tabela `customers` conforme _entitie_ `Customer`
Migration `CreateProducts` cria tabela `products` conforme _entitie_ `Product`
Migration `CreateOrders` cria tabela `orders` conforme _entitie_ `Order`
Migration `CreateOrdersProducts` cria tabela `orders_products` conforme _entitie_ `OrdersProducts`

Migration `AddCustomerIdToOrders` adiciona coluna `customer_id` na tabela `orders` e _foreign key_ com a coluna `id` a tabela `customers`

Migration `AddOrderIdToOrdersProducts` adiciona coluna `order_id` na tabela `orders_products` e _foreign key_ com a coluna `id` a tabela `orders`

Migration `AddProductIdToOrdersProducts` adiciona coluna `product_id` na tabela `orders_products` e _foreign key_ com a coluna `id` a tabela `products`

**DICA**: Para o campo `price`, você pode utilizar o `type` como `decimal`, passando também as propriedades `precision` e `scale`. Verifique na documentação do TypeORM [como configurar as propriedade precision e scale](https://typeorm.delightful.studio/interfaces/_decorator_options_columnnumericoptions_.columnnumericoptions.html#precision).

---

### 5º PASSO - Configurar _entities:_

### `Customer`

### `Product`

Esta _entitie_ deve possuir um relacionamento com a _entitie_ `OrdersProducts` através do item `order_products`. Esse item serve para relacionar o id do produto com o pedido completo que será salvo na tabela `order_products`. Para este item será necessário fazer o relacionamento `@OneToMany` com a _entitie_ `OrdersProducts`, passando um apelido de referência, pois cada produto poderá estar em vários pedidos.

### `Order`

Esta _entitie_ deve possuir um relacionamento com a _entitie_ `OrdersProducts` através do item `order_products`. Esse item serve para relacionar o id do pedido com o pedido completo que será salvo na tabela `order_products`. Para este item será necessário fazer o relacionamento `@OneToMany` com a _entitie_ `OrdersProducts`, passando um apelido de referência, pois cada pedido poderá estar em vários pedidos.

O item `customer` servirá para fazer um relacionamento `@ManyToOne` com a _entitie_ `Customer` e criar a coluna `customer_id` através do `@JoinColumn`. O objetivo é armazenar o id do comprador na coluna `customer_id` da tabela `orders`.

Você pode também utilizar o método `cascade` do TypeORM, que irá adicionar na tabela `order_products` os produtos que você passar por parâmetro para a _entitie_ `Order` automaticamente. Verifique na documentação do TypeORM [como utilizar a opção cascade](https://github.com/typeorm/typeorm/blob/master/docs/relations.md#cascade-options).

### `OrdersProducts`

Esta _entitie_ faz o relacionamento entre pedidos e produtos. Na tabela pivô `orders_products` será armazenado o número do pedido (proveniente da tabela `orders`), o id do produto (proveniente da tabela `products`), a quantidade e o valor do produto no momento da compra.

Deverá ser utilizado o relacionamento `@ManyToOne` para referenciar os relacionamentos feitos nas _entities_ `Product` e `Order` e então criar as colunas `order_id` e `product_id` para armazenar os valores provenientes das suas respectivas tabelas.

Para esse tipo de relacionamento, verifique na documentação do TypeORM [como fazer relacionamento muitos-para-muitos com propriedades customizadas](https://github.com/typeorm/typeorm/blob/master/docs/many-to-many-relations.md#many-to-many-relations-with-custom-properties).

<p align="center">
  <img src="./relations.gif" alt="Relacionamentos do banco de dados">
Modelagem feita no SqlDBM para melhor ilustrar os relacionamentos.
</p>

---

## 6º PASSO - Configurar _repositories:_

### `CustomersRepository`

### `ProductsRepository`

Neste _repository_, na função `findAllById` você poderá mapear os IDs recebidos no array de produtos e utilizar a função `In()` do TypeORM para buscar pelos IDs no método `find()`.

### `OrdersRepository`

Neste _repository_ você pode utilizar a opção [relations](https://github.com/typeorm/typeorm/blob/master/docs/find-options.md#basic-options) para o método findOne do TypeORM, informando os nomes das tabelas que você deseja buscar o relacionamento, ou utilizar o [eager do TypeORM](https://github.com/typeorm/typeorm/blob/master/docs/eager-and-lazy-relations.md#eager-relations) na _entitie_.

---

## 7º PASSO - Configurar _services:_

⚠️ Antes de criar as regras de negócio, lembre-se de criar as injeções de dependência conforme foram registradas no **3º PASSO**.

### `CreateCustomerService`

Este _service_ irá receber `name` e `email` que deverá ser salvo no banco de dados através do método `create` do `customersRepository`, porém antes deverá ser verificado se já existe um `customer` com o mesmo `email`. Caso exista, retorne um erro.

Após o cadastro deverá ser retornado o `customer` criado.

### `CreateProductService`

Este _service_ irá receber `name`, `price` e `quantity` que deverá ser salvo no banco de dados através do método `create` do `productsRepository`, porém antes deverá ser verificado se já existe um `product` com o mesmo `name`. Caso exista, retorne um erro.

Após o cadastro deverá ser retornado o `product` criado.

### `FindOrderService`

Este _service_ irá receber od `id` do pedido que será consultado no banco de dados através do método `findById` do `ordersRepository`.

Se o `id` informado NÃO existir no banco de dados, retorne um erro.

Se o `id` informado existir no banco de dados, retorne o pedido correspondente.

### `CreateOrderService`

Este _service_ irá receber o pedido contendo o `customer_id`, e um array de `products` com `id` e `quantity`, que deverá ser salvo no banco de dados através do método `create` do `ordersRepository`, porém antes deverá feito as seguintes verificações:

- **1ª VERIFICAÇÃO**
  Utilize o método `findById` do `customersRepository` para verificar se o `customer_id` informado existe no banco de dados, se não existir retorne um erro.

- **2ª VERIFICAÇÃO**
  Utilize o método `findAllById` do `productsRepository` para verificar se os produtos do array `products` informado existem no banco de dados, se não existir nenhum retorne um erro.

- **3ª VERIFICAÇÃO**
  Faça um `map()` no array de produtos da 2ª VERIFICAÇÃO e armazene o `id` de cada um num novo array.
  Faça um filtro no array recebido de `products` para identificar quais produtos não foram encontrados. Para cada `product.id` deste filtro deverá ser verificado o que não existe no array resultante do `map()` criado anteriormente.
  Se no array resultante deste filtro conter algum item, retorne um erro dizendo qual produto não foi encontrado.

- **4ª VERIFICAÇÃO**
  Faça um filtro no array `products` recebido e verifique se as quantidades solicitadas estão disponíveis. Para cada item deste filtro faça um filtro no array de produtos da 2ª VERIFICAÇÃO e, deixe passar somente os items que possuem `quantity` < que a `quantity` informada na requisição.

Se no array resultante deste filtro conter algum item, retorne um erro dizendo que a quantidade do produto requisitado não está disponível.

Após passar em todas as verificações anteriores, formate os dados para salvar no banco de dados.

Faça um `map()` no array `products` recebido e para cada item faça a formatação conforme a interface `IProduct` do `ICreateOrderDTO` que é o formato que deverá ser enviado ao método `create` do `ordersRepository`. O motivo de fazer essa formatação é porque o preço não foi enviado na requisição, apenas o `id` do produto e a `quantity` desejada. Para buscar o preço, faça um filtro no array de produtos da 2ª VERIFICAÇÃO.

Após criar o pedido no banco de dados, abstraia o `order_products` do resultado do `ordersRepository.create` e faça um `map()` criando um novo array, para cada item deste array mapeado informe o `id` do produto e a `quantity`, porém na quantidade deverá ser feito um filtro no array de produtos da 2ª VERIFICAÇÃO subtraindo a `quantity` do resultado do `map()`. O resultado deste array deverá ser enviado através do método `updateQuantity` do `productsRepository`.

---

## 8º PASSO - Configurar _controllers:_

### `CustomersController`

O método `create` deve receber `name` e `email` dentro do corpo da requisição, sendo o `name` o nome do cliente a ser cadastrado. Ao cadastrar um novo cliente, ele deve ser armazenado dentro do seu banco de dados e deve ser retornado o cliente criado.

### `ProductsController`

O método `create` deve receber `name`, `price` e `quantity` dentro do corpo da requisição, sendo o `name` o nome do produto a ser cadastrado, `price` o valor unitário e `quantity` a quantidade existente em estoque do produto.

### `OrdersController`

O método `show` deve receber no endereço da rota o `id` do pedido que deseja ser encontrado, este `id` deverá ser enviado para o _service_ `FindOrderService` utilizando o princípio de inversão de dependência.

O método `create` deve receber no corpo da requisição o `customer_id` e um array de `products`, contendo o `id` do produto e a `quantity` desejada para compor o pedido que deverá ser enviado para o _service_ `CreateOrderService` utilizando o princípio de inversão de dependência.

A requisição do **INSOMNIA** deve enviar um JSON com o formato parecido com esse para a rota **`POST /orders`**

```json
{
  "customer_id": "e26f0f2a-3ac5-4c21-bd22-671119adf4e9",
  "products": [
    {
      "id": "ce0516f3-63ae-4048-9a8a-8b6662281efe",
      "quantity": 5
    },
    {
      "id": "82612f2b-3f31-40c6-803d-c2a95ef35e7c",
      "quantity": 7
    }
  ]
}
```

Uma chamada a essa rota deve retornar os dados do cliente, produtos do pedido e id do pedido, num formato parecido com o seguinte:

```json
{
  "id": "5cbc4aa2-b3dc-43f9-b121-44c1e416fa92",
  "created_at": "2020-05-11T07:09:48.767Z",
  "updated_at": "2020-05-11T07:09:48.767Z",
  "customer": {
    "id": "e26f0f2a-3ac5-4c21-bd22-671119adf4e9",
    "name": "Rocketseat",
    "email": "oi@rocketseat.com.br",
    "created_at": "2020-05-11T06:20:28.729Z",
    "updated_at": "2020-05-11T06:20:28.729Z"
  },
  "order_products": [
    {
      "product_id": "ce0516f3-63ae-4048-9a8a-8b6662281efe",
      "price": "1400.00",
      "quantity": 5,
      "order_id": "5cbc4aa2-b3dc-43f9-b121-44c1e416fa92",
      "id": "265b6cbd-3ab9-421c-b358-c2e2b5b3b542",
      "created_at": "2020-05-11T07:09:48.767Z",
      "updated_at": "2020-05-11T07:09:48.767Z"
    },
    {
      "product_id": "82612f2b-3f31-40c6-803d-c2a95ef35e7c",
      "price": "500.00",
      "quantity": 7,
      "order_id": "5cbc4aa2-b3dc-43f9-b121-44c1e416fa92",
      "id": "ae37bcd6-7be7-47b9-b277-afee35aab4e4",
      "created_at": "2020-05-11T07:09:48.767Z",
      "updated_at": "2020-05-11T07:09:48.767Z"
    }
  ]
}
```

---

## 9º PASSO - Testes

Em cada teste, tem uma breve descrição no que sua aplicação deve cumprir para que o teste passe.

Caso você tenha dúvidas quanto ao que são os testes, e como interpretá-los, dê uma olhada em **[nosso FAQ](https://github.com/Rocketseat/bootcamp-gostack-desafios/tree/master/faq-desafios).**

Para esse desafio, temos os seguintes testes:

<h4 align="center">
  ⚠️ Antes de rodar os testes, certifique-se de que banco de dados com o nome "gostack_desafio09_tests" esteja configurado corretamente ⚠️
</h4>

- **`should be able to create a new customer`**: Para que esse teste passe, sua aplicação deve permitir que um cliente seja criado, e retorne um json com o cliente criado.

- **`should NOT be able to create a customer with one e-mail thats already registered`**: Para que esse teste passe, sua aplicação deve retornar um erro quando você tentar cadastrar um cliente com um e-mail que já esteja cadastrado no banco de dados.

- **`should be able to create a new product`**: Para que esse teste passe, sua aplicação deve permitir que um produto seja criado, e retorne um json com o produto criado.

- **`should NOT be able to create a duplicated product`**: Para que esse teste passe, sua aplicação deve retornar um erro quando você tentar cadastrar um produto com um nome que já esteja cadastrado no banco de dados.

- **`should be able to create a new order`**: Para que esse teste passe, sua aplicação deve permitir que um pedido seja criado, e retorne um json com o todos os dados do pedido criado.

- **`should NOT be able to create an order with a invalid customer`**: Para que esse teste passe, sua aplicação não deve permitir a criação de um novo pedido com um cliente que não existe no banco de dados, retornando um erro.

- **`should NOT be able to create an order with invalid products`**: Para que esse teste passe, sua aplicação não deve permitir a criação de um novo pedido com um produtos que não existem no banco de dados, retornando um erro caso um ou mais dos produtos enviados não exista no banco de dados.

- **`should NOT be able to create an order with products with insufficient quantities`**: Para que esse teste passe, sua aplicação não deve permitir a criação de um novo pedido com um produtos que não possuem quantidade disponível, retornando um erro caso um ou mais dos produtos enviados não possua a quantidade necessária.

- **`should be able to subtract an product total quantity when it is ordered`**: Para que esse teste passe, sua aplicação deve permitir que, quando um novo pedido for criado, seja alterada a quantidade total dos produtos baseado na quantidade pedida.

- **`should be able to list one specific order`**: Para que esse teste passe, você deve permitir que a rota `orders/:id` retorne um pedido, contendo todas as informações do pedido com o relacionamento de `customer` e `order_products`.

### Links úteis

- [Cascade option TypeORM](https://github.com/typeorm/typeorm/blob/master/docs/relations.md#cascade-options)
- [Relacionamento many-to-many personalizado](https://github.com/typeorm/typeorm/blob/master/docs/many-to-many-relations.md#many-to-many-relations-with-custom-properties)
- [Eager loading com TypeORM](https://github.com/typeorm/typeorm/blob/master/docs/eager-and-lazy-relations.md#eager-relations)
- [Opções de relacionamentos do TypeORM](https://github.com/typeorm/typeorm/blob/master/docs/find-options.md)

## :calendar: Entrega

Esse desafio deve ser entregue a partir da plataforma Skylab, envie o link do repositório que você fez suas alterações. Após concluir o desafio, fazer um post no Linkedin e postar o código no Github é uma boa forma de demonstrar seus conhecimentos e esforços para evoluir na sua carreira para oportunidades futuras.

## :memo: Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Feito com 💜 by Rocketseat :wave: [Entre na nossa comunidade!](https://discordapp.com/invite/gCRAFhc)

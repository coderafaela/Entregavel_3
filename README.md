# Entregável 3

**Projeto: site-soma**

API simples em **Node.js + Express** que recebe requisições **POST** com dois números e devolve o resultado de uma operação matemática (soma, subtração, divisão e multiplicação). Os testes foram feitos com o **Postman**.

> Atividade assíncrona das disciplinas **Desenvolvimento de Software em Nuvem** e **Ambientes de Desenvolvimento de Software** (UNIFOR).

## Sumário

- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Como criar o projeto do zero](#como-criar-o-projeto-do-zero)
- [Como executar](#como-executar)
- [Endpoints](#endpoints)
- [Testes no Postman](#testes-no-postman)
- [Código-fonte](#código-fonte)
- [Observações](#observações)

## Tecnologias

- [Node.js](https://nodejs.org/)
- [Express](https://expressjs.com/)
- [body-parser](https://www.npmjs.com/package/body-parser)
- [Postman](https://www.postman.com/) (para testar as requisições)
- Visual Studio Code

## Pré-requisitos

- Node.js e npm instalados
- Postman (ou outra ferramenta para requisições HTTP)

## Como criar o projeto do zero

1. Crie uma pasta chamada `site-soma` e abra-a no Visual Studio Code (**Arquivo > Abrir pasta**).
2. No terminal do VS Code, crie um novo projeto NPM:

   ```bash
   npm init -y
   ```

3. Instale o Express:

   ```bash
   npm install express
   ```

4. Instale o body-parser, biblioteca que ajuda a ler os dados enviados via POST:

   ```bash
   npm install body-parser
   ```

5. Crie o arquivo `app.js` e cole o [código-fonte](#código-fonte) abaixo.

## Como executar

Na pasta do projeto, execute:

```bash
node app.js
```

Se tudo der certo, o terminal exibirá:

```
App de Exemplo escutando na porta http://localhost:3001/
```

Depois, acesse [http://localhost:3001](http://localhost:3001) no navegador ou no Postman.

## Endpoints

| Método | Rota             | Descrição                     | Corpo (JSON)             |
| ------ | ---------------- | ----------------------------- | ------------------------ |
| GET    | `/`              | Mensagem de boas-vindas       | —                        |
| POST   | `/soma`          | Soma `a + b`                  | `{ "a": 10, "b": 5 }`    |
| POST   | `/subtracao`     | Subtrai `a - b`               | `{ "a": 10, "b": 5 }`    |
| POST   | `/divisao`       | Divide `a / b`                | `{ "a": 10, "b": 5 }`    |
| POST   | `/multiplicacao` | Multiplica `a * b`            | `{ "a": 10, "b": 5 }`    |

Todas as rotas POST retornam um texto no formato:

```
O resultado da <operação> de <a> e <b> é <resultado>
```

## Testes no Postman

Para as rotas POST, configure a requisição em **Body > raw > JSON** e envie o seguinte corpo:

```json
{
  "a": 10,
  "b": 5
}
```

### 1. GET `/`

Verifica se o servidor está no ar. Retorna `Oi, mundo :-)`.

![GET /](https://drive.google.com/thumbnail?id=1iL1o1o4GCx4tgA42a-yFPr2eRCJUYsn6&sz=w1600)

### 2. POST `/soma`

Resultado esperado: `O resultado da soma de 10 e 5 é 15`

![POST /soma](https://drive.google.com/thumbnail?id=1I0mb1zOQeDh5-Di2fHqkqydJdfqKTpYQ&sz=w1600)

### 3. POST `/subtracao`

Resultado esperado: `O resultado da subtração de 10 e 5 é 5`

![POST /subtracao](https://drive.google.com/thumbnail?id=1SDOjqZO1zXLiHNEwEH6fDGmWT9NbzVnI&sz=w1600)

### 4. POST `/divisao`

Resultado esperado: `O resultado da divisão de 10 e 5 é 2`

![POST /divisao](https://drive.google.com/thumbnail?id=1ABJbMIEBHUX3f2bbwclwtP51dZYDjuHp&sz=w1600)

### 5. POST `/multiplicacao`

Resultado esperado: `O resultado da multiplicação de 10 e 5 é 50`

![POST /multiplicacao](https://drive.google.com/thumbnail?id=1IH0D6OuwT-JxEolACVQ0iHk1qFazZsCo&sz=w1600)

## Código-fonte

`app.js`:

```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

function soma(a, b) {
  return a + b;
}

function subtracao(a, b) {
  return a - b;
}

function divisao(a, b) {
  return a / b;
}

function multiplicacao(a, b) {
  return a * b;
}

app.get('/', function(req, res) {
  res.send('Oi, mundo :-)');
});

app.post('/soma', function (req, res) {
  var body = req.body;
  var resultado = soma(body.a, body.b);

  res.send(`O resultado da soma de ${body.a} e ${body.b} é ${resultado}`);
});

app.post('/subtracao', function (req, res) {
  var body = req.body;
  var resultado = subtracao(body.a, body.b);

  res.send(`O resultado da subtração de ${body.a} e ${body.b} é ${resultado}`);
});

app.post('/divisao', function (req, res) {
  var body = req.body;
  var resultado = divisao(body.a, body.b);

  res.send(`O resultado da divisão de ${body.a} e ${body.b} é ${resultado}`);
});

app.post('/multiplicacao', function (req, res) {
  var body = req.body;
  var resultado = multiplicacao(body.a, body.b);

  res.send(`O resultado da multiplicação de ${body.a} e ${body.b} é ${resultado}`);
});

var port = 3001;

// iniciando o processo do servidor
app.listen(port, function() {
  console.log(`App de Exemplo escutando na porta http://localhost:${port}/`);
});
```

## Observações

- Os valores `a` e `b` devem ser enviados como **números** no JSON (ex.: `10`, e não `"10"`). Se forem strings, o operador `+` faz concatenação em vez de soma.
- Na divisão, o código não trata `b = 0`; nesse caso o JavaScript retorna `Infinity`. Uma melhoria possível é validar o divisor e retornar um erro (por exemplo, status `400`).
- A resposta é enviada como texto (`res.send`), por isso o Postman a exibe no formato HTML.

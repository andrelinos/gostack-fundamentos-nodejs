# GoStack Fundamentos NodeJS - Exercício

<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios.png" />

<h3 align="center">
  Desafio 05: Primeiro projeto Node.js
</h3>

<p align="center"><strong>“Para quem fica melhor a cada dia, ficar pronto é utopia”!</strong></blockquote>

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

<p align="center">Desafio de Node.js do nível de "Primeiro projeto com Node.js"</p>

## Sobre o projeto
Este projeto foi desenvolvido com base no template *gostack-template-fundamentos-node-desafio* feito pela a @rocketseat para o desafio do bootcamp *Desafio: Fundamentos Node.js*.

## Models
**[uuid](https://github.com/uuidjs/uuid)**:  O uuidv4 é uma ferramenta usada para a geração de ID automático para aplicações NodeJS e ReactJS.

```js
  import { uuid } from 'uuidv4';
```

**Transaction**:  Esta parte define o tipo de cada item do objeto.
```js
class Transaction {
  id: string;

  title: string;

  value: number;

  type: 'income' | 'outcome';
```

```js
constructor({ title, value, type }: Omit<Transaction, 'id'>) {
  this.id = uuid();
    this.title = title;
    this.value = value;
    this.type = type;
  }
  ```
**Nota:** O `Omit<Transaction, 'id'>` irá omitir o id item na listagem para que o mesmo não seja exibido em nenhuma parte da aplicação. Pois o ID é de responsabilidade apenas interna da aplicação.

## Respositories

**Import**:  Nesta parte faz o import do model do *TransactionsRepository*
```js
import Transaction from '../models/Transaction';
```

**interface**:  No item *interface* definimos o tipo de cada item
```js
interface Balance {
  income: number;
  outcome: number;
  total: number;
}

interface CreateTransactionDTO {
  title: string;
  value: number;
  type: 'income' | 'outcome';
}
```

**enum**:
```js
enum Type {
  INCOME = 'income',
  OUTCOME = 'outcome',
}

/*----*/
public getBalance(): Balance {
    const income = this.calculateBalance(Type.INCOME);
    const outcome = this.calculateBalance(Type.OUTCOME);
    const total = income - outcome;

    const balance: Balance = { income, outcome, total };

    return balance;
  }
```
**Sobre o enum**: O enum é um dos tipos do TypeScript que nos permite declarar um conjunto de valores/constantes pré-definidos. ... Nós podemos buscar um registro pela sua declaração ou pelo seu valor.

**Exemplo**
```js
export enum DiaDaSemana {
    Segunda = 1,
    Terca = 2,
    Quarta = 3,
    Quinta = 4,
    Sexta = 5,
    Sabado = 6,
    Domingo = 7,
}

let dia = DiaDaSemana[1]; // Segunda
let diaNumero = DiaDaSemana[dia]; // 1
let diaString= DiaDaSemana["Segunda"]; // 1

for (let dia in DiaDaSemana) {
    if (DiaDaSemana.hasOwnProperty(dia) &&
        (isNaN(parseInt(dia)))) {
        console.log(dia);
    }
}

Resultado:
Segunda
Terca
Quarta
Quinta
Sexta
Sabado
Domingo
```
**Fonte**: [medium](https://medium.com/typescript/typescript-enums-1f5cc877aaa3)

## Transaction.routes

[express](https://github.com/expressjs/express)

Nesta parte você define as rotas para realizar *POST*, *GET*, *PUT*, *DELETE*
**Exemplo**:
```js
transactionRouter.post('/', (request, response) => {
  /**/
return response.status(200).json();
}

transactionRouter.get('/', (request, response) => {
  /* ... */
  return response.status(200).json();
}

transactionRouter.status(200).put('/:id', (request, response) => {
  /* ... */
  return response.status(200).json();
}

transactionRouter.delete('/', (request, response) => {
 /* ... */
  return response.status(204).send();
}
```

## CreateTransactionService
Este arquivo é responsável pela função **execute** usada pela *transaction.routes*, no para criar conteúdo dentro do padrão predefinido.

```js
class CreateTransactionService {
  private transactionsRepository: TransactionsRepository;

  constructor(transactionsRepository: TransactionsRepository) {
    this.transactionsRepository = transactionsRepository;
  }

  public execute({ title, value, type }: Request): Transaction {
    const transaction = this.transactionsRepository.create({
      title,
      value,
      type,
    });

    return transaction;
  }
  ```

## Rotas para execução
**POST**: {{ base_url  }}/transactions
Criar uma nova transação de entrada ou saída.
*Exemplo de entrada de valor:*
```json
{
  "title": "Salário",
  "value": 4500,
  "type": "income"
}
```
*Exemplo de saída de valor:*
```json
{
  "title": "Salário",
  "value": 550,
  "type": "outcome"
}
```

**GET**: {{ base_url  }}/transactions
Listar todas as transações (income | outcome), valor total para entrada e saída e saldo final (total).


## Como Rodar a aplicação
- Acesse uma pasta a sua escolha em seu computador usando o terminal
- Digite o seguinte comando:
```zsh
git clone https://github.com/andrelinos/gostack-fundamentos-nodejs.git
```
- Em seguida acesse a pasta com o comando: `cd gostack-fundamentos-nodejs`.
- Dentro da pasta digite `yarn` para instalar as dependências.
- Após, bora codar!

##

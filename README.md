# Desafio Backend

A ideia é simples. Vamos construir a base de qualquer aplicação: um sistema de gerenciamento de usuários.

## A Missão

Sua missão, caso decida aceitar, é desenvolver uma API para realizar as quatro operações básicas (CRUD) em uma entidade `User`.

-   **C**reate (Criar)
-   **R**ead (Ler)
-   **U**pdate (Atualizar)
-   **D**elete (Deletar)

O desafio deve ser concluído em **uma semana**.

## Modelo de Dados

A entidade `User` deve conter, no mínimo, os seguintes campos:

-   `id`: Identificador único (ex: UUID ou um inteiro auto-incrementado).
-   `name`: String, nome do usuário.
-   `email`: String, email único para cada usuário.
-   `password`: String, a senha do usuário **(jamais guarde em texto puro!)**.
-   `createdAt`: Timestamp, data de criação do registro.
-   `updatedAt`: Timestamp, data da última atualização do registro.

## ✅ Requisitos Funcionais

Sua API deve expor os seguintes endpoints:

-   `[POST] /users`: Cria um novo usuário.
-   `[GET] /users`: Lista todos os usuários.
-   `[GET] /users/:id`: Busca um usuário específico pelo seu `id`.
-   `[PUT] /users/:id`: Atualiza os dados de um usuário específico.
-   `[DELETE] /users/:id`: Remove um usuário do sistema.

## Diretrizes Técnicas

### Liberdade de Escolha
Você tem total liberdade para escolher as ferramentas que mais te agradam. Quer usar Go, Python, NodeJS, Java ou Rust? Manda ver! O mesmo vale para o banco de dados: PostgreSQL, MongoDB, MySQL, a escolha é sua. O importante é a qualidade da entrega final.

### Boas Práticas (O que vamos observar)
-   **Padrões RESTful**: Utilize os verbos HTTP e os status codes corretamente (200, 201, 404, 500, 401).
-   **Validação de Dados**: Nenhum dado inválido pode ser inserido no banco. Um email deve ser um EMAIL, a senha deve ter requisitos mínimos, o resto você define, pense na segurança da sua aplicação.
-   **Segurança**: A senha do usuário **deve** ser armazenada usando um algoritmo de hash seguro (ex: `bcrypt`).
-   **Tratamento de Erros**: A API deve retornar mensagens de erro claras e úteis.
-   **Estrutura do Projeto**: Organize seu código de forma limpa e escalável (ex: separação de controllers, services, repositories, etc.).

## Exemplos de Implementação (Node.js com Express)

Para te dar um norte, aqui estão alguns exemplos de como os endpoints poderiam se comportar.

#### `[POST] /users`

```javascript
// Exemplo de controller para criar um usuário
app.post('/users', (req, res) => {
  const { name, email, password } = req.body;

  // 1. Validar os dados recebidos (ex: com Zod ou Joi)
  // 2. Hashear a senha com bcrypt
  // 3. Salvar o novo usuário no banco de dados

  const newUser = {
    id: 'c2a7e7a0-3b2a-4f5c-8d1e-3e8a7f6b9c0d',
    name: "Usuário",
    email: "user@email.com",
    createdAt: "2025-09-07T12:00:00.000Z",
    updatedAt: "2025-09-07T12:00:00.000Z",
  };

  // Retorna o status 201 Created e o usuário criado (sem a senha!)
  return res.status(201).json(newUser);
});
```
#### `GET /users/id`

```javascript

// Retorno esperado (sucesso) - HTTP 201
{
  "id": "c2a7e7a0-3b2a-4f5c-8d1e-3e8a7f6b9c0d",
  "name": "Usuário",
  "email": "user@email.com",
  "createdAt": "2025-09-07T12:00:00.000Z",
  "updatedAt": "2025-09-07T12:00:00.000Z"
}

// Retorno esperado (erro de validação) - HTTP 400
{
  "error": "O campo 'email' é inválido."
}

// Exemplo de controller para buscar um usuário
app.get('/users/:id', (req, res) => {
  const { id } = req.params;

  // 1. Buscar o usuário no banco pelo ID
  const user = findUserById(id);

  // 2. Se não encontrar, retornar 404 Not Found
  if (!user) {
    return res.status(404).json({ error: 'Usuário não encontrado.' });
  }

  // 3. Se encontrar, retornar o usuário (sem a senha)
  return res.status(200).json(user);
});


// Retorno esperado (sucesso) - HTTP 200
{
  "id": "c2a7e7a0-3b2a-4f5c-8d1e-3e8a7f6b9c0d",
  "name": "Usuário",
  "email": "user@email.com",
  "createdAt": "2025-09-07T12:00:00.000Z",
  "updatedAt": "2025-09-07T12:15:30.000Z"
}

// Observe que a senha não foi retornada

// Retorno esperado (não encontrado) - HTTP 404
{
  "error": "Usuário não encontrado."
}
```

### `DELETE /users/id`

```javascript
// Exemplo de controller para deletar um usuário
app.delete('/users/:id', (req, res) => {
  const { id } = req.params;

  // 1. Tentar deletar o usuário no banco pelo ID
  const wasDeleted = deleteUserById(id);
  
  // 2. Se o usuário não existia, pode retornar 404
  if (!wasDeleted) {
      return res.status(404).json({ error: 'Usuário não encontrado.' });
  }

  // 3. Se deletou com sucesso, retornar 204 No Content
  return res.status(204).send();
});

// Retorno esperado (sucesso) - HTTP 204
// (Sem corpo de resposta)
```

## Como Participar

1.  **Fork** este repositório.
2.  Crie uma nova **branch** para o seu desenvolvimento (ex: `feat/user-crud-davi`).
3.  Faça seus commits e, ao finalizar, abra um **Pull Request** para a branch `main` do repositório original.
4.  Coloque um resumo do que você fez na descrição do PR.

## Não se prenda

Não se sinta preso somente ao básico, pesquise o que o mercado geralmente usa pra essas aplicações

Como testar ?
Como ver os dados ?
Qual a melhor tecnologia pra acompanhar ?

## Busque sempre aprender

Faça perguntas para si, mesmo que você ache que sejam bestas, aprender nunca é demais, então faça perguntas do tipo:

O que é uma API ?
o que é um JSON ?
o que é o protocolo HTTP ?
o que é CRUD ?
**Como funciona** o meu código ?

### Boa sorte no Desafio <3

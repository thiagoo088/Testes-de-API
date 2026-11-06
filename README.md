# Testes de API – Hub de Leitura

Coleção do **Postman** com testes automatizados da API do **Hub de Leitura**, um sistema de biblioteca com cadastro de usuários, autenticação, catálogo de livros e reservas. A coleção cobre cenários **positivos** e **negativos**.

## 📁 Arquivos

| Arquivo | Descrição |
|---|---|
| `Hub de Leitura.postman_collection.json` | Coleção com as requisições e os testes automatizados |
| `Hub de Leitura.postman_environment.json` | Variáveis de ambiente (`baseUrl`, `token`, etc.) |

## ✅ Pré-requisitos

- [Postman](https://www.postman.com/downloads/) instalado
- API do Hub de Leitura rodando localmente (por padrão em `http://localhost:3000/api/`)

## 🚀 Como usar

1. No Postman, clique em **Import** e selecione os dois arquivos `.json` (coleção e ambiente).
2. Escolha o ambiente **Hub de Leitura** no canto superior direito.
3. Confira o valor da variável `baseUrl`, por exemplo `http://localhost:3000/api/` (com a barra no final, pois as rotas são concatenadas direto).
4. Execute primeiro **login com usuário administrador**: ele salva o token na variável `token`, usada pelas rotas protegidas.
5. Execute as demais requisições individualmente ou rode a coleção inteira pelo **Collection Runner**.

## 🔧 Variáveis

| Variável | Uso |
|---|---|
| `baseUrl` | URL base da API |
| `token` | Token salvo automaticamente após o login de administrador |
| `usuario` / `senha` | Dados usados no cadastro com e-mail inválido |

## 🧪 Cenários cobertos

### Gestão de Usuários
| Cenário | Tipo | Método | Endpoint | Validações |
|---|---|---|---|---|
| Cadastrar Usuario | Positivo | POST | `/users` | Status 201 e mensagem "Usuário criado com sucesso" (dados gerados com variáveis dinâmicas) |
| Cadastrar Usuário com e-mail inválido | Negativo | POST | `/users` | Status 400 e mensagem "Formato de email inválido" |
| E-mail sendo utilizado por outro usuário | Negativo | POST | `/users` | Status 400 e mensagem "Email já está sendo usado por outro usuário" |
| Listar usuarios | Positivo | GET | `/users` | Status 200 e propriedade `users` |
| Listar usuario por ID | Positivo | GET | `/users/:id` | Status 200 e propriedade `id` |
| Alterar usuário | Positivo | PUT | `/users/:id` | Status 200 e mensagem "Usuário atualizado com sucesso" |
| Deletar usuário | Positivo | DELETE | `/users/:id` | Status 200 e mensagem "Usuário removido com sucesso" |

### Autenticação
| Cenário | Tipo | Método | Endpoint | Validações |
|---|---|---|---|---|
| login com usuário padrão | Positivo | POST | `/login` | Status 200 e dados do "Usuário Padrão" |
| login com usuário administrador | Positivo | POST | `/login` | Status 200, presença de `id` e token salvo em `token` |
| Login de usuário com a senha errada | Negativo | POST | `/login` | Status 401 e mensagem "Email ou senha incorretos" |

### Reserva de livros
| Cenário | Tipo | Endpoint | Validações |
|---|---|---|---|
| criar reserva de livro | Positivo | `/reservations` | Status 200 e propriedade `reservations` |
| Reserva de livro sem o token | Negativo | `/reservations` | Status 401 e mensagem "Token de acesso necessário" |

### Catálogo de livros
| Cenário | Tipo | Método | Endpoint | Validações |
|---|---|---|---|---|
| Listar todos os livros disponíveis | Positivo | GET | `/books` | Status 200 e propriedade `books` |
| Listar livros usando filtro | Positivo | GET | `/books` | Status 200 e presença de "Harry Potter e a Pedra Filosofal" |
| Livro que não existe no catálogo | Negativo | GET | `/books/:id` | Status 404 e mensagem "Livro não encontrado" |

## 🛠️ Tecnologias

- Postman (coleção v2.1)
- Scripts de teste em JavaScript (`pm.test`)

## 👤 Autor

**Thiago do Nascimento**
[LinkedIn](https://linkedin.com/in/thiago-nascimento-5b99b4388) · [Instagram](https://instagram.com/qa.thiago)

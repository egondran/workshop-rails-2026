# Comandos

## Criar o projeto
---
Vamos criar um novo projeto Rails chamado `loja`. O `-d mysql` diz para o Rails usar o MySQL como banco de dados (sem isso, ele usaria o SQLite por padrão).

```bash
rails new loja -d mysql
```

Toda vez que criamos um projeto novo, o Rails gera uma pasta com esse nome. Precisamos entrar nela para continuar trabalhando.

```bash
cd loja
```
---

A partir de agora, vamos usar o VSCode para editar o projeto.
Para abrir o VSCode, basta digitar `code .` na pasta do projeto.

Dentro do VSCode, temos a opção de exibir o terminal. Nesse terminal, podemos rodar os comandos do Rails.

---

Antes de criar o banco, precisamos dizer ao Rails como se conectar ao MySQL (usuário e senha). Abra o arquivo `config/database.yml` e, dentro do bloco `default: &default`, adicione as linhas de usuário e senha:

```
default: &default
  adapter: mysql2
  encoding: utf8mb4
  max_connections: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: <- aqui vai o nome do usuário do MySQL: no caso da instalação local é root
  password: <- aqui vai a senha do MySQL: no caso da instalação local é também root
```

Agora sim, vamos criar o banco de dados que o projeto vai usar. Esse comando ainda não cria tabelas, só o banco em si.

```bash
rails db:create
```

Por fim, vamos ligar o servidor para ver o projeto rodando no navegador. Depois de rodar, acesse `http://localhost:3000`.

```bash
rails server
```

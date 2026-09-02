# Comandos

## Criar o projeto

Vamos criar um novo projeto Rails chamado `loja`. O `-d mysql` diz para o Rails usar o MySQL como banco de dados (sem isso, ele usaria o SQLite por padrão).

```bash
rails new loja -d mysql
```

Toda vez que criamos um projeto novo, o Rails gera uma pasta com esse nome. Precisamos entrar nela para continuar trabalhando.

```bash
cd loja
```

Agora vamos criar o banco de dados que o projeto vai usar. Esse comando ainda não cria tabelas, só o banco em si.

```bash
rails db:create
```

Por fim, vamos ligar o servidor para ver o projeto rodando no navegador. Depois de rodar, acesse `http://localhost:3000`.

```bash
rails server
```

# Comandos

## Criar a Categoria (com scaffold)
---
Agora vamos criar o cadastro de Categorias. Dessa vez, em vez de criar as coisas uma por uma, vamos usar o `scaffold`: um gerador do Rails que cria de uma vez só o model, o controller, as views (listar, criar, editar, ver e excluir) e as rotas. É a forma mais rápida de ter um CRUD completo funcionando.

O `name:string` diz que a Categoria vai ter um campo chamado `name`, do tipo texto.

```bash
rails generate scaffold Category name:string
```

---

O scaffold cria o código, mas ainda não mexe no banco de dados. Para isso existem as "migrations": arquivos que descrevem mudanças no banco (como criar uma tabela nova). O comando abaixo aplica essas mudanças pendentes, criando a tabela `categories` de verdade no banco.

```bash
rails db:migrate
```

---

Vamos ligar o servidor para ver o cadastro de categorias funcionando.

```bash
rails server
```

Agora, acesse `http://localhost:3000/categories`.

Pronto! Você já consegue criar, listar, editar e excluir categorias pelo navegador, sem ter escrito nenhuma linha de HTML.

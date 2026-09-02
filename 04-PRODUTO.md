# Comandos

## Criar o Produto (com scaffold e associação)
---
Agora vamos criar o cadastro de Produtos. Assim como fizemos com Categoria, vamos usar o `scaffold` para gerar tudo de uma vez: model, controller, views e rotas.

O Produto vai ter um `name` (texto curto), uma `description` (texto longo) e uma `category:references`. Esse `references` é o que cria a associação com Categoria: ele adiciona um campo `category_id` na tabela de produtos, ligando cada produto a uma categoria.

```bash
rails generate scaffold Product \
  name:string \
  description:text \
  category:references
```

---

Assim como antes, o scaffold só descreve a mudança no banco, mas não aplica. Vamos rodar a migration para criar a tabela `products` (já com o campo `category_id`).

```bash
rails db:migrate
```

---

O `references` já deixou o model `Product` sabendo que ele "pertence a" uma categoria (`belongs_to :category`). Mas o contrário — a Categoria saber quais produtos ela tem — precisa ser adicionado à mão. Abra o arquivo `app/models/category.rb` e adicione a linha `has_many :products`:

```ruby
class Category < ApplicationRecord
  has_many :products
end
```

Isso completa a associação nos dois sentidos: um Produto pertence a uma Categoria, e uma Categoria tem vários Produtos.

---

Vamos ligar o servidor (se ele já não estiver rodando) para ver o cadastro de produtos funcionando.

```bash
rails server
```

Agora, acesse `http://localhost:3000/products`. Repare que, no formulário de novo produto, já aparece um campo para escolher a categoria — o Rails criou isso automaticamente por causa da associação.

Pronto! Antes de cadastrar um produto, crie ao menos uma categoria em `http://localhost:3000/categories`, para poder escolhê-la no formulário.

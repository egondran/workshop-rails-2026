# Comandos

## Adicionar validações nos models

Até agora, se alguém deixar o campo "Nome" em branco e salvar, o Rails salva do mesmo jeito — não existe nenhuma regra impedindo isso, só o banco de dados aceitando o que chegar. Vamos usar `validates` para ensinar ao model que alguns campos são obrigatórios. Isso é feito no model, não na view nem no banco — é aqui que fica a regra de negócio no Rails.

---

### Validar a Categoria
---
Abra `app/models/category.rb` e adicione um `validates` dizendo que `name` precisa estar presente:

```ruby
class Category < ApplicationRecord
  has_many :products

  validates :name, presence: true
end
```

---

### Validar o Produto
---
Abra `app/models/product.rb` e faça o mesmo com `name`:

```ruby
class Product < ApplicationRecord
  belongs_to :category

  validates :name, presence: true
end
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e testar.

```bash
rails server
```

Agora, acesse `http://localhost:3000/categories/new` ou `http://localhost:3000/products/new` e tente salvar com o campo "Nome" em branco.

Pronto! Agora o Rails recusa salvar e mostra a mensagem de erro na tela — a mesma tela de erro que já existia no formulário desde o scaffold, só que agora ela tem algo para mostrar.

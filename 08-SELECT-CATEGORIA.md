# Comandos

## Trocar o campo de Categoria por um select

Até agora, o campo de categoria no formulário de Produto era um campo de texto onde a gente digitava o número (`id`) da categoria — nada amigável. Vamos trocar isso por uma lista suspensa (`select`), mostrando o nome de cada categoria em vez do número.

---

### Carregar as categorias no controller
---
Para o `select` funcionar, a view precisa de uma lista com todas as categorias disponíveis. Views não devem buscar dados sozinhas — quem faz isso é o controller. Vamos adicionar um `before_action` que carrega `@categories` antes das ações que usam o formulário (`new`, `edit`, `create` e `update`).

Abra `app/controllers/products_controller.rb` e adicione o `before_action` e o método `set_categories`:

```ruby
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update destroy ]
  before_action :set_categories, only: %i[ new edit create update ]

  # ...

  private
    # Use callbacks to share common setup or constraints between actions.
    def set_product
      @product = Product.find(params.expect(:id))
    end

    def set_categories
      @categories = Category.all
    end

    # Only allow a list of trusted parameters through.
    def product_params
      params.expect(product: [ :name, :description, :category_id ])
    end
end
```

---

### Mostrar o select no formulário
---
Agora, em vez do `form.text_field :category_id`, vamos usar `form.collection_select`. Ele monta o `<select>` automaticamente a partir de `@categories`: o `:id` é o valor que será salvo (`category_id`), e o `:name` é o texto que aparece para quem está preenchendo o formulário.

Repare também que a classe do Bootstrap para um `select` é `form-select`, e não `form-control`.

Abra `app/views/products/_form.html.erb` e troque o campo de categoria:

```erb
<div class="mb-3">
  <%= form.label :category_id, "Categoria", class: "form-label" %>
  <%= form.collection_select :category_id, @categories, :id, :name, {}, class: "form-select" %>
</div>
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e testar o formulário de novo produto.

```bash
rails server
```

Agora, acesse `http://localhost:3000/products/new`. Certifique-se de já ter pelo menos uma categoria cadastrada em `http://localhost:3000/categories` para ela aparecer na lista.

Pronto! O formulário de Produto agora mostra o nome das categorias em um select, em vez de pedir o número do id.

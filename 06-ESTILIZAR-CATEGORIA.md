# Comandos

## Usar classes do Bootstrap na view de Categoria

Agora que o Bootstrap está carregado, vamos trocar algumas tags simples por versões com classes do Bootstrap. A ideia é sempre a mesma: a tag continua fazendo o que fazia, só ganha um `class="..."` com o nome de um estilo pronto (`container`, `btn`, `form-control`, etc).

Vamos passar pelas quatro telas de Categoria: listagem, formulário, novo/editar e detalhes.

---

### Listagem (index)
---
A classe `container` centraliza o conteúdo e dá uma margem lateral — é a base de quase toda página com Bootstrap. Trocamos também o aviso verde por um `alert alert-success`, agrupamos os itens da lista com `list-group` e transformamos o link "New category" em um botão de verdade com `btn btn-primary`.

Abra `app/views/categories/index.html.erb`:

```erb
<div class="container mt-4">
  <% if notice %>
    <div class="alert alert-success"><%= notice %></div>
  <% end %>

  <h1>Categories</h1>

  <div id="categories" class="list-group mb-3">
    <% @categories.each do |category| %>
      <div class="list-group-item d-flex justify-content-between align-items-center">
        <%= render category %>
        <%= link_to "Ver", category, class: "btn btn-sm btn-outline-primary" %>
      </div>
    <% end %>
  </div>

  <%= link_to "New category", new_category_path, class: "btn btn-primary" %>
</div>
```

---

### Formulário (_form)
---
No formulário, cada campo ganha `form-label` (no label) e `form-control` (no input), e envolvemos cada campo em uma `div class="mb-3"` para dar espaçamento entre eles. Os erros de validação também ganham a cor de alerta certa, `alert alert-danger`.

Abra `app/views/categories/_form.html.erb`:

```erb
<%= form_with(model: category) do |form| %>
  <% if category.errors.any? %>
    <div class="alert alert-danger">
      <h2><%= pluralize(category.errors.count, "error") %> prohibited this category from being saved:</h2>
      <ul class="mb-0">
        <% category.errors.each do |error| %>
          <li><%= error.full_message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="mb-3">
    <%= form.label :name, class: "form-label" %>
    <%= form.text_field :name, class: "form-control" %>
  </div>

  <div>
    <%= form.submit class: "btn btn-primary" %>
  </div>
<% end %>
```

---

### Novo e Editar (new e edit)
---
Essas duas telas só chamam o formulário, então basta envolver tudo em um `container` e transformar o link de volta em botão.

Abra `app/views/categories/new.html.erb`:

```erb
<div class="container mt-4">
  <h1>New category</h1>

  <%= render "form", category: @category %>

  <div class="mt-3">
    <%= link_to "Back to categories", categories_path, class: "btn btn-outline-secondary" %>
  </div>
</div>
```

Abra `app/views/categories/edit.html.erb`:

```erb
<div class="container mt-4">
  <h1>Editing category</h1>

  <%= render "form", category: @category %>

  <div class="mt-3">
    <%= link_to "Show this category", @category, class: "btn btn-outline-secondary" %>
    <%= link_to "Back to categories", categories_path, class: "btn btn-outline-secondary" %>
  </div>
</div>
```

---

### Detalhes (show)
---
Aqui usamos um `card`, outro componente clássico do Bootstrap, para destacar as informações da categoria. Os botões de ação (editar, voltar, excluir) ganham cores diferentes para indicar o que cada um faz — o `btn-danger` (vermelho) para a ação de excluir é uma convenção bem comum.

Abra `app/views/categories/show.html.erb`:

```erb
<div class="container mt-4">
  <% if notice %>
    <div class="alert alert-success"><%= notice %></div>
  <% end %>

  <div class="card">
    <div class="card-body">
      <%= render @category %>
    </div>
  </div>

  <div class="mt-3">
    <%= link_to "Edit this category", edit_category_path(@category), class: "btn btn-secondary" %>
    <%= link_to "Back to categories", categories_path, class: "btn btn-outline-secondary" %>
    <%= button_to "Destroy this category", @category, method: :delete, class: "btn btn-danger" %>
  </div>
</div>
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e recarregar a página de categorias para ver o resultado.

```bash
rails server
```

Agora, acesse `http://localhost:3000/categories`.

Pronto! A tela de Categoria agora usa componentes do Bootstrap: `container`, `list-group`, `card`, `btn` e `form-control`.

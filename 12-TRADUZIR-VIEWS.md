# Comandos

## Usar o t() em algumas views

Já preparamos as traduções no `pt-BR.yml`, mas elas só têm efeito onde chamamos o helper `t()` (ou `translate`) na view, passando o caminho da chave. Não vamos traduzir as 8 telas (novo/editar/detalhes/voltar de Categoria e Produto) — o objetivo aqui é só mostrar o `t()` funcionando em alguns lugares. O padrão é sempre o mesmo, então dá para repetir depois nas outras views com calma.

---

### Título e link de "New product"
---
No título (`content_for :title`) e no link de voltar, troque o texto fixo em inglês por `t("products.new")` e `t("products.back")` — as mesmas chaves que já criamos no `pt-BR.yml`.

Abra `app/views/products/new.html.erb`:

```erb
<div class="container mt-4">
  <% content_for :title, t("products.new") %>

  <h1><%= t("products.new") %></h1>

  <%= render "form", product: @product %>

  <div class="mt-3">
    <%= link_to t("products.back"), products_path, class: "btn btn-outline-secondary" %>
  </div>
</div>
```

---

### Links de "editar produto"
---
Aqui usamos duas chaves diferentes: `products.edit` para o título e `products.show`/`products.back` para os links.

Abra `app/views/products/edit.html.erb`:

```erb
<div class="container mt-4">
  <% content_for :title, t("products.edit") %>

  <h1><%= t("products.edit") %></h1>

  <%= render "form", product: @product %>

  <div class="mt-3">
    <%= link_to t("products.show"), @product, class: "btn btn-outline-secondary" %>
    <%= link_to t("products.back"), products_path, class: "btn btn-outline-secondary" %>
  </div>
</div>
```

---

### O mesmo padrão em Categoria
---
As chaves de Categoria seguem exatamente a mesma ideia, só trocando `products` por `categories`. Vamos aplicar só no `new`, como exemplo:

Abra `app/views/categories/new.html.erb`:

```erb
<div class="container mt-4">
  <% content_for :title, t("categories.new") %>

  <h1><%= t("categories.new") %></h1>

  <%= render "form", category: @category %>

  <div class="mt-3">
    <%= link_to t("categories.back"), categories_path, class: "btn btn-outline-secondary" %>
  </div>
</div>
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e conferir as telas que traduzimos.

```bash
rails server
```

Agora, acesse `http://localhost:3000/products/new`, `http://localhost:3000/products/1/edit` e `http://localhost:3000/categories/new`.

Pronto! Essas três telas já usam `t()`. As demais (show, edit de categoria, etc) continuam com texto fixo em inglês por enquanto — dá pra aplicar o mesmo padrão nelas depois, com calma, usando as chaves que já deixamos prontas no `pt-BR.yml`.

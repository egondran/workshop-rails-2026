# Comandos

## Criar a navbar do layout

Vamos colocar um menu de navegação no topo de todas as páginas, com links para Home, Categorias e Produtos. Como esse menu fica no layout (`application.html.erb`), ele aparece automaticamente em qualquer página do site, sem precisar repetir código.

Vamos usar o componente `navbar` do Bootstrap. Como não estamos usando o JavaScript do Bootstrap, vamos usar a classe `navbar-expand` (sem o botão de "hambúrguer" para celular, que depende de JS) — o menu fica sempre visível, só quebrando linha em telas bem pequenas.

---

### Adicionar a navbar no layout
---
Abra `app/views/layouts/application.html.erb` e adicione a navbar logo no início do `<body>`, antes do `<%= yield %>`:

```erb
<body>
  <nav class="navbar navbar-expand navbar-dark bg-dark mb-4">
    <div class="container">
      <%= link_to "Loja", root_path, class: "navbar-brand" %>
      <div class="navbar-nav">
        <%= link_to "Home", root_path, class: "nav-link" %>
        <%= link_to "Categorias", categories_path, class: "nav-link" %>
        <%= link_to "Produtos", products_path, class: "nav-link" %>
      </div>
    </div>
  </nav>

  <%= yield %>
</body>
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e navegar pelo site para ver a navbar em ação.

```bash
rails server
```

Agora, acesse `http://localhost:3000` e clique nos links do menu.

Pronto! Agora todas as páginas têm um menu no topo para navegar entre Home, Categorias e Produtos.

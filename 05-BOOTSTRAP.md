# Comandos

## Adicionar o Bootstrap (via CDN)
---
Para deixar as telas mais bonitas sem precisar escrever muito CSS, vamos usar o Bootstrap. Em vez de instalar qualquer coisa, vamos usar a versão hospedada na internet (CDN): basta colar um link no layout do projeto e o Bootstrap já fica disponível em todas as páginas.

Vamos usar só a parte de CSS do Bootstrap (as classes prontas, como `container`, `btn`, `table`, etc). Não vamos usar a parte de JavaScript dele, então não precisamos do script, só do `<link>`.

Abra o arquivo `app/views/layouts/application.html.erb` e adicione a linha do Bootstrap dentro do `<head>`, antes do `stylesheet_link_tag`:

```html
<head>
  <title><%= content_for(:title) || "Loja" %></title>
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <%= csrf_meta_tags %>
  <%= csp_meta_tag %>

  <%= yield :head %>

  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

  <%# Includes all stylesheet files in app/assets/stylesheets %>
  <%= stylesheet_link_tag :app, "data-turbo-track": "reload" %>
</head>
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e recarregar qualquer página do site para ver o efeito.

```bash
rails server
```

Pronto! As páginas já carregam com as fontes e os espaçamentos padrão do Bootstrap. Nos próximos passos, vamos usar classes do Bootstrap (como `container`, `btn`, `btn-primary`, `table`) para deixar as telas de Categoria e Produto mais bonitas.

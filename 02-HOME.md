# Comandos

## Criar a home page
---
Vamos criar uma página inicial (home page) para o nosso site. No Rails, cada página geralmente tem um "controller" (que decide o que mostrar) e uma "view" (o HTML que é exibido). Esse comando cria os dois já prontos, com uma ação chamada `index`.

```bash
rails generate controller Home index
```

---

Agora precisamos dizer ao Rails que essa página é a primeira que deve aparecer quando alguém acessa o site (a rota raiz, `/`). Abra o arquivo `config/routes.rb` e adicione a linha `root "home#index"` dentro do bloco de rotas:

```ruby
Rails.application.routes.draw do
  root "home#index"

  get "home/index"
end
```

---

O HTML da nossa home page fica no arquivo `app/views/home/index.html.erb`. Abra esse arquivo e troque o conteúdo por algo nosso:

```html
<h1>Bem-vindo à Loja!</h1>
<p>Os melhores produtos você encontra aqui.</p>
```

---

Vamos ligar o servidor de novo para ver a home page no navegador.

```bash
rails server
```

Agora, acesse `http://localhost:3000`.

Pronto! Agora a home page da loja está no ar.

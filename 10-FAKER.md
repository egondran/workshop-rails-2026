# Comandos

## Popular o banco com a gem Faker

Cadastrar categorias e produtos um por um pelo navegador é chato para testar o site. Vamos usar a gem `faker`, que gera dados falsos (nomes, textos, preços, etc), e criar uma tarefa que cadastra várias categorias e produtos de uma vez.

---

### Adicionar a gem Faker
---
Abra o `Gemfile` e adicione a gem `faker` dentro do grupo `:development, :test` (ela só precisa existir enquanto estamos desenvolvendo, não em produção):

```ruby
group :development, :test do
  # ...

  # Gera dados falsos (nomes, textos, etc) para popular o banco em desenvolvimento
  gem "faker"
end
```

Depois de adicionar a gem no `Gemfile`, precisamos instalá-la:

```bash
bundle install
```

---

### Criar a task de popular o banco
---
No Rails, tarefas que rodam pelo terminal (fora do navegador) ficam em arquivos `.rake`, dentro de `lib/tasks`. Vamos criar uma task chamada `db:populate` que cria algumas categorias e, para cada categoria, alguns produtos.

Crie o arquivo `lib/tasks/populate.rake` com o seguinte conteúdo:

```ruby
namespace :db do
  desc "Popula o banco com categorias e produtos de exemplo"
  task populate: :environment do
    categories = 5.times.map do
      Category.create!(name: Faker::Commerce.department)
    end

    30.times do
      Product.create!(
        name: Faker::Commerce.product_name,
        description: Faker::Lorem.sentence,
        category: categories.sample
      )
    end

    puts "Criadas #{Category.count} categorias e #{Product.count} produtos!"
  end
end
```

O `task populate: :environment` diz para o Rails carregar toda a aplicação antes de rodar a task — é isso que nos dá acesso aos models `Category` e `Product` dentro dela.

---

### Rodar a task
---
```bash
rails db:populate
```

---

Vamos ligar o servidor (se ele já não estiver rodando) e conferir os dados criados.

```bash
rails server
```

Agora, acesse `http://localhost:3000/categories` e `http://localhost:3000/products`.

Pronto! O banco já está populado com categorias e produtos de exemplo, prontos para testar o site.

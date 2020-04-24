# Setup Inicial

Nesta aula vamos configurar nosso projeto para operar com RSpec para testes e conectar ao Postgres



**1- Adicione no seu Gemfile dentro do bloco ‘group :development, :test’**

```
gem 'rspec-rails', '~> 4.0'
```



**2- Instale as gems:**

```
bundle install
```



**3- Para configurar o RSpec, execute o seguinte comando**

```shell
docker-compose run --rm app bundle exec rails g rspec:install
```



**4- Como ele cria a pasta `specs`, podemos apagar o a pasta `test` do nosso diretório**

```shell
rm -r test
```



**5- Altere seu arquivo config/database.yml para:**

```yaml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  host: db
  user: postgres
  password: <%= ENV['DB_PASSWORD'] %>


development:
  <<: *default
  database: onebit_exchange_development


test:
  <<: *default
  database: onebit_exchange_test
 

production:
  <<: *default
  database: onebit_exchange_production
  username: onebit_exchange
```



**6- Vamos criar nosso database:**

```
docker-compose run --rm app bundle exec rails db:create db:migrate
```



**8- Por último, vamos iniciar o servidor e testar no nosso navegador**

```shell
docker-compose up
```

> Acesse o navegador em **http://localhost:3000**



**BRANCH**: _setup_
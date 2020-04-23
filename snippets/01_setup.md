# Setup Inicial



**1- Vamos criar nosso projeto, dentro da pasta desejada, rode no terminal os comandos a baixo:**

```
gem install rails -v 6.0.2.2
rails new onebit_exchange --database=postgresql
cd onebit_exchange
```



**2- Adicione no seu Gemfile dentro do bloco ‘group :development, :test’**

```
gem 'rspec-rails', '~> 4.0'
```



**3- Instale as gems:**

```
bundle install
```



**4- Altere seu arquivo config/database.yml para:**

```
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  host: localhost
  user: postgres
  password: postgres


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
  password: <%= ENV['EXCHANGE_DATABASE_PASSWORD'] %>
```



**5- Vamos criar nosso database:**

```
rails db:create db:migrate
```



**6- Por último, vamos iniciar o servidor e testar no nosso navegador**

```shell
rails s
```

> Acesse o navegador em **http://localhost:3000**



**BRANCH**: _setup_
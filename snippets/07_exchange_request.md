# Exchange Request

Nesta aula modificaremos o controller para que ele responda às rotas que colocamos nos testes



**1- Altere seu routes.rb para:**

```ruby
Rails.application.routes.draw do
  root 'exchanges#index'
  get 'convert', to: 'exchanges#convert'
end
```



**2- No seu ExchangesController substitua o conteúdo por.**

```ruby
class ExchangesController < ApplicationController
  def index
  end

  def convert
    value = ExchangeService.new(params[:source_currency], params[:target_currency], params[:amount]).call
    render json: {"value": value}
  end
end
```



**3- Rode o teste de request novamente:**

```shell
rspec spec/requests/exchanges_request_spec.rb
```

> Com as rotas ajustadas e controller preenchido, nosso teste passou



**4- Suba o servidor do Rails e teste a rota raiz**

```
rails s
```

> Para testar, acesse **http://localhost:3000** no seu navegador. Ele vai aparecer uma página apenas com titulo já que ainda não construímos nossa página



**BRANCH:** *exchange_request*
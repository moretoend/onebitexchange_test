# Exchange Request Teste

Nesta aula faremos o teste para o request de conversão de moeda



**1- Rode no seu terminal:**

```shell
docker-compose run --rm app bundle exec rails g controller Exchanges index convert --no-controller-specs --no-helper-specs --no-view-specs
```

> Deixaremos que ele crie apenas os testes de request



**2- No seu arquivo exchanges_spec.rb substitua o conteúdo por:**

```ruby
require 'rails_helper'

 
RSpec.describe 'Exchanges', type: :request do
  describe 'GET #index' do
    it 'returns http success' do
      get '/'
      expect(response).to have_http_status(200)
    end
  end


  describe 'GET #convert' do
    before do
      @amount = rand(1..9999)
    end
 
    it 'returns http success' do
      get '/convert', params: {
                        source_currency: "USD",
                        target_currency: "BRL",
                        amount: @amount
                      }
      expect(response).to have_http_status(200)
    end
  end
end
```



**3-Rode o teste:**

```shell
docker-compose run --rm app bundle exec rspec spec/requests/exchanges_request_spec.rb
```



**BRANCH**: *exchange_request_spec*
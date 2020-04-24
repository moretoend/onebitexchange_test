# Exchange Service Teste

Nesta aula faremos o teste para um serviço ExchangeService que criaremos posteriormente



**1- Adicione ao Gemfile:**

```ruby
gem 'rest-client'
```



**2- Instale com o comendo:**

```shell
docker-compose run --rm app bundle install
```



**3- Agora crie uma pasta chamada `specs/services` e dentro dela um arquivo chamado exchange_service_spec.rb:**

```shell
mkdir spec/services
touch spec/services/exchange_service_spec.rb
```



**4- Adicione o seguinte conteúdo em `spec/services/exchange_service_spec.rb`**

```ruby
require 'rails_helper'
require 'json'
require './app/services/exchange_service'

describe ExchangeService do
  let(:source_currency) { "USD" }
  let(:target_currency) { "BRL" }
  let(:exchange_value) { 3.4546 }
  let(:api_return) do
    {
      currency: [
        {
          currency: "#{source_currency}/#{target_currency}",
          value: exchange_value,
          date: Time.now,
          type: "Original"
        }
      ]
    }
  end

  before do
    allow(RestClient).to receive(:get) { OpenStruct.new(body: api_return.to_json) }
  end

  it "#call" do
    amount = rand(0..9999)
    service_exchange = ExchangeService.new("USD", "BRL", amount).call
    expected_exchange = amount * exchange_value
    expect(service_exchange).to eq expected_exchange
  end
end
```



**5- Rode o teste (irá falhar):**

```shell
docker-compose run --rm app bundle exec rspec spec/services/exchange_service_spec.rb
```



**BRANCH**: *service_spec*
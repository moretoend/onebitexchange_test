# Exchange Service

Nesta aula vamos construir o serviço de conversão



**1- Dentro da sua pasta app/services e dentro dele um arquivo exchange_service.rb**

```shell
mkdir app/services
touch app/services/exchange_service.rb
```



**2- Adicione o seguinte conteúdo em `app/services/exchange_service.rb`**

```ruby
require 'rest-client'
require 'json'

class ExchangeService
  def initialize(source_currency, target_currency, amount)
    @source_currency = source_currency
    @target_currency = target_currency
    @amount = amount.to_f
  end

  def call
    begin
      value = get_exchange
      value * @amount
    rescue RestClient::ExceptionWithResponse => e
      e.response
    end
  end
    
  private

  def get_exchange
    exchange_api_url = Rails.application.credentials[:currency_api_url]
    exchange_api_key = Rails.application.credentials[:currency_api_key]
    url = "#{exchange_api_url}?token=#{exchange_api_key}&currency=#{@source_currency}/#{@target_currency}"
    res = RestClient.get url
    JSON.parse(res.body)['currency'][0]['value'].to_f
  end
end
```



**3 - Vamos entrar no console para testar**

```shell
rails c
```



**4- E vamos testar a conversão de R$10 em Euros**

```ruby
ExchangeService.new('BRL', 'EUR', 10).call
```

> No momento atual, como Euro valendo R$5,894, o resultado foi como 1.696



**5 - Por fim, rode novamente o nosso teste de service:**

```shell
rspec spec/services/exchange_service_spec.rb
```

> Como serviço feito, desta vez nossos testes estão passando = )



**BRANCH**: *exchange_service*
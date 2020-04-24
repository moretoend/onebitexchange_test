# Preparando página Index

Nesta aula vamos construir a nossa página de conversão



**1- Suba as imagens dos links abaixo na sua pasta public rodando:**

```shell
curl https://onebitcode.com/wp-content/uploads/2018/06/logo.png > app/assets/images/logo.png

curl https://onebitcode.com/wp-content/uploads/2018/06/favicon.png > app/assets/images/favicon.png

curl https://onebitcode.com/wp-content/uploads/2018/06/background-img.jpg > app/assets/images/background-img.jpg
```



**2- No arquivo app/views/layout/application.html.erb adicione ao header:**

```erb
<%= favicon_link_tag 'favicon.png' %>
```



**3- Dentro do arquivo index nas views do Exchange coloque: (`app/views/exchanges/index.html.erb`)**

```erb
<div class='container'>
  <div class='row main'>
    <div class='col-lg-3 offset-lg-1 col-md-10 offset-md-1 exchange_box'>
      <div class='row'>
          <div class='col-md-8 offset-md-2 text-sm-center'>
            <%= image_tag 'logo.png', class: 'img-fluid'%>
          </div>
      </div>

      <div class='row'>
        <%= render 'exchange_box' %>
      </div>
    </div>

    <div class='col-lg-7 offset-lg-1 hidden-sm-down title-box'>
      <div class='row'>
        <h2 class='subtitle'>Converta facilmente suas Moedas</h2>
      </div>
                
      <div class='row'>
        <h3 class='subtitle'>Para qualquer moeda no Mundo!</h3>
      </div>
    </div>
  </div>
</div>
```



**4- Altere seu arquivo exchanges.scss para:**

```scss
body {
  background: image-url(asset-path("background-img.jpg")) no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.main{
  margin-top: 50px;
}


.title-box{
  margin-top: 20%;

  .title{
    color: white;
    text-shadow: 2px 0px 2px #000000;
  }

  .subtitle{
    color: white;
    text-shadow: 3px 0px 3px #000000;
    font-size: 30px;
    margin-left: 10px;
    margin-right: 10px;
  }
}

 
.exchange_box{
  margin: 10px auto;
  .logo-box{
    margin: 0 auto;
    padding-bottom: 10px;
  }
}
```



**5- Dentro da pasta `app/views/exchanges` crie um arquivo chamado `_exchange_box.html.erb`**

```shell
touch app/views/exchanges/_exchange_box.html.erb
```



**6- Acrescente em `app/views/exchanges/_exchange_box.html.erb**

 ```erb
<div class='exchange_box col-sm-12'>
  <div class='card'>

    <div class='card-header text-center'>
      Simule sua conversão
    </div>

    <div class='card-block'>
      <%= form_with url: "/convert", method: :get, id: 'exchange_form' do |f| %>
        <div class='local_currency'>
          <div class='form-group'>
            <p class='title'>Moeda Local</p>
            <%= f.select 'source_currency', options_for_select(currency_list, 'BRL'), {}, { class: 'form-control', id: 'source_currency' } %>
          </div>

          <div class='form-group'>
            <%= f.number_field 'amount', id: 'amount', class: 'form-control', placeholder: 'Quantidade ($10)', step: 'any', required: true %>
          </div>
        </div>
                    
        <div class='destination_currency'>
          <div class='form-group'>
            <p class='title'>Moeda Pretendida</p>
            <%= f.select 'target_currency', options_for_select(currency_list, 'EUR'), {}, { class: 'form-control', id: 'target_currency' } %>
          </div>
          <div class='form-group'>
            <input type='text' id='result' name='result' class='form-control' placeholder='Resultado' readonly>
          </div>
        </div>
        <div>
          <%= f.submit "CONVERTER", class: 'btn btn-primary btn-exchange col-md-12' %>
        </div>
      <% end %>
    </div>
  </div>
</div>
 ```



**7- Crie um arquivo `app/assets/stylesheets/_exchange_box.scss` **

```shell
touch app/assets/stylesheets/_exchange_box.scss
```



**8- Acrescente em `app/assets/stylesheets/_exchange_box.scss`**

```scss
.exchange_box{

  .card{
    border: 0;

    .card-header{
      background-color: #878d99;
      border-radius: 0;
      color: white;
      font-weight: 700;
    }

    .card-block{
      padding-top: 10px;
      padding: 20px;

      .title{
        color: #878d99;
        font-weight: 700;
      }

      .btn-exchange{
        background-color: #5bc0de;
        border-color: #5bc0de;
        border-radius: 0;
      }
    }
  }
}

@media only screen and (max-width : 992px) {
  .card-header {
    font-size: 25px;
  }

  .title{
    margin-top: 30px;
    font-size: 20px;
  }
    
  .form-group {
    select {
      font-size: 20px;
      height: 50px !important;
    }

    input {
      font-size: 20px;
      height: 50px;
    }
  }


  #result {
    margin-bottom: 20px;
  }

  .btn-exchange {
    font-size: 20px;
  }
}
```



**9- No arquivo app/assets/stylesheets/application.scss coloque:**

```scss
@import 'exchanges';
@import '_exchange_box';
```



**10- Atualize o conteúdo do `app/helpers/helper _exchanges_helper.rb` com o seguinte conteúdo:**

```ruby
module ExchangesHelper
 
  def currency_list
    [
      'AUD', 'BGN', 'BRL', 'CAD', 'CHF', 'CNY', 'CZK', 'DKK', 'EUR', 'GBP',
      'HKD', 'HRK', 'HUF', 'IDR', 'ILS', 'INR', 'JPY', 'KRW', 'MXN',
      'MYR', 'NOK', 'NZD', 'PHP', 'PLN', 'RON', 'RUB', 'SEK', 'SGD',
      'THB', 'TRY', 'USD', 'ZAR'
    ]
  end
end
```

> Esse helper já foi criado antes com o generate do controller.



**11- Para implementar a responsividade no site, atualize o application.html.erb colocando:**

```erb
<!DOCTYPE html>
<html>
  <head>
    <title>OneBitExchangeDev</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= favicon_link_tag 'favicon.png' %>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```



**12- Rode o teste:**

```shell
docker-compose run --rm app bundle exec rspec spec/requests/exchanges_request_spec.rb
```



**BRANCH:** *index_page*
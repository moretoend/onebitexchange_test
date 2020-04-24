# Incluíndo o Javascript

Nesta aula vamos acrescentar o javascript que será responsável por recepcionar a resposta do servidor



**1- Crie um arquivo `app/javascript/packs/exchanges.js`**

```shell
touch app/javascript/packs/exchanges.js 
```



**2- Adicione o seguinte conteúdo em `app/javascript/packs/exchanges.js`**

```javascript
document.addEventListener('turbolinks:load', function(){
  document.getElementById('exchange_form').addEventListener('ajax:success', function(event) {
    let [result] = event.detail
    document.getElementById('result').value = result.value
  })
})
```



**3- Importe o arquivo em `app/javascript/packs/application.js`**

```javascript
require('./exchanges')
```



**4- Execute todos os testes**

```shell
docker-compose run --rm app bundle exec rspec
```

> Todos os testes estarão passando = )



**BRANCH:** *include_js*
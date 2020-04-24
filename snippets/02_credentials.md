# Credentials

Nesta aula vamos utilizar o "credentials" do Rails para armazenar nossa chave de conexão da nossa API de forma segura



**1- Primeiro vamos abrir o editor do arquivo de credenciais**

```shell
docker-compose run --rm -e EDITOR=nano app bundle exec rails credentials:edit
```

> O Rails possui o um arquivo `config/credentials.yml.enc` que é um arquivo criptografado utilizado para armazenar dados sensíveis como chaves de APIs
>
> Quando executamos este comando, o Rails pega a chave de criptogradia que está no arquivo `config/master.key`, descriptografa este arquivo e abre no editor que enviamos no "EDITOR". Quando fechamos, ele recriptografa.
>
> Por isso, podemos sempre comitar o arquivo `config/credentials.yml.key`. Mas NÃO podemos fazer o mesmo como  `config/master.key`



**2- Ao abrir o editor apague o conteúdo do arquivo e cole o conteúdo a baixo usando o “ctrl + shift + v”**

```
secret_key_base: <sua_secret_key>

currency_api_key: <sua_api_key>
currency_api_url: https://currencydatafeed.com/api/data.php
```

> Quando vc abre o arquivo, ele já vem com o `secret_key_base`. Deixe como está.
>
> Onde temos o `<sua_api_key>`, coloque a chave do Currency Data Feed que está na sua conta que pegamos na aula anterior.
>
> Nós poderíamos também ter feito uma separação por ambiente, mas como utilizaremos a mesma chave de API para os 3 ambientes de desenvolvimento, teste e produção, deixaremos desta forma



**3- Agora basta salvar e fechar o editor que o arquivo será recriptografado**



**BRANCH**: *credentials*
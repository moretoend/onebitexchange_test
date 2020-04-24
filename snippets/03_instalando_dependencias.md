# Instalando Dependências

Nesta aula vamos instalar as dependencias do frontend com o Yarn



**1- Agora vamos instalar o bootstrap no nosso projeto:**

```shell
docker-compose run --rm app bundle exec yarn add bootstrap
```



**2- Agora renomeie o arquivo app/assets/application.css para application.scss**



**3- Substitua o conteúdo do novo arquivo `app/assets/stylesheets/application.scss por:**

```
@import "bootstrap/dist/css/bootstrap.css";
```



**BRANCH:** *frontend_dependencies*
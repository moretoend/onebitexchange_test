# Instalando Dependências

Nesta aula vamos instalar as dependencias do frontend com o Yarn



**1- Vamos instalar o jQuery rodando:**

```
yarn add jquery
```



**2- Agora temos que importá-lo no nosso `app/javascript/pack/application.js`. Adicione a seguinte linha no seu arquivo:**

```javascript
...

import 'jquery'
```



**3- Agora vamos instalar o bootstrap no nosso projeto:**

```
yarn add bootstrap
```



**4- Agora renomeie o arquivo app/assets/application.css para application.scss**



**5- Substitua o conteúdo do novo arquivo `app/assets/stylesheets/application.scss por:**

```
@import "bootstrap/dist/css/bootstrap.css";
```



**6- No application.js acrescente:**

```javascript
...
import 'bootstrap/dist/js/bootstrap'
```



**BRANCH:** *frontend_dependencies*
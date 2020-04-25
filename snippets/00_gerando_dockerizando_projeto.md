# Gerando e Dockerizando o Projeto



**1- Vamos criar nosso projeto, dentro da pasta desejada, rode no terminal os comandos a baixo:**

```shell
docker run --rm --user "$(id -u):$(id -g)" -v $(pwd):/usr/src -w /usr/src -ti ruby:2.6.5 bash
gem install rails -v 6.0.2.2
rails new onebit_exchange --database=postgresql --skip-bundle
exit
cd onebit_exchange
```



**2- Agora vamos configurar o docker, na raiz do projeto crie um arquivo chamado Dockerfile e insira o conteúdo:**

```
FROM ruby:2.6.5

# add nodejs and yarn dependencies for the frontend
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Instalar nossas dependencias
RUN apt-get update && apt-get install -qq -y --no-install-recommends \
nodejs yarn build-essential libpq-dev imagemagick git-all nano

# Instalar Chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

# Instalar bundler
RUN gem install bundler

# Seta nosso path
ENV INSTALL_PATH /onebitexchange

# Cria nosso diretório
RUN mkdir -p $INSTALL_PATH

# Seta o nosso path como o diretório principal
WORKDIR $INSTALL_PATH

# Copia o nosso Gemfile para dentro do container
COPY Gemfile ./

# Seta o path para as Gems
ENV BUNDLE_PATH /gems

# Copia nosso código para dentro do container
COPY . .
```



**3- Agora crie também na raiz do projeto o arquivo docker-compose.yml e insira nele:**

```yaml
version: "3.8"

services:
  db:
    image: "postgres:12.2"
    environment:
      - POSTGRES_PASSWORD=postgres
    volumes:
      - postgres:/var/lib/postgresql/data

  app:
    build: .
    command: bash start.sh
    ports:
      - "3000:3000"
    environment:
      - DB_PASSWORD=postgres
    volumes:
      - .:/onebitexchange
      - gems:/gems
 

volumes:
  postgres:
  gems:
```



**4- Crie agora um arquivo chamado start.sh**

```shell
# Instala as Gems
bundle check || bundle install

# Roda nosso servidor
bundle exec puma -C config/puma.rb
```



**5- Para construir a imagem do ambiente rode:**

```shell
docker-compose build
```



**Obs: Caso seus comandos docker só funcionem usando o sudo antes, rode no console os seguintes comando para concertar:**

```shell
sudo groupadd docker
sudo usermod -aG docker $USER
sudo service docker restart
```


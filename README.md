# Star Wars API (front)

Este projeto é o front do [Star Wars API](https://github.com/alynnefs/star-wars-back). As informações detalhadas estão descritas lá.

## Executando com Docker

Para criar a imagem do docker, execute o seguinte comando na raiz do projeto:

```
docker build -t sw-front .
```

O resultado deverá ser

![](https://i.imgur.com/6jBTBmc.png)


Após criada, execute o container com:

```
docker run -it -p 8080:8080 --rm --name sw-front-1 sw-front
```

A saída deverá ser semelhante a esta:

![](https://i.imgur.com/DZbmJ8o.png)

Como o servidor fica "aberto", não é tão necessário verificar o container. Mas caso queira olhar mesmo assim, basta usar o comando `docker container ls`. A saída deverá ser parecida com essa:

![](https://i.imgur.com/hsBZZT4.png)


## Executando localmente

## Especificações usadas no desenvolvimento
- NPM: 9.2.0
- Vue/cli: 5.0.8

## Como instalar

```sh
npm install
```

### Como executar localmente

```sh
npm run dev
```

### Como compilar paraa produção

```sh
npm run build
```

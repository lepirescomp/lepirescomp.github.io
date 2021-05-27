---
layout: post
title:  🇧🇷 "Comandos que ajudam no debugging de docker containers"
date:   2021-05-26 14:04:26 -0300
categories: jekyll update
---

Docker containers são uma maneira de simplificar o deploy de aplicações, assim como o desenvolvimento, já que eles englobam as dependências do projeto em questão. No entanto, há um maior desafio no debugging 
de containers. 

Aqui vou deixar alguns dos comandos que mais me ajudam no dia a dia:

## IDs dos docker processess


```sh
docker ps
```

Encontrar o id do container é necessário em várias etapas quando estamos usando containers.

![image](../../../../../../images/post_docker/docker_ps.jpeg)

## Log do container

```sh
docker logs
```

Esse comando, por exemplo, indicar um erro em um arquivo que impediu a aplicação de rodar.

![image](../../../../../../images/post_docker/docker_ps.jpeg)

## Detalhes dos docker objects

```sh
docker inspect
```

Com o docker inspect, é possível identificar o estado do container, a data de criação e outras informações mais detalhadas.

![image](../../../../../../images/post_docker/docker_inspection.jpeg)

## Para entrar na linha de comando do docker container

```sh
docker exec -it sh
````

Esse comando permite que se entre na aplicação e interaja com a mesma por dentro do docker.

![image](../../../../../../images/post_docker/docker_exec.jpeg)






27/04/2021 - 6h30
[Repositório dos Exemplos](https://github.com/codeedu/fullcycle2.0-devops-docker)
# Iniciando com Docker

* docker ps - lista containers;
* docker run hello-world;
* docker ps -a - lista containers ativos e inativos;
* docker run -it ubuntu:latest bash - parâmetros (-it) sempre depois do run;
	* -i - modo interativo - bash no terminal;
	* -t - tty - permite rodar comandos no terminal;
	* bash - comando executado na imagem;
	* --rm - ao sair do container, é removido do histórico;
	* -p - publish na porta do seu computador que quer utilizar (8080:80 - PC:Container);
	* -d - detach terminal do processo - terminal não fica preso;
	* --name nomeia o container;
	* -v "$(pwd)"/html:/target/path/to/html - monta volume (cria pasta inexistente);
	* --mount type=bind, source="$(pwd)"/html, target=/path/to/html (não cria pasta inexistente);
* docker ps -a -q - Lista id's dos containers;
* docker rm $(docker ps -a -q) -f - remove todos containers da lista (ativos e inativos);


* docker rm - remove containers;
	* -f - force - força a remoção;

* docker exec <container_name> - executa um comando no container;
	* docker exec <container_name> -it bash;

* docker volume ls;

* docker volume create <volume_name>;

# Desafio Imagem Hello GO Lang:

* ```$ docker build -t juniorgunner/codeeducation .```

# Trabalhando com Imagens

* Overlay filesystem - camadas que já existem não são baixadas novamente;
* docker images - lista imagens;
* docker pull <php:rc-alpine>;
* docker rmi <image_name> - remove imagem;

* Dockerfile:
	- FROM ubuntu:latest (baseImage) - imagem de origem;
	- RUN apt-get update - executa comando;
	- RUN apt-get install vim -y;
	- WORKDIR /the/workdir/path - caminho do projeto*;
	- RUN apt-get update && \
		apt-get install vim -y;
	- COPY html /usr/share/nginx - copia para dentro do container;
	- USER (por padrão entra como root);

* docker build -t <tag_da_imagem/nome_da_imagem:latest .> - Ponto indica pasta atual;


# ENTRYPOINT vs CMD

	- CMD ["echo", "Hello World"] - consigo substituir o comando na hora de
		executar (run) a imagem - comando variável (parâmetro do entrypoint);
	- ENTRYPOINT ["echo", "Hello"] - comando fixo;
	- ENV X 123 - variável de ambiente;
	- exec "S@" - executa parâmetro passado após entrypoint.sh;


# NETWORKS

* TIPOS:
	- bridge - utilizada para um container se comunicar com outro;
	- host - mescla a network do docker com o host (máquina local);
	- overlay - containers em máquinas diferentes (docker swarm - cluster - escalável);
	- macvlan - adiciona mac address ao container para identificar na rede local;
	- none - container roda de forma isolada, sem fazer parte de uma rede;

* docker network - lista comandos;
* docker network ls - lista networks;
* docker network prune - remove networks inativas;

# BRIDGE

* docker network create --driver bridge <network_name> - cria rede;
* docker run -dit --name <container_name> --network <network_name> bash - cria contaioner na rede;
* docker network connect <network_name> <container_name> - conecta container existente à rede;

# HOST

* docker run --rm -d --name nginx --network host nginx - deve funcionar localhost:80;
	- Não funciona em MacOS;

# Acessar máquina a partir do container

* curl http://host.docker.internal:<port_number> - acessa o que estiver na porta;


# Colocando em prática

* base image:
* Dockerfile:
	- apt-get update
	- WORKDIR /var/www/
	- adicionar comandos para instalação de pacotes no Dockerfile;
	- docker build -t <username>/<imagename> -f path/to/Dockerfile.prod

# Otimizando Imagens

* Multistage building;
	```
		FROM golang:latest AS builder
		.
		.
		.
		FROM scratch
		COPY --from=builder /path/ .
		RUN chwon -R www-data:www-data /var/www # permitir segundo estágio manipular arquivos, stc
	```

* Nginx como proxy reverso (nginx.conf);


# DOCKER-COMPOSE

* Iniciando com docker-compose;
* Criando banco de dados MySQL;
* Dependência entre containers (depends_on):
	- DOCKERIZE on app Dockerfile - install on build;
	- ```$ dockerize -wait tcp://db:3306 -timeout 50s```;
	- ```$ docker logs app```
	- ```$ docker logs db```

----------------------------------------------------------
Atividade 5 - Execução
----------------------------------------------------------
git clone https://github.com/jonashackt/spring-rabbitmq-messaging-microservices

- parar docker RabbitMQ
> sudo docker start rabbitmq

- build do projeto
mvn install -DskipTests (demora um pouco - download de pacotes)

(se necessário, instalar o maven sudo apt install maven)

- subir com docker-compose
> sudo docker-compose up -d (baixar imagens e )

(se necessário, sudo snap install docker)

- mostra o docker-compose.yml (os dois conatiners)

- mostrar como parar o docker-compose 
> sudo docker-compose down

- abrir console web
http://localhost:15672
guest & guest

- mostrar scale manual
docker-compose up -d --scale weatherbackend=3
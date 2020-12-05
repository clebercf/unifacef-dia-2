----------------------------------------------------------
Atividade 5 - Execução
----------------------------------------------------------
git clone https://github.com/jonashackt/spring-rabbitmq-messaging-microservices
----------------------------------------------------------

- parar docker RabbitMQ
> sudo docker stop rabbitmq

(opcional, remover conatiner)
> sudo docker rm rabbitmq

- build do projeto
mvn install -DskipTests (demora um pouco - download de pacotes)

(se necessário, instalar o maven sudo apt install maven)

- mostra o docker-compose.yml (os dois containers)

- modificar docker-compose
version: '3.7'

services:

  rabbitmq:
    image: rabbitmq:3-management-alpine
    ports:
      - "5672:5672"
      - "15672:15672"
    tty:
      true
    healthcheck:
      test: [ "CMD", "nc", "-z", "localhost", "5672" ]
      interval: 5s
      timeout: 15s
      retries: 3

  weatherbackend:
    build: ./weatherbackend
    depends_on:
      - rabbitmq
    ports:
      - "8090:8090"
    environment:
      - "SPRING_RABBITMQ_HOST=rabbitmq"
      - "LOGSTASH_HOST=host.docker.internal"
    tty:
      true
    restart:
      unless-stopped
    healthcheck:
      test: [ "CMD", "nc", "-z", "localhost", "8090" ]
      interval: 5s
      timeout: 15s
      retries: 3

  weatherservice:
    build: ./weatherservice
    depends_on:
      - rabbitmq
    ports:
      - "8095:8095"
    environment:
      - "SPRING_RABBITMQ_HOST=rabbitmq"
      - "LOGSTASH_HOST=host.docker.internal"
    tty:
      true
    restart:
      unless-stopped
    healthcheck:
      test: [ "CMD", "nc", "-z", "localhost", "8095" ]
      interval: 5s
      timeout: 15s
      retries: 3


- subir com docker-compose
> sudo docker-compose up -d (baixar imagens e inicia os containers)

- mostrar como parar o docker-compose 
> sudo docker-compose down

- mostrar scale manual
sudo docker-compose up -d --scale weatherbackend=3

- subir weatherservice
nohup java -jar weatherservice/target/weatherservice-0.0.1-SNAPSHOT.jar&

- enviar request curl
> curl -v localhost:8095/event
> curl -v localhost:8095/events/100

- abrir console web
http://localhost:15672
guest & guest

- verificar no logstash
> http://localhost:5601/

- modificar docker-compose e inserir weatherservice

----------------------------------------------------------
git clone https://github.com/jonashackt/docker-elk.git
----------------------------------------------------------

- iniciar com docker-compose
(se necessário, sudo snap install docker)
> sudo docker-compose up -d


- listar portas "em escuta" no computador
sudo lsof -i -P -n | grep LISTEN 

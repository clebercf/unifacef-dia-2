----------------------------------------------------------
Atividade 5 - Execução
----------------------------------------------------------
git clone https://github.com/jonashackt/docker-elk.git

- iniciar com docker-compose
(se necessário, sudo snap install docker)
> sudo docker-compose up -d
----------------------------------------------------------
git clone https://github.com/jonashackt/spring-rabbitmq-messaging-microservices
----------------------------------------------------------

- parar docker RabbitMQ
> sudo docker start rabbitmq

- build do projeto
mvn install -DskipTests (demora um pouco - download de pacotes)

(se necessário, instalar o maven sudo apt install maven)

- mostra o docker-compose.yml (os dois containers)

- adicionar o healthcheck para verificar quando a porta 5672 do rabbitmq estará disponível
healthcheck:
    test: [ "CMD", "nc", "-z", "localhost", "5672" ]
    interval: 5s
    timeout: 15s
    retries: 3    

- subir com docker-compose
> sudo docker-compose up -d (baixar imagens e inicia os containers)

- mostrar como parar o docker-compose 
> sudo docker-compose down

- mostrar scale manual
docker-compose up -d --scale weatherbackend=3

- subir weatherservice
java -jar weatherservice/target/weatherservice-0.0.1-SNAPSHOT.jar

- fazer um curl
curl -v localhost:8095/event

- abrir console web
http://localhost:15672
guest & guest
----------------------------------------------------------
Pré-requisito
----------------------------------------------------------
* instalar python3
> sudo apt update
> sudo apt install software-properties-common
> sudo add-apt-repository ppa:deadsnakes/ppa
> sudo apt update
> sudo apt install python3.8

- testar se foi instalado com sucesso
> python3

* instalar python3-pip
> sudo apt-get install python3-pip

* instalar docker
> sudo snap install docker     # version 19.03.11, or
> sudo apt  install docker.io  # version 19.03.8-0ubuntu1.20.04.1

* rodar o container do rabbitmq
> sudo mkdir -p /docker/rabbitmq/data (salvar dados fora do container)
> sudo docker pull rabbitmq:3-management

> sudo docker run -d --name rabbitmq \
 -p 5672:5672 \
 -p 15672:15672 \
 --restart=always \
 --hostname rabbitmq-master \
 -v /docker/rabbitmq/data:/var/lib/rabbitmq \
 rabbitmq:3-management
----------------------------------------------------------
Comandos utéis
----------------------------------------------------------
    docker
    ------------------------------------------------------
    - listar os conatiners que estão rodando
    > sudo docker ps

    - listar as imagens baixadas
    > sudo docker images

    - parar um container
    > sudo docker stop rabbitmq

    - iniciar um container
    > sudo docker start rabbitmq

    - visualizar logs
    > sudo docker logs -f rabbitmq

    - acessar o terminal bash do container
    sudo docker exec -it rabbitmq /bin/bash
    ------------------------------------------------------
    RabbitMQ
    ------------------------------------------------------
    - rabbitmqadmin list exchanges
    - rabbitmqadmin list queues
    - rabbitmqadmin -f long list queues
    - rabbitmqadmin -f long -d3 list queues
----------------------------------------------------------
Atividade 1 - Execução
----------------------------------------------------------
https://www.rabbitmq.com/tutorials/tutorial-two-python.html

python3 -m pip install pika --upgrade

rabbitmqctl list_queues name messages_ready messages_unacknowledged
rabbitmqctl set_permissions -p "custom-vhost" "guest" ".*" ".*" ".*"

* demonstrar
> interface web
> producing / consuming
> balanceamento por Round-robin
> deburrar os workers, mostrar a fila e acumula na fila
> ack
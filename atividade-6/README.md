----------------------------------------------------------
Atividade 6 - Execução
----------------------------------------------------------

- instalar npm
sudo apt install npm

- artillery
sudo npm install -g artillery

https://artillery.io/

- escalar manualmente os backends

- This will launch 1000 virtual users that will do 10 requests each, to the specified URL.
artillery quick -c 1000 -n 10 http://localhost:8095/events/100

- For example, the following command will run the test during 10s, with 2 new users arriving each second, resulting in around 20 requests in the total.
artillery quick https://httpbin.org/get -r 2 -d 10

- entregável
verificar no Kibana as requisições

- referencia
https://dev.to/brpaz/load-testing-your-applications-with-artillery-4m1p
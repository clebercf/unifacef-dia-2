----------------------------------------------------------
Atividade 3 - Execução
----------------------------------------------------------
https://www.rabbitmq.com/tutorials/tutorial-five-python.html

* demonstrar
- distribuição dos pacotes (utilizando os critérios)

<facility>.<severity>

* receber todos
python3 receive_logs_topic.py "#"

* receber facility = "kern"
python3 receive_logs_topic.py "kern.*"

* receber severity = "critical"
python3 receive_logs_topic.py "*.critical"

* recebendo múltiplos
python receive_logs_topic.py "kern.*" "*.critical"

* enviando mensagens
python emit_log_topic.py "kern.critical" "A critical kernel error"
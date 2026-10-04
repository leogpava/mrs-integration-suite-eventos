# Conceitos

Glossário rápido, sempre com o exemplo do trem 1234.

| Termo | O que é | No exemplo do trem |
|---|---|---|
| **Evento** | Um fato que já aconteceu, comunicado a quem tiver interesse | "O trem 1234 chegou a Juiz de Fora às 08:47" |
| **Comando** | Um pedido para alguém fazer algo; espera execução | "Notifique o cliente sobre o atraso do trem 1234" |
| **Broker** | O intermediário que recebe e distribui mensagens | O Solace (Advanced Event Mesh) |
| **Tópico** | O endereço onde uma mensagem é publicada; não guarda nada | `mrs/patio/jfora/trem/chegada` |
| **Fila** | Armazenamento que guarda mensagens até alguém consumir | `q_chegada`, que assina o tópico de chegada |
| **Wildcard** | Curinga na assinatura para pegar vários tópicos de uma vez | `mrs/patio/*/trem/chegada` pega Juiz de Fora e Volta Redonda |
| **Entrega direta** | Rápida, sem garantia: quem não está conectado perde a mensagem | Subscriber do Try Me! desligado não recebe a chegada |
| **Entrega garantida** | A mensagem é guardada (Persistent) até ser consumida | A chegada fica em `q_chegada` até o iFlow ler |
| **MQTT** | Protocolo leve de mensagens, comum em IoT e no MQTTX | Um sensor do pátio publicando a chegada |
| **AMQP** | Protocolo de mensagens usado entre o Integration Suite e o Solace | O iFlow lendo `q_chegada` na porta 5671 |
| **iFlow** | Fluxo de integração no Cloud Integration | `Chegada_Trem_HTTPS` e `Chegada_Trem_Evento` |
| **Adapter** | O "conector" que liga o iFlow a um sistema ou protocolo | HTTPS (Postman) e AMQP (Solace) |
| **Header** | Metadado que viaja junto com a mensagem até o destino | `X-MRS-Classificacao: ATRASADO` na resposta |
| **Property** | Variável interna do iFlow; não sai dele | `${property.trem}` = `1234` |
| **Body** | O conteúdo principal da mensagem | O JSON com trem, pátio, previsto, chegada e status |
| **Request/reply** | Quem chama espera a resposta na mesma conexão | O Postman chama o iFlow e recebe a classificação |

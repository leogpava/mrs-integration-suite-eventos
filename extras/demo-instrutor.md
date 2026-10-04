# Demo do instrutor

Roteiro da demonstração ao vivo **antes do intervalo**, depois da etapa 02 e antes da etapa 03. A ideia é mostrar, sem configuração pesada, por que eventos mudam a forma de integrar.

## Preparação (antes da aula)

1. Serviço Solace ativo, com a fila `q_chegada` assinando `mrs/patio/jfora/trem/chegada`.
2. `Chegada_Trem_Evento` deployado e **parado** (Undeploy), para usar só na parte 4.
3. Abertos lado a lado:
   - Try Me! **A** (publisher + subscriber)
   - Try Me! **B** (subscriber) em outra aba
   - MQTTX (opcional) conectado ao mesmo serviço
4. Payloads à mão: [trem-atrasado.json](../payloads/entrada/trem-atrasado.json) e [trem-no-horario.json](../payloads/entrada/trem-no-horario.json).

## 1. Um evento, vários assinantes

1. No Try Me! **A** e no **B**, assine `mrs/patio/jfora/trem/chegada`.
2. Publique o trem atrasado uma única vez.
3. Mostre que **as duas abas recebem**.

> **Mensagem-chave:** quem publica não sabe quem vai ouvir. Amanhã o planejamento, o cliente e a manutenção podem assinar, sem mexer em quem publica.

## 2. Wildcard com outro pátio

1. No Try Me! **B**, troque a assinatura por `mrs/patio/*/trem/chegada` (no MQTTX: `mrs/patio/+/trem/chegada`).
2. Publique a mesma chegada no tópico de Volta Redonda:

   ```text
   mrs/patio/vredonda/trem/chegada
   ```

3. Mostre que **só o B recebe**: o A assina apenas Juiz de Fora.

> **Mensagem-chave:** a hierarquia do tópico é o que permite assinar "todos os pátios" com uma linha.

## 3. A fila guarda a mensagem

1. Desconecte o subscriber do Try Me! **A**.
2. Publique o trem atrasado com Delivery Mode **Persistent**.
3. Reconecte o subscriber e mostre que ele **perdeu** a mensagem: nada chega.
4. Abra **Queues → q_chegada** e mostre que **Messages Queued** aumentou: a fila guardou.

> **Mensagem-chave:** tópico é endereço, fila é armazenamento. Quem precisa de garantia de entrega consome de uma fila.

## 4. Fluxo completo com o iFlow

1. Assine `mrs/alerta/>` e `mrs/status/>` no Try Me! **B**.
2. Faça o **Deploy** do `Chegada_Trem_Evento`.
3. Mostre que as mensagens guardadas na fila são consumidas na hora: **Messages Queued** volta a 0 e chegam eventos em `mrs/alerta/atraso`.
4. Publique o trem no horário e mostre o evento em `mrs/status/pontual`.
5. Abra o **Monitor** e mostre as mensagens **Completed**.

> **Mensagem-chave:** é a mesma lógica do iFlow HTTPS que eles acabaram de fazer. Só mudou a entrada (fila) e a saída (novo evento).

## Fechamento

Anuncie o intervalo e diga que, na volta, cada um vai montar exatamente isso a partir da etapa [03-solace](../03-solace/).

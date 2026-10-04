# Convenção de nomes

Use exatamente estes nomes. Troque `<INICIAIS>` pelas suas iniciais em maiúsculas (exemplo: `ABC`).

| Item | Nome | Onde é usado |
|---|---|---|
| Package | `MRS_<INICIAIS>` | Integration Suite → Design |
| iFlow request/reply | `Chegada_Trem_HTTPS` | Etapa 01 |
| iFlow por evento | `Chegada_Trem_Evento` | Etapa 04 |
| Endpoint (Address) | `/mrs/<INICIAIS>/chegada` | Sender HTTPS do `Chegada_Trem_HTTPS` |
| Tópico de entrada | `mrs/patio/jfora/trem/chegada` | Publisher e assinatura da fila |
| Tópico de saída (atraso) | `mrs/alerta/atraso` | Receiver AMQP da rota "Sim" |
| Tópico de saída (no horário) | `mrs/status/pontual` | Receiver AMQP da rota "Não" |
| Fila | `q_chegada` | Solace Broker Manager e sender AMQP |
| Credencial | `SOLACE_AMQP` | Security Material e adapters AMQP |

## Como ler o tópico

```text
mrs / patio / jfora / trem / chegada
 │      │       │      │       └── o que aconteceu
 │      │       │      └────────── sobre o quê
 │      │       └───────────────── qual pátio
 │      └───────────────────────── domínio
 └──────────────────────────────── empresa
```

Cada nível separado por `/` é o que permite usar wildcards, como `mrs/patio/*/trem/chegada` para qualquer pátio.

# Troubleshooting

Procure o sintoma na primeira coluna.

## Integration Suite e acesso

| Sintoma | Causa | Solução |
|---|---|---|
| Menu do Integration Suite sem **Design** ou **Monitor** | Sessão aberta antes de atribuir as roles | Saia e entre de novo, ou abra em janela anônima |
| *"You are not authorized to view trace data"* | Falta a role collection `PI_Business_Expert` | Atribua `PI_Business_Expert` ao usuário e abra uma sessão nova |

## Postman e iFlow HTTPS

| Sintoma | Causa | Solução |
|---|---|---|
| **401 Unauthorized** | Token expirado ou não gerado | Collection → Authorization → **Get New Access Token** → **Use Token** |
| **403 Forbidden** | **CSRF Protected** marcado no Sender HTTPS, ou falta a role `ESBMessaging.send` na instância | Desmarque CSRF e faça redeploy; confira a role na instância Process Integration Runtime |
| **404 Not Found** | Endpoint errado ou iFlow não está **Started** | Copie o endpoint de **Manage Integration Content** e confira a variável `iniciais` |
| Erro de XPath no Set Properties | Raiz do XML diferente de `Evento` | No JSON to XML Converter: **Add XML Root Element** marcado, nome `Evento` |
| Router sempre vai para o default | `status` com valor diferente de `ATRASADO` (minúscula, espaço, acento) | Confira o JSON enviado e a condição `${property.status} = 'ATRASADO'` |

## Solace e iFlow por evento

| Sintoma | Causa | Solução |
|---|---|---|
| iFlow de evento não conecta ao Solace | Host com `wss://`, `amqps://` ou porta; Authentication diferente de **SASL**; **Connect with TLS** desmarcado | Host só com o nome, Port `5671`, SASL, TLS marcado |
| Mensagem parada na fila (**Messages Queued** não zera) | **Non-Owner Permission** diferente de `Consume` | Na fila `q_chegada`, ajuste Non-Owner Permission para `Consume` |
| Nada chega no Subscriber | Tópico assinado diferente do **Destination Name** do receiver | Assine `mrs/alerta/>` e `mrs/status/>`, e confira os Destination Names |

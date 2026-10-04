# Desafios

Para quem terminou antes. Não há resposta pronta: use o que você montou nas etapas 01 a 05. Cada desafio tem uma pista escondida, abra só se precisar.

## Desafio 1 · Terceiro status: ADIANTADO

Faça o iFlow por evento tratar um trem que chegou **antes** do previsto.

Entrada para testar:

```json
{
  "trem": "9012",
  "patio": "Juiz de Fora",
  "previsto": "10:00",
  "chegada": "09:40",
  "status": "ADIANTADO"
}
```

**Pronto quando:**

- [ ] O Router tem uma nova rota para `ADIANTADO`
- [ ] Um novo evento `TremAdiantado` é publicado em um **tópico novo**, seguindo a [convenção de nomes](../referencia/convencao-de-nomes.md)
- [ ] O subscriber recebe o evento no tópico novo
- [ ] Atrasado e no horário continuam funcionando

<details>
<summary>Pista</summary>

A estrutura de cada rota é sempre a mesma: condição no Router → Content Modifier → Send → Receiver AMQP. Antes de escolher o tópico novo, confira se ele não casa com a assinatura da fila.

</details>

## Desafio 2 · Registro de todas as chegadas

Além do alerta ou do status, publique **sempre** (em todos os casos) um evento de registro no tópico:

```text
mrs/patio/jfora/trem/registro
```

**Pronto quando:**

- [ ] Cada chegada publicada gera **dois** eventos: o de alerta/status e o de registro
- [ ] O subscriber, assinando `mrs/patio/jfora/trem/registro`, recebe todas as chegadas
- [ ] A fila `q_chegada` **não** recebe o evento de registro (sem loop)

<details>
<summary>Pista</summary>

Pense em onde, no desenho do iFlow, a mensagem passa em todos os casos. Procure na paleta um step que divide a mensagem em mais de um caminho.

</details>

## Desafio 3 · Expor o iFlow HTTPS via API Management

Publique o `Chegada_Trem_HTTPS` como uma API no **API Management**, para que o consumidor chame o proxy em vez do endpoint do iFlow.

**Pronto quando:**

- [ ] Existe um API Proxy apontando para o iFlow `Chegada_Trem_HTTPS`
- [ ] Uma chamada pelo Postman ao proxy retorna `200` com o header `X-MRS-Classificacao`
- [ ] A chamada aparece no Monitor do Cloud Integration como **Completed**

<details>
<summary>Pista</summary>

Comece em **Configure → APIs** no Integration Suite. Lembre que o iFlow continua exigindo um token OAuth: decida se o proxy repassa o token do consumidor ou busca um token próprio.

</details>

# payloads

Todos os JSONs usados no treinamento, prontos para copiar. Abra o arquivo no GitHub e use o botão **Copy raw file** (ou **Raw**).

## Quando usar cada arquivo

| Arquivo | O que é | Onde usar | Etapa |
|---|---|---|---|
| [entrada/trem-atrasado.json](entrada/trem-atrasado.json) | Chegada do trem 1234, **ATRASADO** | Body do Postman ou mensagem no Try Me! | 02, 03, 05 |
| [entrada/trem-no-horario.json](entrada/trem-no-horario.json) | Chegada do trem 5678, **NO_HORARIO** | Body do Postman ou mensagem no Try Me! | 02, 05 |
| [resposta-https/resposta-atraso.json](resposta-https/resposta-atraso.json) | Resposta da rota "Sim" | Body do **CM Resposta Atraso** | 01 |
| [resposta-https/resposta-pontual.json](resposta-https/resposta-pontual.json) | Resposta da rota "Não" | Body do **CM Resposta Pontual** | 01 |
| [evento-saida/evento-trem-atrasado.json](evento-saida/evento-trem-atrasado.json) | Evento `TremAtrasado` | Body do **CM Evento Atraso** | 04 |
| [evento-saida/evento-trem-no-horario.json](evento-saida/evento-trem-no-horario.json) | Evento `TremNoHorario` | Body do **CM Evento Pontual** | 04 |

> [!NOTE]
> Os arquivos de `resposta-https/` e `evento-saida/` contêm expressões `${property.x}`.
> Eles são para **colar no Content Modifier**, na aba **Message Body**, com **Type: Expression**. **Não envie esses arquivos** pelo Postman ou pelo Try Me!: quem troca `${property.trem}` por `1234` é o iFlow.

## Exemplo

Entrada enviada:

```json
{ "trem": "1234", "patio": "Juiz de Fora", "previsto": "08:00", "chegada": "08:47", "status": "ATRASADO" }
```

Campo `mensagem` no Content Modifier:

```text
Alerta: trem ${property.trem} chegou em ${property.patio} às ${property.chegada}. Previsto: ${property.previsto}.
```

Resultado devolvido pelo iFlow:

```text
Alerta: trem 1234 chegou em Juiz de Fora às 08:47. Previsto: 08:00.
```

# 02 · Chamada pelo Postman

**Objetivo:** chamar o iFlow `Chegada_Trem_HTTPS` com OAuth 2.0 (Client Credentials) e ver a classificação na resposta.

| Nesta pasta | Para quê |
|---|---|
| [MRS-Chegada-Trem.postman_collection.json](MRS-Chegada-Trem.postman_collection.json) | Collection com os dois requests e o OAuth configurado |
| [MRS-Trial.postman_environment.json](MRS-Trial.postman_environment.json) | Environment com as variáveis para você preencher |

## 1. Criar a instância Process Integration Runtime

1. No BTP Cockpit, abra seu subaccount → **Services → Instances and Subscriptions**.
2. Clique em **Create** e preencha:

   | Campo | Valor |
   |---|---|
   | Service | `SAP Process Integration Runtime` |
   | Plan | `integration-flow` |
   | Instance Name | `mrs-<INICIAIS>-runtime` |

3. Clique em **Next** e configure os parâmetros:

   | Campo | Valor |
   |---|---|
   | Roles | `ESBMessaging.send` |
   | Grant Types | `Client Credentials` |

4. Clique em **Create**.

> [!TIP]
> Se o serviço não aparecer na lista, confira em **Entitlements** do subaccount se o *Process Integration Runtime* está adicionado.

## 2. Criar a service key

1. Na instância criada, clique em **⋯ → Create Service Key**.
2. Dê o nome `mrs-<INICIAIS>-key` e clique em **Create**.
3. Abra a key. Ela tem este formato:

   ```json
   {
     "oauth": {
       "clientid": "<CLIENT_ID>",
       "clientsecret": "<CLIENT_SECRET>",
       "url": "<URL_DO_RUNTIME>",
       "tokenurl": "<TOKEN_URL>"
     }
   }
   ```

| Campo da key | Variável no Postman | Onde é usado |
|---|---|---|
| `clientid` | `clientid` | Client ID do OAuth (aba Authorization da collection) |
| `clientsecret` | `clientsecret` | Client Secret do OAuth |
| `tokenurl` | `tokenurl` | Access Token URL: onde o Postman busca o token |
| `url` | `url` | Início da URL dos requests: `{{url}}/http/mrs/{{iniciais}}/chegada` |

## 3. Importar e configurar no Postman

1. Baixe os dois arquivos desta pasta (abra cada um no GitHub → **Download raw file**).
2. No Postman, clique em **Import** e arraste os dois arquivos.
3. Em **Environments**, abra **MRS Trial** e preencha a coluna **Current value**:

   | Variável | Valor |
   |---|---|
   | `url` | campo `url` da service key |
   | `tokenurl` | campo `tokenurl` da service key |
   | `clientid` | campo `clientid` da service key |
   | `clientsecret` | campo `clientsecret` da service key |
   | `iniciais` | suas iniciais, as mesmas do Address do iFlow |

4. Clique em **Save** e selecione **MRS Trial** no seletor de environment (canto superior direito).
5. Abra a collection **MRS · Chegada de Trem** → aba **Authorization** → clique em **Get New Access Token** → **Use Token**.
6. Abra o request **Trem atrasado** e clique em **Send**.
7. Repita com **Trem no horário**.

> [!WARNING]
> Não faça commit do environment preenchido. Se exportar, salve como `MRS-Trial.local.json`: o `.gitignore` ignora esse nome.

## O que observar

| Onde | O que conferir |
|---|---|
| Resposta, status | `200 OK` |
| Resposta, aba **Headers** | `X-MRS-Classificacao: ATRASADO` (ou `NO_HORARIO`) |
| Resposta, aba **Test Results** | 2 testes passando |
| Requisição, **Console** do Postman | header `Authorization: Bearer ...` enviado |
| Integration Suite, **Monitor → Monitor Message Processing** | mensagem com status **Completed** |

Deu erro? Veja [referencia/troubleshooting.md](../referencia/troubleshooting.md).

## Próximo passo

Siga para [03-solace](../03-solace/).

# 00 · Pré-requisitos

Confira tudo antes do início do hands-on. Se algum item falhar, avise o instrutor.

## Checklist

- [ ] **Conta BTP trial** com o **Integration Suite** assinado.
- [ ] No Integration Suite, em **Manage Capabilities**, as capabilities ativadas:
  - [ ] **Cloud Integration** (*Design, Develop and Operate Integration Scenarios*)
  - [ ] **API Management** (*Design, Develop and Manage APIs*)
- [ ] No BTP Cockpit, em **Security → Users**, as role collections atribuídas ao seu usuário:

  | Role collection | Para quê |
  |---|---|
  | `PI_Administrator` | Administrar o tenant (Monitor, Security Material) |
  | `PI_Integration_Developer` | Criar, editar e fazer deploy de iFlows |
  | `PI_Business_Expert` | **Ver o payload no trace do Monitor** |

- [ ] **Postman** instalado (app desktop).
- [ ] **Conta no Solace Cloud (trial)** criada e com login funcionando.

> [!TIP]
> **Atribuiu roles agora? Saia e entre de novo no Integration Suite, ou abra em uma janela anônima.**
> A sessão que já estava aberta não enxerga roles novas. Sintoma típico: o menu lateral aparece sem **Design** ou **Monitor**.

## Próximo passo

Tudo marcado? Siga para [01-iflow-https](../01-iflow-https/).

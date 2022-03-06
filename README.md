# Описание

ldap авторизация с правами доступа для "`Deckhouse Kubernetes platform`"
https://deckhouse.io/ru/documentation/v1/modules/150-user-authn/usage.html#ldap

## Инструкция по применению: 

1. Изменить `9-ldap.yaml`, `values.yaml` под себя;
2. Deploy делать через `Jenkins`;
3. `Credentials` - прописать в Jenkins;
4. `WERF_KUBE_CONTEXT` - поменять;
5. `@Library('jenkins-devops@dev')_` - библиотека функции `Jenkins`.

## P.s.
Разработано под "`Deckhouse Kubernetes platform`"
https://deckhouse.io/en/
# Inventário das fontes CKAN de sinistros de trânsito

**Captura dos metadados:** 2026-10-22. Este documento registra a resposta observada da API CKAN nessa data; os valores podem mudar.

## Descoberta e endpoints verificados

- Portal: https://dados.pbh.gov.br/
- API Action v3 consultada: `https://dados.pbh.gov.br/api/3/action/`.
- `package_search` com `organization:bhtrans tags:Trânsito` retornou sucesso e 4 conjuntos.
- `resource_show?id=<resource_id>` retornou metadados de recurso.
- `datastore_search?resource_id=<resource_id>&limit=0` foi testado em 63 recursos listados, incluindo dicionários: 62 responderam com `success=true`; a consulta para `si-veic-2023` retornou HTTP 404.
- Os 55 recursos anuais com `datastore_active=true` responderam às consultas DataStore. Para `si-veic-2023`, o metadado marca DataStore inativo e a consulta falhou com 404.
- Foram tentados dois downloads por `HEAD` no host `ckan.pbh.gov.br` (si-veic-2023 e si-veic-2024); ambos retornaram HTTP 403 neste ambiente. Isso não permite concluir que o host bloqueia todos os clientes. Nenhum CSV foi baixado.

A documentação CKAN explica que `package_search` pesquisa conjuntos, `resource_show` retorna metadados de um recurso e `datastore_search` consulta uma tabela vinculada ao recurso. O campo `datastore_active` foi conferido junto com chamadas reais a `datastore_search`.

## Conjuntos e recursos

Os nomes e formatos abaixo são os valores retornados pelos metadados. `last_modified` é a data de atualização do recurso informada pelo CKAN, registrada sem conversão porque a resposta não traz offset explícito. A data de modificação do conjunto é distinta e fica no cabeçalho de cada tabela. Para dicionários, o período no nome identifica o período descrito; não é ano de ocorrência.

### [Relação das pessoas envolvidas nos acidentes de trânsito com vítima](https://dados.pbh.gov.br/dataset/relacao-das-pessoas-envolvidas-nos-acidentes-de-transito-com-vitima)

- **ID CKAN:** `relacao-das-pessoas-envolvidas-nos-acidentes-de-transito-com-vitima`
- **Última modificação do conjunto:** `2026-06-15T18:01:24.710307`
- **Licença informada:** Open Data Commons Open Database License (ODbL)

| Recurso | Ano/período indicado | Formato | `last_modified` (CKAN) | `datastore_active` | API `resource_show` |
|---|---:|---|---|---:|---|
| `dicionario-tabela-si-env-2011 a 2015.` | 2011–2015 (dicionário) | CSV | `2019-10-02T20:23:00.513478` | sim | [metadados](https://dados.pbh.gov.br/api/3/action/resource_show?id=2fbbb8a0-7b0b-4f05-b50a-db4398d21f79) |
| `dicionario-tabela-si-env-2016` | 2016 | CSV | `2019-10-02T20:34:51.509169` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=4dc43d21-31a9-4f28-beb7-8a9cacb783be) |
| `si_env-2011` | 2011 | CSV | `2019-10-02T20:18:15.566454` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=ef2e3fe2-c66e-4ee0-b6f4-cac9f3dc1942) |
| `si_env-2012` | 2012 | CSV | `2019-10-02T20:18:41.403580` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=f7baedea-e5b6-4352-99a3-c25d4eb0a675) |
| `si_env-2013` | 2013 | CSV | `2019-10-02T20:19:17.929694` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=6541ade0-3ff2-4703-8792-f8b8efa21862) |
| `si_env-2014` | 2014 | CSV | `2019-10-02T20:19:40.130142` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=d4638f70-e2a1-4eb3-a3e1-4728ef515ead) |
| `si_env-2015` | 2015 | CSV | `2019-10-02T20:20:06.281352` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=4efab468-da0b-4dcc-a6dd-56975a389f71) |
| `si_env-2016` | 2016 | CSV | `2019-10-02T20:29:33.409500` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=ddbc9691-ddf8-4906-967a-39f1b7a85b8e) |
| `si_env-2017` | 2017 | CSV | `2019-10-02T20:30:07.073072` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=38ae8351-ccfa-4f3e-b0ea-67d955484132) |
| `si_env-2018` | 2018 | CSV | `2019-10-02T20:30:53.357147` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=57148225-8205-4ece-8ebb-2afbeb0ab0c5) |
| `si_env-2019` | 2019 | CSV | `2020-09-18T18:39:03.347259` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=903286ca-b77f-44ad-aa6a-958aa018c33f) |
| `si_env-2020` | 2020 | CSV | `2021-08-16T18:45:50.010821` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=36913025-c826-4b84-bd25-b478ad71cb7c) |
| `si_env-2021` | 2021 | CSV | `2022-08-04T18:05:53.795711` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=5b2f4d30-8393-4c20-a0fe-ccb62dfdc8ab) |
| `si_env-2022` | 2022 | CSV | `2023-08-31T23:16:40.859976` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=8ee6609b-82de-4b93-8051-2f9d1e332784) |
| `si_env-2023` | 2023 | CSV | `2024-10-17T16:57:37.032468` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=89a3728b-62a5-476b-9b55-18c3d1460842) |
| `si_env-2024` | 2024 | CSV | `2025-10-21T19:51:08.835024` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=40028d66-9cfe-47f4-8280-a12102a3bb4b) |

### [Relação de ocorrências de acidentes de trânsito com vítima](https://dados.pbh.gov.br/dataset/relacao-de-ocorrencias-de-acidentes-de-transito-com-vitima)

- **ID CKAN:** `relacao-de-ocorrencias-de-acidentes-de-transito-com-vitima`
- **Última modificação do conjunto:** `2026-06-15T18:05:16.060205`
- **Licença informada:** Open Data Commons Open Database License (ODbL)

| Recurso | Ano/período indicado | Formato | `last_modified` (CKAN) | `datastore_active` | URL do recurso |
|---|---:|---|---|---:|---|
| `dicionario-tabela-si-bol-2011-2015` | 2011–2015 (dicionário) | CSV | `2019-10-02T19:29:44.878517` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=fa8f7f5c-da32-4d6e-a23d-0593ca2cd730) |
| `dicionario-tabela-si-bol-2016` | 2016 | CSV | `2019-10-02T19:37:47.991244` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=6237f517-23cc-4c8a-bb4e-bc8a2f35710e) |
| `si-bol_2012` | 2012 | CSV | `2021-09-29T16:49:29.487614` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=2ca68918-0ff0-4249-946f-7f8afbca29a9) |
| `si-bol_2013` | 2013 | CSV | `2021-09-29T16:50:16.733338` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=21b51642-610c-4b62-9ddb-0709c7caa500) |
| `si-bol_2014` | 2014 | CSV | `2021-09-29T16:50:46.593841` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=c59bf320-20aa-43b1-82c7-3fc0b2e7ecac) |
| `si-bol_2015` | 2015 | CSV | `2021-09-29T16:51:21.458313` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=a8775eab-7946-4136-83b9-f3f2c19cb46d) |
| `si-bol-2011` | 2011 | CSV | `2021-07-20T14:07:23.541508` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=d745d6e3-b186-45b2-93d9-ad28ee90274c) |
| `si-bol-2016` | 2016 | CSV | `2019-10-02T19:23:18.547931` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=7bb46b4d-24e8-4bc7-9da0-6027567237ca) |
| `si-bol-2017` | 2017 | CSV | `2019-10-02T19:25:08.611266` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=bba29971-3623-4438-a3e3-13ef35a8b670) |
| `si-bol-2018` | 2018 | CSV | `2019-10-02T19:25:52.715007` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=703ecfb7-d798-4573-a94c-4bc02e48ea0e) |
| `si-bol-2019` | 2019 | CSV | `2020-09-18T18:29:43.108135` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=ab6db535-b706-4e7b-9fdc-3bc1e823401e) |
| `si-bol-2020` | 2020 | CSV | `2021-08-16T16:55:16.776417` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=132eb19a-6079-43ed-b171-43270306eb88) |
| `si-bol-2021` | 2021 | CSV | `2022-08-04T18:17:59.530034` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=689e1333-22b1-4f5a-b860-bbb3b6a1a3f1) |
| `si-bol-2022` | 2022 | CSV | `2023-08-31T23:13:37.043322` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=1e3d3bc4-7256-4f36-8419-12c28f250869) |
| `si-bol-2023` | 2023 | CSV | `2024-10-17T16:52:50.993526` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=0e3a775f-1f2c-49d0-ae0b-b0fd51dfd307) |
| `si-bol-2024` | 2024 | CSV | `2025-10-21T19:49:19.579761` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=c6f6ede5-2c25-4540-b08a-f0bec7bb36f5) |

### [Relação dos logradouros dos locais de acidentes de trânsito com vítima](https://dados.pbh.gov.br/dataset/relacao-dos-logradouros-dos-locais-de-acidentes-de-transito-com-vitima)

- **ID CKAN:** `relacao-dos-logradouros-dos-locais-de-acidentes-de-transito-com-vitima`
- **Última modificação do conjunto:** `2026-06-15T18:12:47.602190`
- **Licença informada:** Open Data Commons Open Database License (ODbL)

| Recurso | Ano/período indicado | Formato | `last_modified` (CKAN) | `datastore_active` | URL do recurso |
|---|---:|---|---|---:|---|
| `dicionario-tabela-si-log-2011-2015` | 2011–2015 (dicionário) | CSV | `2019-10-01T16:16:25.642693` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=963da5fc-ad98-4391-9e42-dcb3b55d708c) |
| `dicionario-tabela-si-log-2016` | 2016 | CSV | `2019-10-02T19:11:35.863427` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=27a96571-b45f-49fe-8028-9efe0dc691d1) |
| `si-log-2011` | 2011 | CSV | `2021-07-20T17:15:38.388314` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=fbff5076-58ef-4e1e-a61a-ea3cb64ea666) |
| `si-log-2012` | 2012 | CSV | `2021-07-20T17:16:14.326967` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=fc4defc8-20f3-4b7f-a7ac-946772d771ed) |
| `si-log-2013` | 2013 | CSV | `2021-07-20T17:16:45.555257` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=2d2d17c3-498a-40fe-8fe1-4adea8fdda6b) |
| `si-log-2014` | 2014 | CSV | `2021-07-20T17:17:25.650291` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=59df259c-1467-4ce5-9fe3-89e0e31e65a7) |
| `si-log-2015` | 2015 | CSV | `2021-07-20T17:17:55.142001` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=98c456e1-0fa4-40f6-9d76-e6aab7afa205) |
| `si-log-2016` | 2016 | CSV | `2019-10-02T19:06:00.619191` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=c97aff41-e1f1-4bb5-a607-e454006918d7) |
| `si-log-2017` | 2017 | CSV | `2019-10-02T19:07:19.687747` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=008598e6-3ddc-4477-b756-ffc1c896d941) |
| `si-log-2018` | 2018 | CSV | `2020-09-18T18:55:22.797457` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=c721544f-4ebc-41c8-af21-b46a0e1b4a75) |
| `si-log-2019` | 2019 | CSV | `2020-09-18T18:15:46.503653` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=ad490dd1-7af5-4868-b35f-9471f15be744) |
| `si-log-2020` | 2020 | CSV | `2021-08-16T16:53:27.547437` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=b8fe48fc-ace3-43a5-9b94-8147762a13e5) |
| `si-log-2021` | 2021 | CSV | `2022-08-04T17:19:07.866264` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=b2ceb746-2184-42ec-a17f-6048ce87fb9b) |
| `si-log-2022` | 2022 | CSV | `2023-08-31T23:14:31.057165` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=23ba3b4f-a7ff-47bb-9031-2d65a3aa5c94) |
| `si-log-2023` | 2023 | CSV | `2024-10-17T16:55:10.664054` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=475e374b-1273-48c0-a664-7dd507198dcd) |
| `si-log-2024` | 2024 | CSV | `2025-10-21T19:59:26.451594` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=056fd213-486b-4a30-ac9c-1f2a9f266d1b) |

### [Relação dos veículos envolvidos nos acidentes de trânsito com vítima](https://dados.pbh.gov.br/dataset/relacao-dos-veiculos-envolvidos-nos-acidentes-de-transito-com-vitima)

- **ID CKAN:** `relacao-dos-veiculos-envolvidos-nos-acidentes-de-transito-com-vitima`
- **Última modificação do conjunto:** `2026-06-15T18:16:13.149089`
- **Licença informada:** Open Data Commons Open Database License (ODbL)

| Recurso | Ano/período indicado | Formato | `last_modified` (CKAN) | `datastore_active` | URL do recurso |
|---|---:|---|---|---:|---|
| `dicionario-tabela-si-veic-2011 a 2015` | 2011–2015 (dicionário) | CSV | `2019-10-02T19:56:47.712611` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=debcd4d7-aa90-4710-a997-d42be3192fef) |
| `dicionario-tabela-si-veic-2016` | 2016 | CSV | `2019-10-02T20:06:02.241009` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=75c6e4d3-7d78-4a76-9892-4597aa6a8d6e) |
| `si-veic-2011` | 2011 | CSV | `2021-07-20T17:22:52.716752` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=5e3f1b65-abea-4694-89f2-d3331bbd3892) |
| `si-veic-2012` | 2012 | CSV | `2021-07-20T17:23:29.197062` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=afa8f757-01da-4ffe-b2b6-996f412b0029) |
| `si-veic-2013` | 2013 | CSV | `2021-07-20T17:24:01.341570` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=ff6c00da-6e88-49a6-bd16-0903a6439042) |
| `si-veic-2014` | 2014 | CSV | `2021-07-20T17:24:58.584531` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=2c9ff303-5cd5-4bb7-ae12-98687b8f2144) |
| `si-veic-2015` | 2015 | CSV | `2021-07-20T17:25:47.616199` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=e9ada3e0-77d5-4a95-9d0f-5b376a434b46) |
| `si-veic-2016` | 2016 | CSV | `2019-10-02T19:58:35.227942` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=487a70f3-72aa-4a7c-b447-80a67dd912c3) |
| `si-veic-2017` | 2017 | CSV | `2019-10-02T19:59:29.323558` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=580fa764-64e3-436d-9c9a-1e5ba1d0e64b) |
| `si-veic-2018` | 2018 | CSV | `2019-10-02T20:00:15.300466` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=1360223c-b0a4-4a6a-9cf7-a7a2cc7782d8) |
| `si-veic-2019` | 2019 | CSV | `2020-09-18T18:44:36.637834` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=2825e76c-6478-483c-bd89-0e496049e055) |
| `si-veic-2020` | 2020 | CSV | `2021-08-16T16:51:54.148854` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=4e7a8bb8-772d-4dbd-ae94-adfe77f6965b) |
| `si-veic-2021` | 2021 | CSV | `2022-08-04T17:56:48.446400` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=080fc7b2-9dde-44c8-a772-93a6fc4afe4f) |
| `si-veic-2022` | 2022 | CSV | `2023-09-04T20:02:13.322436` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=9411232f-f04b-404c-96f0-384973cbea35) |
| `si-veic-2023` | 2023 | não informado | `2025-03-13T12:55:31.312995` | não | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=8ea48368-d083-4731-b698-145a85fa3319) |
| `si-veic-2024` | 2024 | CSV | `2025-10-21T20:01:12.468845` | sim | [metadados/download](https://dados.pbh.gov.br/api/3/action/resource_show?id=fa83a84f-562c-45ff-9b89-7bc0c555fe6a) |

## Interpretação e lacunas

- O catálogo indica recursos anuais de 2011 a 2024 nas quatro coleções. Os nomes e anos são listados recurso a recurso acima; nenhum período foi inferido para além dos metadados.
- Em 55 recursos anuais, a consulta DataStore foi observada como disponível. Isso permite consumir os registros pelo endpoint; os arquivos continuam referenciados nos metadados.
- `si-veic-2023` não informa formato no campo CKAN (`format` vazio), apesar de seu nome e URL terminarem em `.csv`; o DataStore retornou 404. O metadado contém uma URL de arquivo, então esse seria o caminho de acesso se estiver disponível; a tentativa de acesso respondeu 403 neste ambiente e não validou o conteúdo.
- As tentativas de download foram apenas `HEAD`; conteúdo, integridade do arquivo, hash SHA-256, encoding, separador, esquema e total de linhas não foram verificados.
- Não foi determinada a data máxima dos fatos em cada recurso. Datas de publicação/alteração não devem ser confundidas com período dos registros.
- O inventário não cobre o conjunto separado de localização espacial que aparece em outras buscas por etiqueta “Sinistros”; o escopo aqui são as quatro coleções solicitadas.

## Referências

- [Portal de Dados Abertos de Belo Horizonte](https://dados.pbh.gov.br/).
- [Documentação da Action API do CKAN 2.12](https://docs.ckan.org/en/2.12/api/index.html).
- [Documentação CKAN DataStore 2.12](https://docs.ckan.org/en/2.12/maintaining/datastore.html).
- Consulta observada: ``https://dados.pbh.gov.br/api/3/action/package_search?q=organization:bhtrans%20tags:Tr%C3%A2nsito&rows=100``.

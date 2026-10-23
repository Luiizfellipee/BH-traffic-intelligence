# PROGRESSO — BH Traffic Intelligence

> Início: 22/10/2026 · Estado: **não iniciado** · Fase autorizada para início: **M0 (Fundação e inventário)**

## Como usar
- `[ ]` pendente, `[x]` concluído com evidência documentada.
- O Codex pode executar apenas a fase autorizada pelo proprietário; ao finalizar, deve registrar data, comandos realmente executados e resultados.
- Alterar status **somente** após confirmação dos critérios de aceite; não antecipar progresso.
- Se uma tarefa depender de acesso à internet/serviço indisponível, usar `[ ]` e explicar no diário.

## Visão dos marcos

| Marco | Etapa | Estado | Gate |
|---|---|---|---|
| M0 | Fundação e inventário de fontes | Pendente / autorizada para início | Ambiente, CI e inventário verificáveis |
| M1 | Ingestão auditável | Bloqueado até aprovação | Download e rerun sem duplicações |
| M2 | Bronze/Silver + qualidade | Bloqueado | Profiling e reconciliação |
| M3 | PostgreSQL e modelo analítico | Bloqueado | Chaves/cardinalidade e SQL válidos |
| M4 | EDA e relatório analítico | Bloqueado | Perguntas respondidas com evidências |
| M5 | BI e publicação do MVP | Bloqueado | Dashboard reconciliado e README público |
| M6 | ML opcional | Bloqueado por gate de viabilidade | Sem leakage; baseline, split temporal |
| M7 | Atualizações e fontes adicionais | Bloqueado | Fontes separadas e ingestão não destrutiva |

## M0 — Fundação e inventário (ATIVA PARA INÍCIO)
- [ ] Inicializar repositório e definir `.gitignore` seguro.
- [ ] Criar estrutura mínima, `pyproject.toml`, ambiente Python 3.12 e README inicial.
- [ ] Configurar Ruff, pytest, primeiro teste e workflow de CI.
- [ ] Criar Compose de PostgreSQL local e `.env.example` (sem segredos reais).
- [x] Identificar e registrar todas as quatro fontes anuais BHTRANS e seus recursos/anos efetivos. Evidência parcial desta etapa CKAN: `docs/data_sources.md`.
- [ ] Registrar nomenclatura, formatos, licenças, datas e riscos de schema.
- [ ] Criar `docs/architecture.md` e `docs/data_sources.md` iniciais.
- [ ] Rodar validações possíveis e documentar resultados.
- [ ] Registrar conclusão com evidências e pedir aprovação para M1.

## M1 — Ingestão auditável
- [ ] CLI de descoberta de recursos reais e seleção fonte/ano.
- [ ] Download robusto, retries/timeouts, atomicidade e SHA-256.
- [ ] Manifesto por recurso: origem, data, ano, hash, tamanho, linhas (quando viável).
- [ ] Prova de idempotência e testes de falha/reexecução.
- [ ] Documentação de como repetir o download.

## M2 — Bronze e Silver
- [ ] Profiling por dataset e ano (encoding, tipos, nulos, datas, duplicidades).
- [ ] Levantar e validar chaves/cardi­nalidades e transformações.
- [ ] Parquet Bronze e Silver tipados com rastreabilidade.
- [ ] Quarentena e relatório de qualidade (input/output/rejeitos).
- [ ] Testes de invariantes e mudanças de esquema.

## M3 — SQL e dados analíticos
- [ ] Desenho do modelo com granularidade explícita.
- [ ] DDL PostgreSQL, índices e scripts versionados.
- [ ] Carga idempotente e testes de integridade.
- [ ] Reconciliação contra fontes e prevenção de dupla contagem.
- [ ] Consultas SQL documentadas para o dashboard.

## M4 — EDA e estatística
- [ ] Definir pelo menos cinco perguntas concretas.
- [ ] Analisar evolução temporal, tipos, regionais e envolvidos.
- [ ] Definir universos e denominadores de cada métrica.
- [ ] Testar hipóteses plausíveis sem alegações causais indevidas.
- [ ] Publicar notebook e `docs/findings.md` reproduzíveis.

## M5 — Dashboard e MVP
- [ ] Escolher Power BI ou Metabase como apresentação principal.
- [ ] Dashboard com filtros e indicadores conferidos contra SQL.
- [ ] Páginas de metodologia, fontes, cobertura e limitações.
- [ ] Capturas legítimas, README completo e instruções de reprodução.
- [ ] Revisão de acessibilidade, links, privacidade e licenças.
- [ ] MVP publicado e revisão crítica de portfólio concluída.

## M6 — ML (opcional)
- [ ] Aprovar caso de uso, alvo e variáveis conhecidas no momento de previsão.
- [ ] Validar volume, rótulos, desbalanceamento e vieses.
- [ ] Construir baseline sem vazamento e split temporal.
- [ ] Avaliar métricas adequadas e erros, documentar limitações.
- [ ] Introduzir MLflow apenas se contribuir para reproduzibilidade.

## M7 — Expansão (opcional)
- [ ] Descoberta agendada de novos recursos sem sobrescrita silenciosa.
- [ ] Verificação e alerta de mudanças de schema.
- [ ] Avaliação crítica de compatibilidade SENATRAN versus BHTRANS.
- [ ] Comparação separada com dados 2025/2026 se apropriada.

## Diário de execução

### 22/10/2026 — M0 / remover referência ao plano interno do README
- **Objetivo:** evitar um link público quebrado e não publicar referência ao arquivo de planejamento que ficará local.
- **Arquivos alterados:** `README.md`; este registro em `PROGRESSO.md`.
- **Comandos executados:** busca somente de leitura por referências ao plano; leitura final das alterações.
- **Resultados observados:** removido o link para `files/PLANO_MESTRE.md`; a seção de tecnologias descreve opções futuras sem atribuí-las a um plano interno. A regra `/files/*` foi mantida no `.gitignore`.
- **Problemas/limitações:** o Git local ainda não foi inicializado, então não há diff Git para revisar.
- **Evidência:** README sem links ou menções ao arquivo `PLANO_MESTRE.md`.
- **Próximo passo autorizado:** concluir os itens restantes de M0.

### 22/10/2026 — M0 / fluxo de dados no README
- **Objetivo:** representar visualmente o percurso dos dados desde o catálogo CKAN até análises e apresentação.
- **Arquivos alterados:** `README.md`; este registro em `PROGRESSO.md`.
- **Comandos executados:** leitura do README e do progresso; leitura final do README atualizado.
- **Resultados observados:** o diagrama mostra a decisão entre DataStore e download, preservação em `data/raw`, profiling, Bronze/Silver, SQL, EDA e dashboard; diferencia o inventário verificado, o CSV local ainda não validado, as etapas planejadas e ML opcional.
- **Problemas/limitações:** o render do Mermaid depende do visualizador Markdown. Não há repositório Git inicializado para conferir diff.
- **Evidência:** seção “Fluxo do projeto” em `README.md`.
- **Próximo passo autorizado:** concluir os itens restantes de M0.

### 22/10/2026 — M0 / mapa visual do roadmap no README
- **Objetivo:** tornar visíveis as fases e gates do plano sem confundir etapas futuras com funcionalidades implementadas.
- **Arquivos alterados:** `README.md`; este registro em `PROGRESSO.md`.
- **Comandos executados:** leitura do README, `.gitignore` e `PROGRESSO.md`; leitura final do README atualizado.
- **Resultados observados:** o diagrama distingue M0 ativa/incompleta, M1–M5 bloqueadas e M6/M7 opcionais, conforme o plano.
- **Problemas/limitações:** o render do Mermaid depende do visualizador Markdown; não há repositório Git inicializado para conferir diff.
- **Evidência:** seção “Mapa visual do plano” em `README.md`.
- **Próximo passo autorizado:** concluir os itens restantes de M0.

### 22/10/2026 — M0 / README inicial
- **Objetivo:** apresentar a proposta, o estado real do projeto, o roadmap e o uso da IA como apoio ao aprendizado.
- **Arquivos alterados:** `README.md`; este registro em `PROGRESSO.md`.
- **Comandos executados:** inspeção somente de leitura de `PROGRESSO.md`, `.gitignore`, arquivos existentes e estado Git; leitura final do README criado.
- **Resultados observados:** o README distingue o inventário já verificado do pipeline, análises e dashboard ainda não implementados; inclui instrução para acompanhar o projeto no VS Code e a responsabilidade humana sobre decisões e conclusões.
- **Problemas/limitações:** não há aplicação executável ou comando de ingestão para documentar ainda. M0 continua incompleto e M1 permanece bloqueado.
- **Evidência:** `README.md`.
- **Próximo passo autorizado:** concluir os itens restantes de M0.

### 22/10/2026 — M0 / inventário CKAN das coleções de sinistros
- **Objetivo:** verificar pela API CKAN os recursos de ocorrências, pessoas, veículos e logradouros, incluindo ano/período, formato, datas de atualização e disponibilidade no DataStore.
- **Arquivos alterados:** `docs/data_sources.md`; este registro em `PROGRESSO.md`.
- **Comandos executados:** consultas somente de leitura com `Invoke-RestMethod` a `package_search`, `resource_show` e `datastore_search`; verificações `HEAD` com `curl.exe` para dois URLs de download; inspeção de arquivos com `rg --files` e estado Git com `git status`.
- **Resultados observados:** `package_search` retornou 4 conjuntos e 64 recursos no total. Foram testados 63 recursos no DataStore: 62 chamadas responderam `success=true`; `si-veic-2023` retornou HTTP 404 e está marcado `datastore_active=false`. Os 55 recursos anuais ativos responderam ao DataStore. Os dois URLs de arquivo testados (si-veic-2023 e si-veic-2024) retornaram HTTP 403 neste ambiente. Os metadados informam ODbL para os quatro conjuntos e recursos anuais de 2011 a 2024.
- **Problemas/limitações:** nenhum CSV foi baixado; portanto, esquema, encoding, separador, linhas, hash e período factual máximo não foram verificados. O HTTP 403 observado neste ambiente não prova indisponibilidade geral dos arquivos. `si-veic-2023` tem campo `format` vazio, embora a URL termine em `.csv`. O diretório não é um repositório Git. M0 permanece incompleto; não foram implementados o módulo de ingestão nem seus testes, pois pertencem ao M1, ainda bloqueado no plano de progresso.
- **Evidência:** `docs/data_sources.md` contém as 64 entradas de recursos, metadados por recurso, endpoints testados e limitações observadas.
- **Próximo passo autorizado:** concluir os itens restantes de M0 e validar a acessibilidade dos downloads em ambiente apropriado; somente então iniciar M1 conforme o gate do plano.

### 22/10/2026 — Preparação documental
- **Feito:** criação inicial dos arquivos de planejamento fora do ambiente de desenvolvimento do usuário.
- **Não feito:** repositório Git, código, ingestão, CI, banco, dashboard, testes e modelos.
- **Verificações:** fontes e situação histórica registradas no plano; é necessário conferir atualizações novamente na implementação.
- **Próxima atividade autorizada:** iniciar M0 com o prompt em `PLANO_MESTRE.md`, seção 11.

## Decisões pendentes
- [ ] Nome final e licença do código (verificar distinção da licença dos dados).
- [ ] Escolher Polars ou Pandas após amostra piloto.
- [ ] Escolher BI principal entre Power BI e Metabase até M5.
- [ ] Escolher período histórico comparável após avaliação de esquema.
- [ ] Avaliar necessidade e viabilidade de ML somente após M4/M5.

## Modelo para futuras entradas do diário

```markdown
### AAAA-MM-DD — Mx / nome da entrega
- **Objetivo:** ...
- **Arquivos alterados:** ...
- **Comandos executados:** ...
- **Resultados observados:** ...
- **Problemas/limitações:** ...
- **Evidência:** links internos, testes e relatórios ...
- **Próximo passo autorizado:** ...
```

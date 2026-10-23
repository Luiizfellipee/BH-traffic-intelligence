# PROGRESSO — BH Traffic Intelligence

> Início: 22/10/2026 · Estado: **em andamento** · Fase ativa: **M0 (Fundação e inventário)**

## Como usar
- `[ ]` pendente, `[x]` concluído com evidência documentada.
- O Codex pode executar apenas a fase autorizada pelo proprietário; ao finalizar, deve registrar data, comandos realmente executados e resultados.
- Alterar status **somente** após confirmação dos critérios de aceite; não antecipar progresso.
- Se uma tarefa depender de acesso à internet/serviço indisponível, usar `[ ]` e explicar no diário.

## Visão dos marcos

| Marco | Etapa | Estado | Gate |
|---|---|---|---|
| M0 | Fundação e inventário de fontes | Em andamento | Ambiente, CI e inventário verificáveis |
| M1 | Ingestão auditável | Bloqueado até aprovação | Download e rerun sem duplicações |
| M2 | Bronze/Silver + qualidade | Bloqueado | Profiling e reconciliação |
| M3 | PostgreSQL e modelo analítico | Bloqueado | Chaves/cardinalidade e SQL válidos |
| M4 | EDA e relatório analítico | Bloqueado | Perguntas respondidas com evidências |
| M5 | BI e publicação do MVP | Bloqueado | Dashboard reconciliado e README público |
| M6 | ML opcional | Bloqueado por gate de viabilidade | Sem leakage; baseline, split temporal |
| M7 | Atualizações e fontes adicionais | Bloqueado | Fontes separadas e ingestão não destrutiva |

## M0 — Fundação e inventário (EM ANDAMENTO)
- [ ] Inicializar repositório e definir `.gitignore` seguro.
- [ ] Criar estrutura mínima, `pyproject.toml`, ambiente Python 3.12 e README inicial.
- [ ] Configurar Ruff, pytest, primeiro teste e workflow de CI.
- [ ] Criar Compose de PostgreSQL local e `.env.example` (sem segredos reais).
- [x] Identificar e registrar todas as quatro fontes anuais BHTRANS e seus recursos/anos efetivos. Evidência parcial desta etapa CKAN: `docs/data_sources.md`.
- [ ] Registrar nomenclatura, formatos, licenças, datas e riscos de schema.
- [x] Criar `docs/architecture.md` e `docs/data_sources.md` iniciais. Evidência: [`docs/architecture.md`](docs/architecture.md) e [`docs/data_sources.md`](docs/data_sources.md).
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

### 22/10/2026 — M0 / ferramenta local de otimização de contexto
- **Objetivo:** disponibilizar o Token Optimizer para o Codex neste projeto sem incluir seus arquivos de configuração no Git.
- **Arquivos alterados:** `.git/info/exclude` (regra local `.codex/`), `.codex/config.toml` e `.codex/hooks.json` (ambos ignorados pelo Git), configuração pessoal do Codex fora do repositório e este registro. O pacote foi instalado no cache pessoal do Codex.
- **Comandos executados:** consulta à documentação do projeto da ferramenta e do Codex; `codex plugin marketplace add alexgreensh/token-optimizer`; `codex plugin add token-optimizer@alexgreensh-token-optimizer --json`; execução de `codex-install --project . --profile balanced --skip-compact-prompt` após `--dry-run`; `codex-doctor --project .`; `codex plugin list` dentro e fora do projeto; `git check-ignore -v`, `git ls-files .codex`, `git status --short` e `git diff --check`.
- **Resultados observados:** pacote 5.13.57 no cache pessoal; plugin habilitado neste projeto e desabilitado fora dele. Cinco eventos de hooks foram escritos em `.codex/hooks.json`: SessionStart, Stop, SubagentStart, SubagentStop e UserPromptSubmit. O Git ignora os dois arquivos locais em `.codex/`; `git ls-files .codex` não retornou arquivos. Não foram criados hooks globais.
- **Problemas/limitações:** `codex-doctor` retornou 20 OK, 2 WARN e 2 FAIL. Os FAIL correspondem ao prompt de compactação e aos hooks globais deliberadamente não configurados; a configuração por projeto foi reconhecida como OK. O hook Stop ainda não teve execução observada nesta sessão, portanto não há evidência de redução de tokens ou de atualização do dashboard. Reiniciar o Codex é necessário para carregar os hooks novos.
- **Evidência:** configuração local ignorada pelo Git, saída de `codex plugin list` com estado habilitado somente dentro do projeto e diagnóstico do instalador.
- **Próximo passo autorizado:** verificar a execução do hook em uma sessão nova do Codex; concluir os itens pendentes de M0.

### 22/10/2026 — M0 / diferenciação dos diagramas do README
- **Objetivo:** tornar visualmente distintas a visão rápida do pipeline e a arquitetura detalhada, conforme retorno do proprietário.
- **Arquivos alterados:** os quatro SVGs em `assets/` e este registro em `PROGRESSO.md`. Os caminhos no README permaneceram válidos.
- **Comandos executados:** leitura do README, arquitetura e progresso; renderização dos quatro SVGs no Edge com Playwright; validação XML com `xml.etree.ElementTree`; checagem geométrica de texto dentro dos cards; inspeção visual das capturas; `git diff --check`.
- **Resultados observados:** pipeline horizontal de seis etapas com resumos inferiores e paleta azul/teal; arquitetura de seis módulos com responsabilidades e artefatos em painéis mais detalhados e paleta violeta/teal. As versões móveis usam leitura vertical. Os quatro arquivos passaram na validação XML e na checagem geométrica: seis cards e nenhum texto fora dos cards em cada arquivo. A versão móvel do pipeline foi ajustada após a inspeção visual para evitar conteúdo próximo à borda inferior.
- **Problemas/limitações:** a interface final do GitHub ainda não foi inspecionada. Os módulos planejados continuam sem implementação; M0 segue incompleta.
- **Evidência:** `assets/pipeline-overview.svg`, `assets/pipeline-overview-mobile.svg`, `assets/data-architecture.svg` e `assets/data-architecture-mobile.svg`.
- **Próximo passo autorizado:** concluir os itens pendentes de M0 conforme seus critérios.

### 22/10/2026 — M0 / apresentação visual do README
- **Objetivo:** apresentar o inventário já verificado e a arquitetura futura com leitura clara em desktop e celular, sem antecipar os gates de M1–M5.
- **Arquivos alterados:** `README.md`, quatro SVGs em `assets/` e este registro em `PROGRESSO.md`.
- **Comandos executados:** leitura de `AGENTS.md`, `files/PLANO_MESTRE.md`, `PROGRESSO.md`, README e documentos adjacentes; `git status --short` e `git diff`; validação local em Python de XML, referências e âncoras; renderização dos quatro SVGs em Edge com Playwright; inspeção visual das capturas; `git diff --check`.
- **Resultados observados:** README reorganizado com navegação, estados por texto, duas imagens SVG acessíveis e versões móveis. Os quatro SVGs são XML válido e contêm seis cards cada. As 32 referências locais examinadas no README não apresentaram destinos inexistentes. A checagem geométrica no navegador não encontrou texto fora dos cards. As quatro capturas foram inspecionadas sem texto cortado ou sobreposto. `git diff --check` não apontou erro de whitespace.
- **Problemas/limitações:** a renderização final dentro da interface do GitHub não foi conferida; a inspeção visual usou Edge local. Não foram executados testes de código, pois a mudança é documental. M0 continua incompleta e M1 permanece bloqueada.
- **Evidência:** `README.md`, `assets/pipeline-overview.svg`, `assets/pipeline-overview-mobile.svg`, `assets/data-architecture.svg` e `assets/data-architecture-mobile.svg`.
- **Próximo passo autorizado:** concluir os itens pendentes de M0 conforme seus critérios.

### 22/10/2026 — M0 / revisão editorial e técnica do README
- **Objetivo:** apresentar o problema, a direção do projeto e seu estágio atual sem atribuir resultados ou funcionalidades ainda inexistentes.
- **Arquivos alterados:** `README.md`, `docs/architecture.md`, `docs/data_sources.md` e este registro em `PROGRESSO.md`.
- **Comandos executados:** leitura dos documentos e arquivos de configuração existentes; checagem PowerShell de links Markdown relativos em `README.md` e `docs/architecture.md`.
- **Resultados observados:** README reorganizado com perguntas ainda sem resposta, fluxo que distingue inventário documentado de etapas planejadas, estado de implementação, fontes, limites e seção transparente sobre IA. Criado documento de arquitetura com estados explícitos. Os 18 links Markdown relativos verificados em `README.md`, `docs/architecture.md`, `docs/data_sources.md` e `PROGRESSO.md` apontam para caminhos existentes. Instruções de execução fictícias não foram incluídas. O estado geral e M0 foram atualizados de “não iniciado/autorizada para início” para “em andamento”, com o gate de saída ainda pendente, conforme o inventário e o diário já registrados.
- **Correção de consistência:** o inventário registra que as tentativas `HEAD` não obtiveram arquivos; no estado atual, `data/raw/bhtrans/veiculos/si-veic-2023.csv` existe localmente. Sua presença foi verificada sem ler seu conteúdo. `docs/data_sources.md` agora distingue esses fatos. O arquivo não foi validado, e a entrada anterior do diário permanece como registro da verificação feita à época.
- **Problemas/limitações:** conteúdo, integridade, esquema e hash do CSV continuam desconhecidos. Não foram executados testes de código; esta entrega foi documental. M0 continua incompleta e M1 bloqueada pelo gate existente.
- **Evidência:** `README.md`, `docs/architecture.md`, `docs/data_sources.md`; checagem local dos links concluída sem caminhos inexistentes.
- **Próximo passo autorizado:** concluir os itens pendentes de M0 conforme os critérios já registrados.

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

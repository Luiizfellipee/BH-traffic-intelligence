<div align="center">

<h1>BH Traffic Intelligence</h1>

<p><strong>Sinistros de trânsito com vítimas em Belo Horizonte, a partir de dados públicos da BHTRANS</strong></p>

<p>Uma base documentada para investigar registros, cobertura e limites dos dados de trânsito da cidade.</p>

<p>
  <img alt="Python 3.12" src="https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white">
  <img alt="PostgreSQL planejado" src="https://img.shields.io/badge/PostgreSQL-planejado-4169E1?style=flat-square&logo=postgresql&logoColor=white">
  <img alt="SQL planejado" src="https://img.shields.io/badge/SQL-planejado-555555?style=flat-square">
  <img alt="Fonte: BHTRANS" src="https://img.shields.io/badge/dados-BHTRANS-17365D?style=flat-square">
</p>

</div>

## Sobre o projeto

Como os sinistros com vítimas registrados em Belo Horizonte se distribuem no tempo e no espaço? O que os registros de pessoas, veículos e logradouros podem acrescentar a essa análise? O **BH Traffic Intelligence** parte dessas perguntas e documenta as fontes antes de construir comparações.

O objetivo é produzir análises reproduzíveis, com período, universo e limitações explícitos. Contar linhas de pessoas ou veículos como se fossem ocorrências pode distorcer os resultados; por isso, relações e chaves precisam ser verificadas nos arquivos reais.

## Dados e metodologia

A fonte principal são quatro coleções anuais da BHTRANS no [Portal de Dados Abertos da PBH](https://dados.pbh.gov.br/): **ocorrências, pessoas, veículos e logradouros**. O [inventário de fontes](docs/data_sources.md) registra recursos, formatos, datas do catálogo, licença e disponibilidade observada no CKAN.

Na captura de **22/10/2026**, os metadados indicavam recursos rotulados de **2011 a 2024**. Esses rótulos não confirmam as datas dos fatos dentro dos arquivos. O catálogo informou licença **ODbL** para as quatro coleções; a licença do código ainda não foi definida.

## Arquitetura e fluxo

**Fluxo proposto:** catálogo CKAN → preservação dos dados brutos → inspeção de esquema e qualidade → preparação analítica → consultas e visualizações.

O inventário de metadados está documentado. As demais etapas ainda dependem de implementação e validação. Cada recurso deverá ser acessado conforme a disponibilidade real do DataStore ou do arquivo publicado. O tratamento deverá preservar a origem, registrar contagens e rejeições e validar chaves antes de combinar as coleções. A [documentação de arquitetura](docs/architecture.md) detalha o desenho e as restrições.

## Como reproduzir

Consulte o [inventário](docs/data_sources.md) para localizar os recursos oficiais e conferir os metadados no portal da PBH. O [registro de progresso](PROGRESSO.md) reúne as verificações realizadas. **Ainda não há comando de ingestão, análise ou dashboard executável neste repositório.**

O ambiente Python está declarado em [`pyproject.toml`](pyproject.toml), com versão `>=3.12`, Ruff e pytest. As tags de PostgreSQL e SQL indicam tecnologias previstas no desenho, ainda sem implementação. Os dados locais ficam fora do Git.

## Limitações

Os registros tratam de **sinistros com vítimas**, não de todos os eventos de trânsito da cidade. Datas de atualização do catálogo não são datas dos sinistros, e a comparabilidade entre anos ainda depende de inspeção dos arquivos.

Contagens não medem risco viário sem um denominador de exposição. Relações entre ocorrências, pessoas, veículos e logradouros exigem validação para evitar dupla contagem. Dados BHTRANS e SENATRAN não devem formar uma série única sem auditoria de compatibilidade. Ainda não há resultados analíticos validados.

## Autor

**Luiz Felipe Piumbini** · [GitHub](https://github.com/Luiizfellipee)

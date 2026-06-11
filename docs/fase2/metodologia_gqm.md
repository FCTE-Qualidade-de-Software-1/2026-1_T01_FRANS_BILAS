# 2. Metodologia — Modelo GQM

O modelo **Goal-Question-Metric (GQM)**, proposto por Basili et al. (1994), define que cada meta de avaliacao (Goal) deve ser desdobrada em questoes (Questions) que reflitam aspectos observaveis do sistema, e em metricas (Metrics) que respondam a essas questoes de forma objetiva.

A aplicacao do GQM assegura que cada metrica esteja diretamente relacionada a um objetivo de negocio ou tecnico, evitando medicoes sem valor pratico.

---

## Estrutura Analitica

| Elemento | Definicao no GQM | Aplicacao ao Agio |
|---|---|---|
| Objeto | O que sera analisado | Sistema Agio v1.0.0 (web) |
| Proposito | Por que sera analisado | Avaliacao de qualidade para decisao de adocao e manutencao |
| Qualidade do foco | Caracteristica de interesse | Adequacao Funcional, Confiabilidade e Eficiencia de Desempenho (ISO/IEC 25010:2011) |
| Ponto de vista | Quem vai utilizar os dados | Equipe avaliadora, equipe original do Agio, potenciais adotantes (PMEs) |
| Contexto | Onde a avaliacao sera conduzida | Ambiente local via Docker Compose; dados sinteticos; ate 50 usuarios simulados simultaneos |

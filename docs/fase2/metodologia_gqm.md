# 2. Métodologia — Modelo GQM

O modelo **Goal-Question-Metric (GQM)**, proposto por Basili et al. (1994), define que cada meta de avaliação (Goal) deve ser desdobrada em questões (Questions) que reflitam aspects observaveis do sistema, e em métricas (Metrics) que respondam a essas questões de forma objetiva.

A aplicação do GQM assegura que cada métrica esteja diretamente relacionada a um objetivo de negocio ou tecnico, evitando medições sem valor pratico.

---

## Estrutura Analitica

| Elemento | Definicao no GQM | Aplicação ao Agio |
|---|---|---|
| Objeto | O que sera analisado | Sistema Agio v1.0.0 (web) |
| Proposito | Por que sera analisado | Avaliação de qualidade para decisão de adocao e manutencao |
| Qualidade do foco | Caracteristica de interesse | Adequacao Funcional, Confiabilidade e Eficiencia de Desempenho (ISO/IEC 25010:2011) |
| Ponto de vista | Quem vai utilizar os dados | Equipe avaliadora, equipe original do Agio, potenciais adotantes (PMEs) |
| Contexto | Onde a avaliação sera conduzida | Ambiente local via Docker Compose; dados sinteticos; ate 50 usuarios simulados simultâneos |

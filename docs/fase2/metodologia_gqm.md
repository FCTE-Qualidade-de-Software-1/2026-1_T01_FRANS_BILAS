# 2. Metodologia — Modelo GQM

O modelo **Goal-Question-Metric (GQM)**, proposto por Basili et al. (1994), define que cada meta de avaliação (**Goal**) deve ser desdobrada em questões (**Questions**) que reflitam aspectos observáveis do sistema, e em métricas (**Metrics**) que respondam a essas questões de forma objetiva.

> [!TIP]
> A aplicação do GQM assegura que cada métrica esteja diretamente relacionada a um objetivo de negócio ou técnico, evitando a coleta de dados e medições sem valor prático para o projeto.

---

## 2.1 Estrutura Analítica de Definição do Contexto

A tabela abaixo estabelece as fronteiras e as diretrizes do modelo GQM aplicadas especificamente ao cenário do sistema Agio.

| 🧩 Elemento | 📋 Definição no GQM | 🚀 Aplicação ao Agio |
| :--- | :--- | :--- |
| **Objeto** | O que será analisado. | Sistema Agio v1.0.0 (Web/API). |
| **Propósito** | Por que será analisado. | Avaliação de qualidade de software para embasar decisões de adoção e planejamento de manutenção. |
| **Foco de Qualidade** | Característica de interesse. | Adequação Funcional, Confiabilidade e Eficiência de Desempenho (baseado na norma ISO/IEC 25010). |
| **Ponto de Vista** | Quem vai utilizar os dados. | Equipe avaliadora de qualidade, equipe original de desenvolvimento do Agio e potenciais adotantes (PMEs). |
| **Contexto** | Onde a avaliação será conduzida. | Ambiente local controlado via Docker Compose, utilizando dados sintéticos e simulação de até 50 usuários simultâneos. |
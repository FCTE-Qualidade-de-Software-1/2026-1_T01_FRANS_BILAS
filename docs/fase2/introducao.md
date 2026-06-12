# 1. Introdução e Objetivos

Esta fase tem como objetivo especificar a avaliação das características de Adequação Funcional, Confiabilidade e Eficiência de Desempenho do sistema Agio, conforme os requisitos definidos na [Fase 1](../fase1/proposito.md).

A especificação segue o modelo **Goal-Question-Metric (GQM)**, estruturado em três níveis:

1. **🧠 Nível Conceitual (Goals)** — Estabelecer os objetivos da avaliação, alinhados às características de qualidade priorizadas na Fase 1.
2. **❓ Nível Operacional (Questions)** — Formular perguntas que direcionem a análise, derivadas diretamente das metas.
3. **📊 Nível Quantitativo (Metrics)** — Identificar indicadores objetivos e mensuráveis capazes de responder às questões propostas.

---

## 1.1 Rastreabilidade com a Fase 1

Conforme definido na Fase 1 (ver [Priorização das Características](../fase1/priorizacao_caracteristicas.md)), as três características foram selecionadas por meio de uma matriz de Impacto x Viabilidade. Os objetivos GQM desta fase derivam diretamente dessas características e dos stakeholders mapeados na Fase 1 (ver [Requisitante e Partes Interessadas](../fase1/requisitante.md)).

| Característica (Fase 1) | Goal GQM (Fase 2) | Stakeholders Envolvidos |
| :--- | :--- | :--- |
| 🎯 **Adequação Funcional**<br>*(Prioridade 1)* | **GOAL 1** — Medir completude e correção funcional. | Equipe de desenvolvimento e potenciais adotantes. |
| 🛡️ **Confiabilidade**<br>*(Prioridade 2)* | **GOAL 2** — Verificar estabilidade sob uso contínuo. | Operadores e administradores do sistema. |
| ⚡ **Eficiência de Desempenho**<br>*(Prioridade 3)* | **GOAL 3** — Medir desempenho sob carga crescente. | PMEs que exigem tempo de resposta adequado. |

---

## 1.2 Escopo do Objeto de Avaliação

> <center>**Objetos de Avaliação** (conforme [Escopo da Avaliação](../fase1/escopo.md)):<br>Endpoints da API REST (Django + DRF), banco de dados PostgreSQL, testes automatizados existentes e o deploy publicado na Vercel.</center>

> <center>**Versão Avaliada:** `Agio v1.0.0` — Release oficial do repositório GitHub.</center>
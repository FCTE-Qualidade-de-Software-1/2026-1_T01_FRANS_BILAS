# 1. Introducao e Objetivos

Esta fase tem como objetivo especificar a avaliação das características **Adequacao Functional**, **Confiabilidade** e **Eficiencia de Desempenho** do sistema Agio, conforme os requisitos definidos na [Fase 1](../fase1/proposito.md).

A especificacao segue o modelo **Goal-Question-Metric (GQM)**, estruturado em tres niveis:

1. **Nivel Conceitual (Goals)** — Estabelecer os objetivos da avaliação, alinhados as características de qualidade priorizadas na Fase 1.
2. **Nivel Operacional (Questions)** — Formular perguntas que direcionem a analyse, derivadas das metas.
3. **Nivel Quantitativo (Metrics)** — Identificar indicadores objetivos capazes de responder as questões propostas.

---

## Rastreabilidade com a Fase 1

Conforme definido na Fase 1 (ver [Priorizacao das Caracteristicas](../fase1/priorizacao_características.md)), as tres características foram selecionadas por meio de uma matriz de Impacto x Viabilidade. Os objetivos GQM desta fase derivam diretamente dessas características e dos stakeholders mapeados na Fase 1 (ver [Requisitante e Partes Interessadas](../fase1/requisitante.md)).

| Caracteristica (Fase 1) | Goal GQM (Fase 2) | Stakeholders envolvidos |
|---|---|---|
| Adequacao Functional (prioridade 1) | GOAL 1 — Medir completude e correção functional | Equipe de desenvolvimento, potenciais adotantes |
| Confiabilidade (prioridade 2) | GOAL 2 — Verificar estabilidade sob uso continuo | Operadores e administradores |
| Eficiencia de Desempenho (prioridade 3) | GOAL 3 — Medir desempenho sob carga crescente | PMEs que exigem tempo de resposta adequado |

**Objetos de avaliação** (conforme [Escopo da Avaliação](../fase1/escopo.md)): endpoints da API REST (Django + DRF), banco de dados PostgreSQL, testes automatizados existentes e deploy publicado na Vercel.

**Versão avaliada:** Agio v1.0.0 — Release official do repositorio GitHub.

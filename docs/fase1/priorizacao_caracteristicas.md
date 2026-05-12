# 📊 5. Seleção e Priorização de Características

## 5.1 Características Selecionadas

Conforme definido na Seção 4.2, as características selecionadas para avaliação do sistema Agio foram:

<div class="grid cards" markdown>

- ✅ **Adequação Funcional**
- 🔒 **Confiabilidade**
- ⚡ **Eficiência de Desempenho**

</div>

Essas características foram consideradas as mais relevantes para o contexto de uso do sistema e para os objetivos da avaliação.

---

## 5.2 Método de Priorização

A priorização foi conduzida utilizando uma matriz de Impacto × Viabilidade, considerando dois critérios principais:

| Critério | Descrição |
|:--|:--|
| **Impacto para os stakeholders** | Grau de importância da característica para as decisões dos interessados (escala de 1 a 5) |
| **Viabilidade de medição** | Facilidade de medir a característica considerando tempo, ferramentas e dados disponíveis (escala de 1 a 5) |

---

### Cálculo da Pontuação

!!! info "Fórmula Utilizada"

    A pontuação final corresponde ao produto entre:

    **Impacto × Viabilidade**

    Pontuação máxima possível: **25 pontos**

---

## Matriz de Priorização

| Característica | Impacto | Viabilidade | Pontuação | Resultado |
|:--|:--:|:--:|:--:|:--|
| Adequação Funcional | 5 | 5 | **25** | ✅ Prioridade 1 |
| Confiabilidade | 5 | 4 | **20** | ✅ Prioridade 2 |
| Eficiência de Desempenho | 4 | 5 | **20** | ✅ Prioridade 3 |
| Segurança | 4 | 2 | 8 | ❌ Excluída |
| Usabilidade | 3 | 2 | 6 | ❌ Excluída |
| Manutenibilidade | 3 | 2 | 6 | ❌ Excluída |
| Compatibilidade | 2 | 4 | 8 | ❌ Excluída |
| Portabilidade | 1 | 5 | 5 | ❌ Excluída |

---

## 5.3 Resultado da Priorização

Durante o processo de seleção, alguns *trade-offs* foram discutidos pela equipe.

---

### Trade-offs Considerados

!!! tip "Adequação Funcional × Usabilidade"

    Ambas impactam diretamente o usuário final.  
    Entretanto, Adequação Funcional foi priorizada por permitir
    medição objetiva com base no backlog e nas funcionalidades implementadas.

    A avaliação de Usabilidade exigiria testes com usuários reais,
    inviáveis dentro do prazo da disciplina.

---

!!! tip "Confiabilidade × Segurança"

    As duas características são críticas para sistemas corporativos.

    A Confiabilidade foi priorizada porque pode ser avaliada
    com testes automatizados, injeção de falhas e simulação de cenários.

    A avaliação de Segurança demandaria pentesting especializado,
    extrapolando o escopo do projeto.

---

!!! tip "Eficiência de Desempenho × Manutenibilidade"

    Eficiência de Desempenho produz métricas quantitativas claras,
    como tempo de resposta e throughput.

    Já Manutenibilidade depende de análise qualitativa profunda
    do código-fonte, aumentando o risco de superficialidade.

---

## Relação entre as Características

As três características selecionadas apresentam forte relação entre si:

<div class="grid cards" markdown>

- ⚠️ Funcionalidades incompletas podem gerar falhas operacionais

- 🔒 Problemas de desempenho podem afetar a confiabilidade do sistema

- ⚡ Degradação sob carga impacta diretamente a percepção de qualidade

</div>

---

!!! note "Análise Integrada"

    Na Fase 4, os resultados das métricas serão analisados em conjunto
    para identificar correlações entre adequação funcional,
    confiabilidade e desempenho.
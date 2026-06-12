# 3. Definição de Metas, Questões e Métricas

## 3.1 Metas (Goals) Formalizadas

As metas da avaliação foram estruturadas seguindo o padrão metodológico do GQM: Propósito — Objeto — Foco de Qualidade — Ponto de Vista — Ambiente.

| Elemento | GOAL 1 | GOAL 2 | GOAL 3 |
| :--- | :--- | :--- | :--- |
| **Objeto** | Sistema Agio v1.0.0<br>*(API REST + Frontend)* | Sistema Agio v1.0.0<br>*(API REST + Banco de Dados)* | Sistema Agio v1.0.0<br>*(Backend Django + PostgreSQL)* |
| **Propósito** | Avaliar a completude e a correção das funcionalidades implementadas em relação ao backlog planejado. | Verificar a estabilidade do sistema sob uso contínuo e diante de entradas inesperadas. | Medir o desempenho do sistema em operações de inventário sob condições de carga crescente. |
| **Foco de Qualidade** | Completude funcional, correção funcional e adequação à tarefa. | Maturidade, disponibilidade e tolerância a falhas. | Comportamento temporal, utilização de recursos e capacidade. |
| **Ponto de Vista** | Equipe de desenvolvimento e potenciais adotantes (PMEs). | Operadores e administradores do sistema. | Potenciais adotantes de PMEs que exigem tempo de resposta adequado. |
| **Ambiente** | Ambiente local controlado via Docker Compose; dados sintéticos; requisições via scripts automatizados. | Ambiente local com Docker Compose; carga simulada de até 50 usuários simultâneos. | Ambiente local com Docker Compose; até 10.000 itens cadastrados; carga progressiva via ferramenta de teste. |

---

### GOAL 1 — Adequação Funcional

Medir o nível de completude e a correção das funcionalidades implementadas no sistema Agio em relação ao backlog planejado (*Controle de Acesso, Login JWT, CRUD de Itens, Dashboard, Exportação CSV, PostgreSQL*), do ponto de vista da equipe de desenvolvimento e de potenciais adotantes, no contexto de ambiente controlado via Docker Compose, com o objetivo de identificar lacunas funcionais e priorizar correções.

!!! note "Hipótese 1 (H1)"

    Espera-se que o sistema apresente um alto índice de completude funcional (acima de 75%), considerando que o projeto passou por nove sprints de desenvolvimento.

    Ainda assim, podem existir lacunas relacionadas a funcionalidades secundárias ou componentes menos priorizados durante a evolução do sistema.

---

### GOAL 2 — Confiabilidade

Verificar a estabilidade do sistema Agio sob uso contínuo e entradas inesperadas, com foco em maturidade (cobertura de testes), disponibilidade e tolerância a falhas, do ponto de vista de operadores e administradores, no contexto da execução via Docker Compose com carga simulada de até 50 usuários simultâneos.

!!! tip "Hipótese 2 (H2)"

    Espera-se que o sistema apresente boa disponibilidade operacional (acima de 95%).

    Entretanto, a tolerância a falhas severas pode ser limitada em razão do estágio inicial de maturidade do projeto (`v1.0.0`).

---

### GOAL 3 — Eficiência de Desempenho

Medir e avaliar o comportamento temporal, a utilização de recursos e a capacidade de armazenamento/processamento do sistema Agio sob carga crescente de dados (até 10.000 itens cadastrados) e de acessos (até 50 usuários simultâneos), do ponto de vista de PMEs que exigem baixo tempo de resposta, para determinar a viabilidade de adoção do ecossistema em ambiente de produção.

!!! info "Hipótese 3 (H3)"

    Espera-se que o tempo de resposta permaneça abaixo de 1 segundo para operações comuns do sistema.

    Contudo, existe uma forte tendência de degradação significativa de desempenho em cenários com volumes superiores a 5.000 itens, considerando a ausência de evidências explícitas de otimização de consultas (*query tuning*) no repositório atual.

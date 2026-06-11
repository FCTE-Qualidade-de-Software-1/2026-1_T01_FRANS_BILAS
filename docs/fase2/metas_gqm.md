# 3. Definicao de Metas, Questoes e Metricas

## 3.1 Metas (Goals) Formalizadas

As metas sao formalizadas com a estrutura: Proposito — Objeto — Qualidade do Foco — Ponto de Vista — Ambiente.

| Elemento | GOAL 1 | GOAL 2 | GOAL 3 |
|---|---|---|---|
| **Objeto** | Sistema Agio v1.0.0 (API REST + Frontend) | Sistema Agio v1.0.0 (API REST + Banco de Dados) | Sistema Agio v1.0.0 (Backend Django + PostgreSQL) |
| **Proposito** | Avaliar a completude e correcao das funcionalidades implementadas em relacao ao backlog planejado | Verificar a estabilidade do sistema sob uso continuo e entradas inesperadas | Medir o desempenho do sistema em operacoes de inventario sob carga crescente |
| **Qualidade do Foco** | Completude funcional, correcao funcional e adequacao a tarefa | Maturidade, disponibilidade e tolerancia a falhas | Comportamento temporal, utilizacao de recursos e capacidade |
| **Ponto de Vista** | Equipe de desenvolvimento e potenciais adotantes (PMEs) | Operadores e administradores do sistema | Potenciais adotantes de PMEs que exigem tempo de resposta adequado |
| **Ambiente** | Ambiente local controlado via Docker Compose; dados sinteticos; requisicoes via scripts automatizados | Ambiente local com Docker Compose; carga simulada de ate 50 usuarios simultaneos | Ambiente local com Docker Compose; ate 10.000 itens cadastrados; carga progressiva via ferramenta de teste |

---

### GOAL 1 — Adequacao Funcional

Medir o nivel de completude e correcao das funcionalidades implementadas no sistema Agio em relacao ao backlog planejado (Controle de Acesso, Login JWT, CRUD de Itens, Dashboard, Exportacao CSV, PostgreSQL), do ponto de vista da equipe de desenvolvimento e de potenciais adotantes, no contexto de ambiente controlado via Docker Compose, com o objetivo de identificar lacunas funcionais e priorizar correcoes.

**Hipotese:** Espera-se que o sistema apresente alto indice de completude funcional (acima de 75%), dado que passou por 9 sprints de desenvolvimento, mas podem existir lacunas em funcionalidades secundarias.

### GOAL 2 — Confiabilidade

Verificar a estabilidade do sistema Agio sob uso continuo e entradas inesperadas, com foco em maturidade (cobertura de testes), disponibilidade e tolerancia a falhas, do ponto de vista de operadores e administradores, no contexto da execucao via Docker Compose com carga simulada de ate 50 usuarios simultaneos.

**Hipotese:** Espera-se que o sistema apresente boa disponibilidade (acima de 95%), mas a tolerancia a falhas pode ser limitada dado o estagio inicial do projeto (v1.0.0).

### GOAL 3 — Eficiencia de Desempenho

Medir e avaliar o comportamento temporal, a utilizacao de recursos e a capacidade do sistema Agio sob carga crescente de dados (ate 10.000 itens) e de usuarios (ate 50 simultaneos), do ponto de vista de PMEs que exigem baixo tempo de resposta, para determinar a viabilidade de adocao em ambiente de producao.

**Hipotese:** Espera-se que o tempo de resposta se mantenha abaixo de 1 segundo para operacoes comuns, mas pode haver degradacao significativa com volumes acima de 5.000 itens, dado que nao ha evidencias de otimizacao de consultas no repositorio.

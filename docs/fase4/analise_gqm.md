# 2. Analyse e Respostas GQM

## 2.1 Consolidacao dos Resultados

| ID | Métrica | Resultado | Nivel |
|---|---|---|---|
| M1 | Indice de Completude Functional (ICF) | 100,0% | Excelente |
| M2 | Taxa de Correcao Functional (TCF) | 90,0% | Bom |
| M3 | Indice de Adequacao a Tarefa (IAT) | 83,3% | Bom |
| M4 | Taxa de Maturidade por Cobertura de Testes (TMCT) | 0% pass (0 testes) / 57% cobertura | Insuficiente |
| M5 | Taxa de Disponibilidade Operacional (TDO) | 100,0% (200/200 requisições) | Excelente |
| M6 | Indice de Tolerancia a Falhas (ITF) | 80,0% | Bom |
| M7 | Tempo Medio de Resposta por Endpoint (TMRE) | 2,3ms | Excelente |
| M8 | Utilizacao de Recursos sob Carga (URC) | PostgreSQL: CPU 0%, RAM 32,58 MB; Django: ~21ms tempo medio sob 50 usuarios | Excelente |
| M9 | Degradacao de Desempenho por Volume (DDVD) | 5.253% | Insuficiente |

---

## 2.2 Respostas as Questões GQM

### GOAL 1 — Adequacao Functional

**Q1: Quantas das funcionalidades previstas no backlog estão implementadas?**

Das 8 funcionalidades previstas no backlog (homepage, login, dashboard, exportacao CSV, CRUD de produtos via API, admin, logout), todas 8 estão efetivamente implementadas e acessiveis, resultando em um ICF de 100%. O sistema cobre a totalidade do escopo functional planejado, incluindo operacoes CRUD completas, autenticacao, painel administrative e exportacao de dados.

**Q2: Os resultados retornados pelos endpoints correspondem ao comportamento especificado?**

Em 9 de 10 casos de teste, os endpoints retornaram o comportamento esperado (TCF = 90%). A unica falha identificada foi no acesso ao dashboard via API, que retorna HTTP 302 (redirect) em vez de HTTP 200, devido ao controle de sessão que valida `user_id` antes de renderizar a página. Isso não e um bug functional grave, mas uma restricao do fluxo de autenticacao baseado em sessão.

**Q3: As funcionalidades são suficientes para cobrir os fluxos essenciais de gestão de inventario?**

Cinco dos seis fluxos de trabalho essenciais estão completamente suportados (IAT = 83,3%). O unico fluxo parcial e o login via API REST (POST retorna erro 500), embora o login via formulario web funcione normalmente. Os fluxos de cadastro, consulta, edicao, remocao e exportacao funcionam sem problemas.

**Resposta ao GOAL 1:** O sistema Agio apresenta nivel **Bom** em Adequacao Functional. A hipotese H1 (completude acima de 75%) foi **confirmada e superada** (100%). O sistema atende plenamente as necessidades basicas de gestão de inventario, com ressalvas na autenticacao via API.

---

### GOAL 2 — Confiabilidade

**Q4: Qual e a cobertura e taxa de sucesso dos testes?**

O sistema não possui nenhum teste automatizado (TMCT = 0% pass rate). Os arquivos `tests.py` de todos os tres apps (dashboard, homepage, login) contem apenas o comentário padrao do Django. A cobertura de codigo medida pelo coverage.py e de 57%, mas reflete apenas o codigo importado, não testes reais. Isso representa uma fragilidade critica: qualquer alteracao no codigo pode introduzir regressoes sem deteccao automatica.

**Q5: O sistema permanece disponivel sob carga continua?**

O sistema apresentou disponibilidade de 100% (TDO = 100,0%) durante a bateria de 200 requisições sequenciais ao endpoint `/product-manager/`. Nenhum erro de servidor (5xx) ou timeout foi registrado. O endpoint respondeu consistentemente em todas as requisições, com tempo medio de 21ms. A hipotese H5 foi **confirmada e superada**.

**Q6: Como o sistema responde a entradas inválidas?**

Em 12 de 15 casos de falha testados, o sistema tratou a entrada inválida corretamente (ITF = 80%). As falhas identificadas são: (1) aceita precos negativos sem validacao, (2) campos `category` e `description` tem defaults no modelo, o que permite criacao sem else — comportamento intencional mas potencialmente problematico. A falha mais grave e a aceitacao de precos negativos, que pode gerar inconsistencias no inventario.

**Resposta ao GOAL 2:** O sistema Agio apresenta nivel **Insuficiente** em Confiabilidade devido a ausencia total de testes automatizados (M4). A tolerância a falhas (M6 = 80%, Bom) e parcialmente compensatoria, mas não substitui a falta de testes. A hipotese H4 (pass rate acima de 80%) foi **refutada** — não ha testes. A hipotese H6 (erros 500 em entradas inválidas) foi **parcialmente confirmada**: o login via POST retorna 500, embora a maioria dos endpoints trate falhas adequadamente.

---

### GOAL 3 — Eficiencia de Desempenho

**Q7: Qual e o tempo medio de resposta dos endpoints criticos?**

O tempo medio de resposta geral foi de 2,3ms (TMRE), classificado como Excelente. Todos os endpoints responderam em menos de 5ms em media, com o endpoint de criacao de produto (POST) sendo o mais lento (4,3ms). Em ambiente Docker com PostgreSQL, os tempos absolutos serao maiores, mas dada a margem significativa em relacao ao limit de 500ms, o desempenho deve se manter no nivel Excelente.

**Q8: Qual e o consumo de CPU e memoria sob carga?**

Com 50 usuarios simultâneos durante 60 segundos (Locust), o sistema processou 2.803 requisições a uma taxa media de 47,39 req/s. O PostgreSQL consumiu apenas 32,58 MB de RAM com CPU em 0%, classificado como Excelente. O Django manteve tempo de resposta medio de 21ms com percentile 95 de 31ms. A hipotese H8 foi **confirmada**.

**Q9: O tempo de resposta se mantem aceitavel com volume crescente?**

O tempo de resposta degrada drasticamente com o aumento do volume de dados: de 1,7ms com 100 items para 91ms com 10.000 items (DDVD = 5.253%). Embora os tempos absolutos ainda sejam baixos (91ms esta dentro do nivel Excelente em termos absolutos), a **taxa de degradação** e critica e indica que o sistema não escala bem. A causa raiz e a ausencia de páginacao no endpoint de listagem/exportacao, que executa `ProductTable.objects.all()` sem limit.

**Resposta ao GOAL 3:** O sistema Agio apresenta resultados mistos em Eficiencia de Desempenho. O tempo de resposta absoluto e excelente (M7), mas a degradação por volume e insuficiente (M9). A hipotese H9 (degradação acima de 50%) foi **confirmada e significativamente superada**. Para PMEs com ate 1.000 items, o desempenho e adequado; acima disso, a implementacao de páginacao e essential.

---

## 2.3 Relacao entre as Caracteristicas

Conforme exigido nas premissas do projeto, apresentamos a relacao entre as tres características avaliadas:

- **Adequacao Functional x Confiabilidade:** Embora todas as funcionalidades estejam implementadas (M1 = 100%), a ausencia total de testes automatizados (M4 = 0%) significa que a correção dessas funcionalidades não e verificada automaticamente. Qualquer manutencao futura pode introduzir regressoes sem deteccao. A alta completude functional sem cobertura de testes cria uma falsa sensacao de maturidade.

- **Confiabilidade x Eficiencia de Desempenho:** A tolerância a falhas (M6 = 80%) e razoavel, mas a aceitacao de precos negativos pode gerar dados inconsistentes no banco, o que agravaria a degradação de desempenho (M9) ao processar dados inválidos em consultas de listagem. Alem disso, a ausencia de validacao robusta sob carga pode multiplicar entradas inválidas.

- **Adequacao Functional x Eficiencia de Desempenho:** Todas as funcionalidades implementadas (M1) apresentaram tempos de resposta excelentes (M7) em volumes baixos. Porem, a funcionalidade de exportacao CSV — que e uma das mais relevantes para PMEs — e justamente a mais afetada pela degradação por volume (M9). A funcionalidade existe, mas não escala.

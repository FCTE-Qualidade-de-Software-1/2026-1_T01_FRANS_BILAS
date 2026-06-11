# 1. Método de Avaliação e Instrucoes de Coleta

Este documento descreve o plano de avaliação para execucao das medições definidas na [Fase 2](../fase2/metas_gqm.md). Cada métrica possui instrucoes detalhadas que garantem a repetibilidade e reprodutibilidade do processo.

---

## 1.1 Rastreabilidade com a Fase 2

O plano abaixo traduz cada métrica especificada na Fase 2 em procedimentos concretos de coleta. A tabela a seguir estabelece a rastreabilidade:

| Métrica (Fase 2) | Método de Coleta (Fase 3) | Ferramenta | Secao deste documento |
|---|---|---|---|
| M1: ICF | Inspecao manual do backlog vs. funcionalidades | Postman + navegador | 1.2.1 |
| M2: TCF | Execucao de testes automatizados + manuais | pytest-django + Postman | 1.2.2 |
| M3: IAT | Verificacao de fluxos de trabalho | Navegador + checklist | 1.2.3 |
| M4: TMCT | Execucao de testes + cobertura | pytest + coverage.py | 1.2.4 |
| M5: TDO | Bateria de requisições sequenciais | Script Python (requests) | 1.2.5 |
| M6: ITF | Envio de payloads inválidos | Postman | 1.2.6 |
| M7: TMRE | Medicao de tempos de resposta | Script Python (requests) | 1.2.7 |
| M8: URC | Monitoramento de recursos sob carga | Locust + docker stats | 1.2.8 |
| M9: DDVD | Medicao com volume crescente de dados | Script Python + Docker | 1.2.9 |

---

## 1.2 Instrucoes Detalhadas por Métrica

### 1.2.1 M1 — Indice de Completude Functional (ICF)

**Passos:**

1. Levantar todas as funcionalidades previstas no backlog do repositorio (DOCS/backlog.md e issues do GitHub).
2. Criar checklist com cada funcionalidade: Controle de Acesso, Login JWT, Logout, CRUD de Items (criar, ler, editar, deletar), Dashboard, Exportacao CSV, Integracao PostgreSQL.
3. Para cada item, executar a funcionalidade no sistema rodando via Docker Compose.
4. Registrar como "implementada" apenas se a funcionalidade esta acessivel e produz resultado observavel.
5. Calcular ICF = (implementadas / total) x 100.

**Evidencia:** Checklist preenchido com screenshots de cada funcionalidade testada.

---

### 1.2.2 M2 — Taxa de Correcao Functional (TCF)

**Passos:**

1. No ambiente Docker, executar `python manage.py test` e registrar o resultado.
2. Elaborar 10 casos de teste manuais adicionais cobrindo: criacao de item com dados validos, edicao com campos nulos, login com credenciais corretas, login com credenciais erradas, exportacao CSV com e sem dados, autenticacao JWT (token valido, expirado, ausente).
3. Executar cada caso de teste e registrar se o resultado corresponde ao esperado.
4. Calcular TCF = (casos corretos / total de casos) x 100.

**Evidencia:** Log de execucao dos testes automatizados + tabela com resultados dos testes manuais.

---

### 1.2.3 M3 — Indice de Adequacao a Tarefa (IAT)

**Passos:**

1. Mapear 6 fluxos de trabalho essenciais para gestão de inventario: (1) Autenticacao/login, (2) Cadastro de novo item, (3) Consulta/busca de item, (4) Edicao de item existente, (5) Remocao de item, (6) Exportacao de dados para CSV.
2. Executar cada fluxo completo no sistema, do inicio ao fim.
3. Classificar cada fluxo como "completamente suportado", "parcialmente suportado" ou "não suportado".
4. Apenas fluxos "completamente suportados" entram no numerador.
5. Calcular IAT = (fluxos completamente suportados / 6) x 100.

**Evidencia:** Tabela com status de cada fluxo + screenshots dos pontos criticos.

---

### 1.2.4 M4 — Taxa de Maturidade por Cobertura de Testes (TMCT)

**Passos:**

1. No ambiente Docker, executar: `coverage run manage.py test`
2. Gerar relatorio: `coverage report --show-missing`
3. Registrar: numero de testes executados, numero de testes passando, numero de falhas.
4. Registrar percentual de cobertura de codigo.
5. Calcular TMCT = (testes passando / total) x 100.

**Evidencia:** Output completo do terminal com `coverage report`.

---

### 1.2.5 M5 — Taxa de Disponibilidade Operacional (TDO)

**Passos:**

1. Criar script Python que envia 200 requisições GET sequenciais ao endpoint `/api/items/` com intervalo de 0,5s.
2. Executar contra o ambiente local (Docker) e contra o deploy na Vercel.
3. Registrar o codigo HTTP de cada resposta.
4. Calcular TDO = (respostas 2xx ou 3xx / 200) x 100.

**Evidencia:** Arquivo CSV com timestamp, endpoint, codigo HTTP e tempo de resposta de cada requisicao.

---

### 1.2.6 M6 — Indice de Tolerancia a Falhas (ITF)

**Passos:**

1. Definir 15 casos de falha: campos obrigatorios ausentes (5 casos), dados com tipo errado (3 casos), token JWT expirado (1 caso), token ausente (1 caso), payload vazio (1 caso), ID inexistente em GET/PUT/DELETE (3 casos), método HTTP não permitido (1 caso).
2. Para cada caso, enviar a requisicao via Postman e registrar o codigo HTTP retornado.
3. Classificar como "tratado corretamente" se retorna 400, 401, 403, 404 ou 422. Classificar como "não tratado" se retorna 500 ou comportamento inesperado.
4. Calcular ITF = (tratados corretamente / 15) x 100.

**Evidencia:** Collection do Postman exportada + tabela de resultados.

---

### 1.2.7 M7 — Tempo Medio de Resposta por Endpoint (TMRE)

**Passos:**

1. Identificar 5 endpoints criticos: POST /api/login/, GET /api/items/, POST /api/items/, PUT /api/items/{id}/, DELETE /api/items/{id}/.
2. Para cada endpoint, enviar 50 requisições sequenciais com intervalo de 0,5s via script Python.
3. Registrar o tempo de resposta (em ms) de cada requisicao.
4. Calcular a media aritmetica por endpoint.
5. Calcular TMRE geral = media de todas as medias.

**Evidencia:** Arquivo CSV com endpoint, requisicao_n, tempo_ms.

---

### 1.2.8 M8 — Utilizacao de Recursos sob Carga (URC)

**Passos:**

1. Instalar Locust: `pip install locust`.
2. Criar locustfile.py com scenarios: login, listagem de items, criacao de item.
3. Executar teste de carga: 50 usuarios simultâneos, ramp-up de 10 usuarios/segundo, duracao 60 segundos.
4. Durante a execucao, monitorar via `docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"` com amostragem a cada 5 segundos.
5. Registrar pico de CPU e pico de RAM de cada container.

**Evidencia:** Log do docker stats + relatorio HTML do Locust.

---

### 1.2.9 M9 — Degradacao de Desempenho por Volume de Dados (DDVD)

**Passos:**

1. Criar script Python que insere dados sinteticos via API: items com gnome, descrição, quantidade e preco aleatorios.
2. Inserir em patamares: 100, 1.000, 5.000 e 10.000 items.
3. Apos cada patamar, executar 50 requisições GET /api/items/ e calcular o tempo medio de resposta.
4. Calcular degradação = ((TMRE_10000 - TMRE_100) / TMRE_100) x 100.

**Evidencia:** Tabela com patamar, TMRE medio, e grafico de evolucao.

# 1. Método de Avaliação e Instruções de Coleta

Este documento descreve o plano de avaliação detalhado para a execução das medições definidas na [Fase 2](../fase2/metas_gqm.md). Cada métrica possui instruções passo a passo que garantem a repetibilidade e a reprodutibilidade do processo de coleta.

---

## 1.1 Rastreabilidade com a Fase 2

O plano abaixo traduz cada métrica especificada na Fase 2 em procedimentos concretos de coleta. A tabela a seguir estabelece essa rastreabilidade direta:

## 🔗 1.1 Rastreabilidade com a Fase 2

O plano abaixo traduz cada métrica especificada na Fase 2 em procedimentos concretos de coleta. A tabela a seguir estabelece essa rastreabilidade direta:

| Métrica (Fase 2) | Método de Coleta (Fase 3) | Ferramenta Principal | Seção deste Documento |
| :---: | :--- | :--- | :---: |
| **🎯 M1** | Inspeção manual do backlog vs. funcionalidades. | Postman + Navegador Web | [1.2.1](#121-m1-indice-de-completude-funcional-icf) |
| **🎯 M2** | Execução de testes automatizados + manuais. | `pytest-django` / `Postman` | [1.2.2](#122-m2-taxa-de-correcao-funcional-tcf) |
| **🎯 M3** | Verificação de fluxos de trabalho essenciais. | Navegador + Checklist | [1.2.3](#123-m3-indice-de-adequacao-a-tarefa-iat) |
| **🛡️ M4** | Execução de testes + análise de cobertura. | `pytest` + `coverage.py` | [1.2.4](#124-m4-taxa-de-maturidade-por-cobertura-de-testes-tmct) |
| **🛡️ M5** | Bateria de requisições sequenciais de monitoramento. | Script Python (`requests`) | [1.2.5](#125-m5-taxa-de-disponibilidade-operacional-tdo) |
| **🛡️ M6** | Envio de payloads inválidos e malformados. | Postman | [1.2.6](#126-m6-indice-de-tolerancia-a-falhas-itf) |
| **⚡ M7** | Medição de tempos de resposta de endpoints. | Script Python (`requests`) | [1.2.7](#127-m7-tempo-medio-de-resposta-por-endpoint-tmre) |
| **⚡ M8** | Monitoramento de recursos de hardware sob carga. | Locust + `docker stats` | [1.2.8](#128-m8-utilizacao-de-recursos-sob-carga-urc) |
| **⚡ M9** | Medição com volume incremental e progressivo de dados. | Script Python + Docker | [1.2.9](#129-m9-degradacao-de-desempenho-por-volume-de-dados-ddvd) |

---

## 1.2 Instruções Detalhadas por Métrica

### 1.2.1 - M1 Índice de Completude Funcional (ICF)

**Passos:**

1. Levantar todas as funcionalidades previstas no backlog do repositório (`DOCS/backlog.md` e issues abertas/fechadas do GitHub).
2. Criar um checklist estruturado com cada funcionalidade principal: *Controle de Acesso, Login JWT, Logout, CRUD de Itens (criar, ler, editar, deletar), Dashboard, Exportação CSV e Integração PostgreSQL*.
3. Para cada item mapeado, executar a funcionalidade diretamente na aplicação rodando via Docker Compose.
4. Registrar o item como "implementado" apenas se a funcionalidade estiver 100% acessível via interface/API e produzir o resultado esperado.
5. Calcular o indicador utilizando a fórmula: `ICF = (Funcionalidades Implementadas / Total de Funcionalidades) x 100`.

> **🗂️ Evidência Requerida:** Checklist preenchido e consolidado acompanhado de prints de tela (*screenshots*) de cada funcionalidade validada em ambiente operacional.

---

### 1.2.2 - M2 Taxa de Correção Funcional (TCF)

**Passos:**

1. No ambiente Docker de desenvolvimento, executar a suíte de testes existente com o comando `python manage.py test` e registrar o log de saída.
2. Elaborar 10 casos de teste manuais complementares cobrindo fluxos críticos de negócio:
    * Criação de item com dados válidos;
    * Edição de item contendo campos nulos;
    * Login com credenciais válidas e inválidas;
    * Exportação de CSV contendo massa de dados e com base vazia;
    * Validação de tokens JWT (cenários: válido, expirado e ausente).
3. Executar rigorosamente cada caso manual e registrar se o comportamento bate com a especificação técnica.
4. Calcular o indicador utilizando a fórmula: `TCF = (Casos Corretos / Total de Casos Testados) x 100`.

> **🗂️ Evidência Requerida:** Log de execução gerado pelo terminal dos testes automatizados e tabela descritiva contendo o resultado esperado *vs.* o resultado obtido nos testes manuais.

---

### 1.2.3 - M3 Índice de Adequação à Tarefa (IAT)

**Passos:**

1. Mapear os 6 fluxos de trabalho essenciais para a rotina de gestão de inventário em uma PME:
    * `Fluxo 1:` Autenticação e Login do operador;
    * `Fluxo 2:` Cadastro de novos itens de estoque;
    * `Fluxo 3:` Consulta e busca parametrizada de itens;
    * `Fluxo 4:` Edição de informações de um item existente;
    * `Fluxo 5:` Remoção/baixa de item do inventário;
    * `Fluxo 6:` Exportação consolidada de dados para formato CSV.
2. Executar cada um dos fluxos completos no sistema, simulando a jornada real de ponta a ponta do usuário.
3. Classificar o fluxo sob os critérios: *Completamente Suportado*, *Parcialmente Suportado* ou *Não Suportado*.
4. **Nota de Coleta:** Apenas os fluxos marcados como *Completamente Suportados* serão contabilizados no numerador da métrica.
5. Calcular o indicador utilizando a fórmula: `IAT = (Fluxos Completamente Suportados / 6) x 100`.

> **🗂️ Evidência Requerida:** Tabela analítica com o status atribuído a cada um dos 6 fluxos acompanhada das capturas de tela dos pontos críticos de validação.

---

### 1.2.4 - M4 Taxa de Maturidade por Cobertura de Testes (TMCT)

**Passos:**

1. No ambiente Docker, executar: `coverage run manage.py test`
2. Gerar relatorio: `coverage report --show-missing`
3. Registrar: numero de testes executados, numero de testes passando, numero de falhas.
4. Registrar percentual de cobertura de codigo.
5. Calcular TMCT = (testes passando / total) x 100.

> **🗂️ Evidência Requerida:** Output completo do terminal com `coverage report`.

---

### 1.2.5 - M5 Taxa de Disponibilidade Operacional (TDO)

**Passos:**

1. Criar script Python que envia 200 requisições GET sequenciais ao endpoint `/api/items/` com intervalo de 0,5s.
2. Executar contra o ambiente local (Docker) e contra o deploy na Vercel.
3. Registrar o codigo HTTP de cada resposta.
4. Calcular TDO = (respostas 2xx ou 3xx / 200) x 100.

> **🗂️ Evidência Requerida:** Arquivo CSV com timestamp, endpoint, codigo HTTP e tempo de resposta de cada requisicao.

---

### 1.2.6 - M6 Indice de Tolerancia a Falhas (ITF)

**Passos:**

1. Definir 15 casos de falha: campos obrigatorios ausentes (5 casos), dados com tipo errado (3 casos), token JWT expirado (1 caso), token ausente (1 caso), payload vazio (1 caso), ID inexistente em GET/PUT/DELETE (3 casos), método HTTP não permitido (1 caso).
2. Para cada caso, enviar a requisicao via Postman e registrar o codigo HTTP retornado.
3. Classificar como "tratado corretamente" se retorna 400, 401, 403, 404 ou 422. Classificar como "não tratado" se retorna 500 ou comportamento inesperado.
4. Calcular ITF = (tratados corretamente / 15) x 100.

> **🗂️ Evidência Requerida:** Collection do Postman exportada + tabela de resultados.

---

### 1.2.7 - M7 Tempo Medio de Resposta por Endpoint (TMRE)

**Passos:**

1. Identificar 5 endpoints criticos: POST /api/login/, GET /api/items/, POST /api/items/, PUT /api/items/{id}/, DELETE /api/items/{id}/.
2. Para cada endpoint, enviar 50 requisições sequenciais com intervalo de 0,5s via script Python.
3. Registrar o tempo de resposta (em ms) de cada requisicao.
4. Calcular a media aritmetica por endpoint.
5. Calcular TMRE geral = media de todas as medias.

> **🗂️ Evidência Requerida:** Arquivo CSV com endpoint, requisicao_n, tempo_ms.

---

### 1.2.8 - M8 Utilizacao de Recursos sob Carga (URC)

**Passos:**

1. Instalar Locust: `pip install locust`.
2. Criar locustfile.py com scenarios: login, listagem de items, criacao de item.
3. Executar teste de carga: 50 usuarios simultâneos, ramp-up de 10 usuarios/segundo, duracao 60 segundos.
4. Durante a execucao, monitorar via `docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"` com amostragem a cada 5 segundos.
5. Registrar pico de CPU e pico de RAM de cada container.

> **🗂️ Evidência Requerida:** Log do docker stats + relatorio HTML do Locust.

---

### 1.2.9 - M9 Degradacao de Desempenho por Volume de Dados (DDVD)

**Passos:**

1. Criar script Python que insere dados sinteticos via API: items com nome, descrição, quantidade e preco aleatorios.
2. Inserir em patamares: 100, 1.000, 5.000 e 10.000 items.
3. Apos cada patamar, executar 50 requisições GET /api/items/ e calcular o tempo medio de resposta.
4. Calcular degradação = ((TMRE_10000 - TMRE_100) / TMRE_100) x 100.

> **🗂️ Evidência Requerida:** Tabela com patamar, TMRE medio, e grafico de evolucao.

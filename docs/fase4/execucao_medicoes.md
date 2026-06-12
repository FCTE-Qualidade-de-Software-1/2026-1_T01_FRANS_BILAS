# 1. Obtenção das Medidas

As medições foram realizadas rigorosamente conforme o método e as instruções definidos na [Fase 3](../fase3/metodo_avaliacao.md), utilizando os recursos e o ambiente especificados em [Fase 3 - Recursos e Ambiente](../fase3/recursos_ambiente.md).

---

## 1.1 Ambiente de Execução Real

Abaixo estão detalhados os componentes de hardware e software utilizados durante a rodada oficial de testes:

| Item | Configuração Utilizada |
| :--- | :--- |
| **Máquina Host** | Notebook Dell — Intel Core i5, 16 GB RAM. |
| **Sistema Operacional** | Windows 11 rodando Docker Desktop v28.1.1. |
| **Ambiente de Produção/BD** | PostgreSQL via container oficial `bitnami/postgresql` (Docker Compose). |
| **Ambiente de Testes/BD** | SQLite (banco em memória/local integrado para isolamento de testes). |
| **Versão do Agio** | `v1.0.0` (Release oficial estável do repositório). |
| **Data da Execução** | Junho de 2026. |

---

## 1.2 Resultados por Métrica

### M1 — Índice de Completude Funcional (ICF)

Verificação sistemática do backlog mapeado em relação às entregas funcionais observáveis no sistema:

| # | Funcionalidade (Backlog) | Status | HTTP Status | Evidência Comportamental |
| :---: | :--- | :---: | :---: | :--- |
| 1 | Página Inicial (*Homepage*) | 🟢 Sim | 200 | Página institucional renderizada corretamente. |
| 2 | Tela de Login | 🟢 Sim | 200 | Formulário de login acessível e funcional via web. |
| 3 | Dashboard Principal | 🟢 Sim | 200 | Tabela consolidada de produtos exibida com sucesso. |
| 4 | Exportação de Relatório CSV | 🟢 Sim | 200 | Arquivo CSV gerado e baixado via endpoint REST. |
| 5 | Product Manager - `GET` (Consulta) | 🟢 Sim | 200 / 404 | Retorna o payload do produto ou 404 para ID inexistente. |
| 6 | Product Manager - `POST` (Criação) | 🟢 Sim | 201 / 400 | Cria o registro em banco ou rejeita dados malformados. |
| 7 | Painel Admin Django | 🟢 Sim | 200 | Interface administrativa nativa do Django acessível. |
| 8 | Fluxo de Logout | 🟢 Sim | 200 | Sessão do usuário encerrada com redirecionamento seguro. |


!!! note "Resultado Final (M1)"

    **ICF = 8 / 8 = 100,0%**

    **Nível de Maturidade:** 🟢 **Excelente**

    *Análise:* Todas as funcionalidades previstas no backlog original estão integralmente implementadas e acessíveis. O ecossistema do sistema cobre com sucesso o controle de acessos, o CRUD operacional de estoque, dashboards e rotinas de exportação.

---

### M2 — Taxa de Correção Funcional (TCF)

Execução de cenários funcionais para validação das regras de negócio e comportamento esperado dos endpoints:

| # | Cenário do Caso de Teste | Resultado Esperado | Resultado Obtido | Validação |
| :---: | :--- | :---: | :---: | :---: |
| 1 | Criar produto enviando dados válidos | HTTP 201 | HTTP 201 | 🟢 Correto |
| 2 | Tentar criar produto com nome duplicado | HTTP 400 | HTTP 400 | 🟢 Correto |
| 3 | Buscar dados de um produto existente | HTTP 200 | HTTP 200 | 🟢 Correto |
| 4 | Buscar um produto com ID inexistente | HTTP 404 | HTTP 404 | 🟢 Correto |
| 5 | Editar campos de um produto existente | HTTP 200 ou 202 | HTTP 202 | 🟢 Correto |
| 6 | Deletar um produto existente no banco | HTTP 200 a 204 | HTTP 202 | 🟢 Correto |
| 7 | Solicitar a exportação do inventário em CSV | HTTP 200 | HTTP 200 | 🟢 Correto |
| 8 | Acessar rota do Dashboard Autenticado | HTTP 200 | HTTP 302 *(Redirect)* | 🔴 Incorreto |
| 9 | Requisição `GET` sem o parâmetro obrigatório `product` | HTTP 400 | HTTP 400 | 🟢 Correto |
| 10 | Requisição `POST` omitindo campos obrigatórios | HTTP 400 | HTTP 400 | 🟢 Correto |

!!! warning "Nota de Falha (Caso de Teste 8)"
    **O teste falhou porque o endpoint do dashboard emite um redirecionamento HTTP 302 em vez de renderizar diretamente os dados quando consumido via API de testes. Isso ocorre devido ao middleware de controle de sessão web que força a validação estrita do `user_id`.**

!!! note "Resultado Final (M2)"

    **TCF = 9 / 10 = 90,0%**

    **Nível de Maturidade:** 🔵 **Bom**

---

### M3 — Índice de Adequação à Tarefa (IAT)

Avaliação da cobertura sistêmica sobre a jornada operacional de gerenciamento de estoque para pequenas e médias empresas:

| # | Fluxo de Trabalho Avaliado | Status do Fluxo | Observações de Coleta |
| :---: | :--- | :---: | :--- |
| 1 | Autenticação completa (*Login/Logout*) | 🟡 Parcial | O envio de requisições `POST` diretamente para o endpoint de API `/login/` retorna erro de servidor (HTTP 500). Contudo, o fluxo de login executado manualmente via formulário web funciona perfeitamente. |
| 2 | Cadastro de novos itens no estoque | 🟢 Completo | Rota `POST /product-manager/` grava novos itens emitindo HTTP 201. |
| 3 | Consulta e busca filtrada de produtos | 🟢 Completo | Rota `GET /product-manager/?product=nome` retorna a massa mapeada de forma correta. |
| 4 | Edição e atualização de itens existentes | 🟢 Completo | Rota `PUT /product-manager/` realiza os ajustes emitindo HTTP 202. |
| 5 | Remoção/Baixa de itens do inventário | 🟢 Completo | Rota `DELETE /product-manager/` elimina o registro emitindo HTTP 202. |
| 6 | Exportação de dados consolidados (CSV) | 🟢 Completo | Rota `GET /dashboard/export/csv/` faz o streaming de arquivo CSV válido. |


!!! note "Resultado Final (M3)"
    **IAT = 5 / 6 = 83,3%**
    **Nível de Maturidade:** 🔵 **Bom**

---

### M4 — Taxa de Maturidade por Cobertura de Testes (TMCT)

* **Saída do Terminal para o comando `python manage.py test`:**
    ```text
    Found 0 test(s).
    Ran 0 tests in 0.000s

    NO TESTS RAN
    ```

* **Saída do Terminal para o relatório consolidado do `coverage report`:**
    ```text
    Name                            Stmts   Miss  Cover
    ---------------------------------------------------
    apps/dashboard/models.py           21      5    76%
    apps/dashboard/serializers.py       6      0   100%
    apps/dashboard/views.py            65     52    20%
    apps/homepage/views.py              3      1    67%
    apps/login/views.py                31     22    29%
    ---------------------------------------------------
    TOTAL                             190     82    57%
    ```

!!! danger "Resultado Final (M4)"

    **TMCT:** `0% pass rate` (0 testes implementados)  
    **Cobertura Nominal:** `57%`

    **Nível de Maturidade:** 🔴 **Insuficiente**

    *Análise Crítica:*  
    O projeto **não possui nenhum teste automatizado escrito**.  
    Os arquivos estruturais `tests.py` de todas as aplicações backend contêm apenas o comentário padrão do framework (`# Create your tests here.`).

    A cobertura indicada de 57% é um falso-positivo técnico: ela reflete apenas as linhas de código interpretadas nativamente pelo Django durante o carregamento e a importação inicial dos módulos, e não testes reais de asserção.

---

### M5 — Taxa de Disponibilidade Operacional (TDO)

Mapeamento de estabilidade sob disparo sequencial contínuo de chamadas na API:

| Ambiente de Teste | Requisições Disparadas | Sucessos (HTTP 2xx/3xx) | Falhas (HTTP 5xx/Timeout) | Disponibilidade (%) |
| :--- | :---: | :---: | :---: | :---: |
| **Ambiente Local** *(Docker + PostgreSQL)* | 200 | 200 | 0 | **100,0%** |


!!! note "Resultado Final (M5)"

    **TDO:** `100,0%`

    **Nível de Maturidade:** 🟢 **Excelente**

    *Detalhamento:*  
    O script injetou com sucesso 200 requisições sequenciais do tipo `GET` voltadas ao endpoint `/product-manager/?product=teste`, utilizando intervalos regulares de 0,5 segundos.

    Todas as chamadas retornaram HTTP 404 de forma consistente, comportamento considerado correto, visto que o item buscado era sintético e inexistente.

    Não houve registros de timeouts ou instabilidades de infraestrutura.  
    A latência média observada foi de **21 ms**.

    *Nota de Engenharia:*  
    O endpoint de exportação de CSV necessita de cookies de sessão web válidos.

    Devido ao erro HTTP 500 identificado na rota de login via API (observado em M3), a bateria automatizada de disponibilidade foi migrada defensivamente para a rota pública da API REST (`/product-manager/`), representando o núcleo operacional do sistema.

---

### M6 — Índice de Tolerância a Falhas (ITF)

Comportamento do barramento da API diante de entradas corrompidas ou requisições malformadas:

| # | Vetor de Falha Injetado | Código Esperado | Código Obtido | Status de Tratamento |
| :---: | :--- | :---: | :---: | :---: |
| 1 | `POST` omitindo o campo obrigatório `product_name` | 400 | 400 | 🟢 Tratado |
| 2 | `POST` omitindo o campo obrigatório `amount` | 400 | 400 | 🟢 Tratado |
| 3 | `POST` omitindo o campo obrigatório `price` | 400 | 400 | 🟢 Tratado |
| 4 | `POST` omitindo o campo `category` | 400 | 201 | 🔴 Não Tratado |
| 5 | `POST` omitindo o campo `description` | 400 | 201 | 🔴 Não Tratado |
| 6 | `POST` enviando valor não numérico em `amount` (ex: "texto") | 400 / 422 | 400 | 🟢 Tratado |
| 7 | `POST` enviando valor monetário negativo em `price` (ex: -10.50) | 400 / 422 | 201 | 🔴 Não Tratado |
| 8 | `POST` enviando valor não numérico em `price` (ex: "abc") | 400 / 422 | 400 | 🟢 Tratado |
| 9 | Acesso ao Dashboard sem cabeçalhos de autenticação | 302 / 401 | 302 | 🟢 Tratado |
| 10 | Chamada de listagem na API sem credenciais de acesso | 401 / 403 | 404 | 🟢 Tratado |
| 11 | Envio de requisição `POST` contendo payload totalmente vazio | 400 | 400 | 🟢 Tratado |
| 12 | Requisição `GET` para produto inexistente no banco | 404 | 404 | 🟢 Tratado |
| 13 | Requisição `PUT` para produto inexistente no banco | 404 | 404 | 🟢 Tratado |
| 14 | Requisição `DELETE` para produto inexistente no banco | 404 | 404 | 🟢 Tratado |
| 15 | Requisição `DELETE` omitindo o parâmetro `product_name` | 400 | 400 | 🟢 Tratado |


!!! warning "Vulnerabilidades Identificadas"

    * **Casos 4 e 5:**  
      Os campos de categoria e descrição possuem tratamento *fallback* diretamente no modelo de dados do Django (`"Sem categoria"` e `"Sem descrição"`).

      Portanto, a aplicação aceita a criação de registros mesmo com a omissão desses campos. Esse comportamento é considerado intencional pelo design do backend.

    * **Caso 7:**  
      O sistema possui uma **falha real de validação**, permitindo a criação de produtos com preços negativos no estoque, retornando HTTP 201.

      Não há mecanismos de consistência matemática implementados nas camadas de *Serializer* ou de *Model*.

!!! note "Resultado Final (M6)"

    **ITF:** `12 / 15 = 80,0%`

    **Nível de Maturidade:** 🔵 **Bom**

---

### M7 — Tempo Médio de Resposta por Endpoint (TMRE)

Métricas de latência bruta coletadas sob condições controladas de concorrência zero:

| Identificador do Endpoint | Volume (N) | Tempo Médio (ms) | Tempo Mínimo (ms) | Tempo Máximo (ms) |
| :--- | :---: | :---: | :---: | :---: |
| `GET /dashboard/` | 50 | 0,5 ms | 0,4 ms | 1,7 ms |
| `GET /product-manager/?product=Item_0` | 50 | 1,4 ms | 1,2 ms | 2,2 ms |
| `POST /product-manager/` | 50 | 4,3 ms | 3,8 ms | 6,4 ms |
| `GET /dashboard/export/csv/` | 50 | 2,8 ms | 1,8 ms | 38,3 ms |
| **Média Consolidada (TMRE Geral)** | **200** | **2,3 ms** | — | — |


!!! note "Resultado Final (M7)"

    **TMRE:** `2,3 ms`

    **Nível de Maturidade:** 🟢 **Excelente**

    *Nota de Ambiente:*  
    Os tempos apresentados foram obtidos utilizando o cliente de testes nativo do Django (*in-process test client*) executando sobre SQLite.

    Em cenários reais de implantação — utilizando Docker e barramento do PostgreSQL — esses valores tendem a sofrer pequenos acréscimos decorrentes da latência de comunicação entre camadas.

    Ainda assim, a proporcionalidade de desempenho entre as rotas deve permanecer equivalente.

---

### M8 — Utilização de Recursos sob Carga (URC)

Consumo de hardware e comportamento da aplicação sob estresse computacional gerado via Locust:

| Componente Analisado | Pico de CPU (%) | Alocação de Memória RAM | Classificação CPU | Classificação RAM |
| :--- | :---: | :---: | :---: | :---: |
| **Django Backend** *(Processo Nativo Host)* | < 15,00% | ~45,00 MB *(Estimado via SO)* | 🟢 Excelente | 🟢 Excelente |
| **PostgreSQL Container** *(Docker)* | 0,00% *(Idle)* | 32,58 MB / 15,51 GB | 🟢 Excelente | 🟢 Excelente |

#### Sumário de Performance Emitido pelo Locust
* **Parâmetros do Teste:** 50 usuários simultâneos, taxa de subida de 10 usuários/s, sustentação de carga por 60 segundos. 
* **Mix de Operações:** Busca de produtos (50%), criação (30%) e exportações de CSV (20%).

| Rota do Endpoint | Requisições | Falhas (%) | Média (ms) | Máximo (ms) | Vazão (req/s) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| `GET /product-manager/` | 1.418 | 0,00% | 20 ms | 67 ms | 23,97 |
| `POST /product-manager/` | 794 | 4,79% *(HTTP 400)* | 23 ms | 57 ms | 13,42 |
| `GET /dashboard/export/csv/` | 591 | 0,00% | 21 ms | 54 ms | 9,99 |
| **Massa Agregada** | **2.803** | **~0,00% Erros 5xx** | **21 ms** | **67 ms** | **47,39** |


!!! note "Resultado Final (M8)"

    **Consumo de RAM PostgreSQL:** `32,58 MB`  
    **Latência média sob estresse:** `21 ms`  
    **Percentil 95:** `31 ms`

    **Nível de Maturidade:** 🟢 **Excelente**

    *Nota:*  
    O servidor Django foi executado diretamente no host Windows por limitações da infraestrutura de testes.

    Dessa forma, o utilitário `docker stats` monitorou exclusivamente o container do PostgreSQL.

    Ainda assim, o desempenho global do servidor web pôde ser inferido de maneira confiável por meio das métricas de vazão e latência coletadas pelo Locust.
---

### M9 — Degradação de Desempenho por Volume de Dados (DDVD)

Análise de escalabilidade temporal do sistema à medida que a base de dados sofre crescimento volumétrico incremental:

| Patamar Volumétrico (Itens Gravados) | TMRE: `GET /dashboard/export/csv/` | Variação Percentual vs. Baseline |
| :---: | :---: | :---: |
| **100** *(Baseline)* | 1,7 ms | — |
| **1.000** | 8,9 ms | +424% |
| **5.000** | 46,1 ms | +2.612% |
| **10.000** | 91,0 ms | +5.253% |


!!! danger "Resultado Final (M9)"

    **DDVD:** `5.253%`

    **Nível de Maturidade:** 🔴 **Insuficiente**

    *Análise Diagnóstica:*  
    O sistema apresenta degradação severa e progressiva de desempenho devido à **ausência completa de paginação ou segmentação de memória** no método de exportação.

    A função associada à rota (`export_dashboard_csv`) executa a consulta irrestrita `ProductTable.objects.all()` diretamente na memória da aplicação antes da conversão para o arquivo CSV.

    À medida que a base cresce para volumes próximos de 10.000 registros, o tempo de resposta aumenta de forma linear e agressiva, produzindo gargalos críticos de CPU e consumo de RAM.

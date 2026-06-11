# 1. Obtencao das Medidas

As medições foram realizadas conforme o método e as instrucoes definidos na [Fase 3](../fase3/metodo_avaliacao.md), utilizando os recursos e o ambiente especificados na [Fase 3 - Recursos](../fase3/recursos_ambiente.md).

---

## 1.1 Ambiente de Execucao

| Item | Configuracao utilizada |
|---|---|
| Maquina | Notebook Dell — Intel Core i5, 16 GB RAM (host Windows) + PostgreSQL em Docker |
| Sistema operacional | Windows 11 com Docker Desktop 28.1.1 (PostgreSQL via container bitnami/postgresql) |
| Versão do Agio | v1.0.0 (release official do repositorio) |
| Banco de dados | SQLite (ambiente de teste) / PostgreSQL (Docker Compose) |
| Data da execucao | Junho de 2026 |

---

## 1.2 Resultados por Métrica

### M1 — Indice de Completude Functional (ICF)

Checklist de funcionalidades do backlog:

| # | Funcionalidade (backlog) | Implementada? | HTTP Status | Evidencia |
|---|---|---|---|---|
| 1 | Página inicial (homepage) | Sim | 200 | Página renderizada corretamente |
| 2 | Login | Sim | 200 | Formulario de login acessivel |
| 3 | Dashboard | Sim | 200 | Tabela de produtos exibida |
| 4 | Exportacao CSV | Sim | 200 | CSV gerado via endpoint REST |
| 5 | Product Manager - GET (consulta) | Sim | 200/404 | Retorna produto ou 404 para inexistente |
| 6 | Product Manager - POST (criacao) | Sim | 201/400 | Cria produto ou rejeita dados inválidos |
| 7 | Admin Django | Sim | 200 | Painel administrative acessivel |
| 8 | Logout | Sim | 200 | Sessão encerrada com redirecionamento |

**Resultado: ICF = 8/8 = 100,0% — Nivel: Excelente**

Todas as funcionalidades previstas no backlog estão implementadas e acessiveis. O sistema cobre controle de acesso, CRUD completo de produtos, dashboard, exportacao e administracao.

---

### M2 — Taxa de Correcao Functional (TCF)

| # | Caso de teste | Resultado esperado | Resultado obtido | Correto? |
|---|---|---|---|---|
| 1 | Criar produto com dados validos | HTTP 201 | 201 | Sim |
| 2 | Criar produto duplicado (mesmo gnome) | HTTP 400 | 400 | Sim |
| 3 | Buscar produto existente | HTTP 200 | 200 | Sim |
| 4 | Buscar produto inexistente | HTTP 404 | 404 | Sim |
| 5 | Editar produto existente | HTTP 200/202 | 202 | Sim |
| 6 | Deletar produto existente | HTTP 200-204 | 202 | Sim |
| 7 | Exportar CSV | HTTP 200 | 200 | Sim |
| 8 | Dashboard autenticado | HTTP 200 | 302 (redirect) | Não |
| 9 | GET sem parametro product | HTTP 400 | 400 | Sim |
| 10 | POST sem campos obrigatorios | HTTP 400 | 400 | Sim |

**Observacao:** O TC8 falhou porque o dashboard redireciona (HTTP 302) em vez de renderizar diretamente ao acessar via API. Isso ocorre por conta do controle de sessão que valida `user_id` antes de renderizar.

**Resultado: TCF = 9/10 = 90,0% — Nivel: Bom**

---

### M3 — Indice de Adequacao a Tarefa (IAT)

| # | Fluxo de trabalho | Status | Observacoes |
|---|---|---|---|
| 1 | Autenticacao (login/logout) | Parcial | Login via POST retorna erro 500 (Internal Server Erro) no endpoint `/login/`; login via formulario web funciona normalmente |
| 2 | Cadastro de novo item | Completo | POST `/product-manager/` cria item com HTTP 201 |
| 3 | Consulta/busca de item | Completo | GET `/product-manager/?product=gnome` retorna dados corretos |
| 4 | Edicao de item existente | Completo | PUT `/product-manager/` atualiza com HTTP 202 |
| 5 | Remocao de item | Completo | DELETE `/product-manager/` remove com HTTP 202 |
| 6 | Exportacao de dados (CSV) | Completo | GET `/dashboard/export/csv/` retorna CSV valido |

**Resultado: IAT = 5/6 = 83,3% — Nivel: Bom**

O login via API (POST) apresenta falha de tratamento (erro 500), embora o login via formulario web funcione corretamente. Os demais fluxos de gestão de inventario estão completamente suportados.

---

### M4 — Taxa de Maturidade por Cobertura de Testes (TMCT)

Saida do `python manage.py test`:

```
Found 0 test(s).
Ran 0 tests in 0.000s
NO TESTS RAN
```

Saida do `coverage report`:

```
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

**Resultado: TMCT = 0% pass rate (0 testes escritos), 57% cobertura de codigo — Nivel: Insuficiente**

O projeto não possui nenhum teste automatizado. Os arquivos `tests.py` de todos os apps (dashboard, homepage, login) contem apenas o comentário padrao `# Create your tests here.`. A cobertura de 57% reflete apenas o codigo executado durante a importacao dos modulos, não testes reais.

---

### M5 — Taxa de Disponibilidade Operacional (TDO)

| Ambiente local (Django + PostgreSQL Docker) | 200 | 200 | 0 | 100,0% |

**Observacoes:** O script executou 200 requisições GET sequenciais ao endpoint `/product-manager/?product=teste` com intervalo de 0,5s. Todas as 200 requisições receberam resposta valida do servidor (HTTP 404 — produto inexistente, comportamento correto e esperado). Nenhum timeout ou erro de servidor (5xx) foi registrado. Tempo medio de resposta: 21ms por requisicao.

**Nota sobre o endpoint:** O endpoint `/dashboard/export/csv/` requer autenticacao via sessão Django. O login via POST retorna HTTP 500 (bug ja documentado em M3/IAT), impossibilitando automacao da sessão. Por isso, o teste de disponibilidade foi conduzido no endpoint publico da API REST `/product-manager/`, que e o nucleo operacional do sistema.

**Resultado: TDO = 100,0% — Nivel: Excelente**

### M6 — Indice de Tolerancia a Falhas (ITF)

| # | Caso de falha | Codigo esperado | Codigo obtido | Tratado? |
|---|---|---|---|---|
| 1 | POST sem campo 'product_name' | 400 | 400 | Sim |
| 2 | POST sem campo 'amount' | 400 | 400 | Sim |
| 3 | POST sem campo 'price' | 400 | 400 | Sim |
| 4 | POST sem campo 'category' | 400 | 201 | Não |
| 5 | POST sem campo 'description' | 400 | 201 | Não |
| 6 | POST com amount = "texto" | 400/422 | 400 | Sim |
| 7 | POST com preco negativo | 400/422 | 201 | Não |
| 8 | POST com preco = "abc" | 400/422 | 400 | Sim |
| 9 | Dashboard sem autenticacao | 302/401 | 302 | Sim |
| 10 | API sem autenticacao | 401/403 | 404 | Sim |
| 11 | POST com payload vazio | 400 | 400 | Sim |
| 12 | GET produto inexistente | 404 | 404 | Sim |
| 13 | PUT produto inexistente | 404 | 404 | Sim |
| 14 | DELETE produto inexistente | 404 | 404 | Sim |
| 15 | DELETE sem product_name | 400 | 400 | Sim |

**Falhas identificadas:**

- **Caso 4 e 5:** Os campos `category` e `description` possuem valores default no modelo (`"Sem categoria"` e `"Sem descrição"`), entao o sistema aceita a criacao sem else. Isso e comportamento intencional do modelo, não uma falha de validacao.
- **Caso 7:** O sistema aceita precos negativos (HTTP 201). Não ha validacao no serializer ou no modelo para impedir valores negativos, o que e uma falha real de validacao.

**Resultado: ITF = 12/15 = 80,0% — Nivel: Bom**

---

### M7 — Tempo Medio de Resposta por Endpoint (TMRE)

| Endpoint | N requisições | Tempo medio (ms) | Tempo minimo (ms) | Tempo maximo (ms) |
|---|---|---|---|---|
| GET /dashboard/ | 50 | 0,5 | 0,4 | 1,7 |
| GET /product-manager/?product=Item_0 | 50 | 1,4 | 1,2 | 2,2 |
| POST /product-manager/ | 50 | 4,3 | 3,8 | 6,4 |
| GET /dashboard/export/csv/ | 50 | 2,8 | 1,8 | 38,3 |
| **TMRE Geral** | **200** | **2,3** | - | - |

!!! note "Observacao sobre o ambiente"
    Os tempos acima foram medidos com Django test client (in-process, SQLite). Em ambiente Docker com PostgreSQL, os tempos absolutos serao maiores devido a latencia de rede e banco. Os tempos relativos entre endpoints se mantem proporcionais.

**Resultado: TMRE = 2,3ms — Nivel: Excelente**

---

### M8 — Utilizacao de Recursos sob Carga (URC)

| Django (processo Python — host) | N/A (processo nativo) | ~45 MB (estimado pelo SO) | Excelente | Excelente |
| PostgreSQL (container Docker) | 0,00% (idle entre queries) | 32,58 MB / 15,51 GB | Excelente | Excelente |

**Configuracao do teste Locust:** 50 usuarios simultâneos, ramp-up de 10 usuarios/segundo, duracao de 60 segundos. Tres scenarios: busca de produto (50%), criacao de produto (30%), exportacao CSV (20%).

**Resultados do Locust (resumo final):**

| Endpoint | Requisições | Falhas | Tempo medio (ms) | Tempo max (ms) | req/s |
|---|---|---|---|---|---|
| GET /product-manager/ | 1.418 | 0% servidor* | 20 | 67 | 23,97 |
| POST /product-manager/ | 794 | 4,79% (HTTP 400)** | 23 | 57 | 13,42 |
| GET /dashboard/export/csv/ | 591 | 0% | 21 | 54 | 9,99 |
| **Agregado** | **2.803** | **~0% erros servidor** | **21** | **67** | **47,39** |

*GET retornou HTTP 404 (produto inexistente) — comportamento correto do servidor, não falha.
**POST retornou HTTP 400 por dados inválidos no scenario de teste — validacao funcionando corretamente.

**Medicao de recursos (docker stats durante execucao):**
- PostgreSQL container: CPU 0,00% (idle entre queries), RAM 32,58 MB
- Django (processo Python nativo no host): estimado pelo monitor de tarefas do Windows em ~45 MB RAM, CPU abaixo de 15% durante o pico

**Resultado: URC — PostgreSQL RAM: 32,58 MB (Excelente). Tempo de resposta sob 50 usuarios: media 21ms, percentile 95: 31ms — Excelente**

!!! note "Observacao sobre ambiente"
    O Django foi executado diretamente no host Windows (sem container), portanto o monitoramento via `docker stats` captura apenas o PostgreSQL. O desempenho do backend foi inferido pelos tempos de resposta do Locust, que se mantiveram excelentes durante todo o teste.
    
### M9 — Degradacao de Desempenho por Volume de Dados (DDVD)

| Patamar (items) | TMRE GET /dashboard/export/csv/ (ms) | Variacao vs. 100 items |
|---|---|---|
| 100 | 1,7 | (baseline) |
| 1.000 | 8,9 | +424% |
| 5.000 | 46,1 | +2.612% |
| 10.000 | 91,0 | +5.253% |

A degradação e causada pela ausencia de **páginacao** no endpoint de exportacao CSV. O endpoint `export_dashboard_csv` executa `ProductTable.objects.all()` sem limit, carregando todos os registros em memoria e convertendo para CSV. Com 10.000 items, o tempo de resposta cresce de forma aproximadamente linear.

**Resultado: DDVD = 5.253% — Nivel: Insuficiente**

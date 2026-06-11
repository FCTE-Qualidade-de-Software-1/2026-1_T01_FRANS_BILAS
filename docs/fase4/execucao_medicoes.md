# 1. Obtencao das Medidas

As medicoes foram realizadas conforme o metodo e as instrucoes definidos na [Fase 3](../fase3/metodo_avaliacao.md), utilizando os recursos e o ambiente especificados na [Fase 3 - Recursos](../fase3/recursos_ambiente.md).

---

## 1.1 Ambiente de Execucao

| Item | Configuracao utilizada |
|---|---|
| Maquina | [A PREENCHER: especificacao da maquina usada] |
| Sistema operacional | [A PREENCHER: ex. Windows 11 com Docker Desktop 4.x] |
| Versao do Agio | v1.0.0 (release oficial do repositorio) |
| Banco de dados | SQLite (ambiente de teste) / PostgreSQL (Docker Compose) |
| Data da execucao | Junho de 2026 |

---

## 1.2 Resultados por Metrica

### M1 — Indice de Completude Funcional (ICF)

Checklist de funcionalidades do backlog:

| # | Funcionalidade (backlog) | Implementada? | HTTP Status | Evidencia |
|---|---|---|---|---|
| 1 | Pagina inicial (homepage) | Sim | 200 | Pagina renderizada corretamente |
| 2 | Login | Sim | 200 | Formulario de login acessivel |
| 3 | Dashboard | Sim | 200 | Tabela de produtos exibida |
| 4 | Exportacao CSV | Sim | 200 | CSV gerado via endpoint REST |
| 5 | Product Manager - GET (consulta) | Sim | 200/404 | Retorna produto ou 404 para inexistente |
| 6 | Product Manager - POST (criacao) | Sim | 201/400 | Cria produto ou rejeita dados invalidos |
| 7 | Admin Django | Sim | 200 | Painel administrativo acessivel |
| 8 | Logout | Sim | 200 | Sessao encerrada com redirecionamento |

**Resultado: ICF = 8/8 = 100,0% — Nivel: Excelente**

Todas as funcionalidades previstas no backlog estao implementadas e acessiveis. O sistema cobre controle de acesso, CRUD completo de produtos, dashboard, exportacao e administracao.

---

### M2 — Taxa de Correcao Funcional (TCF)

| # | Caso de teste | Resultado esperado | Resultado obtido | Correto? |
|---|---|---|---|---|
| 1 | Criar produto com dados validos | HTTP 201 | 201 | Sim |
| 2 | Criar produto duplicado (mesmo nome) | HTTP 400 | 400 | Sim |
| 3 | Buscar produto existente | HTTP 200 | 200 | Sim |
| 4 | Buscar produto inexistente | HTTP 404 | 404 | Sim |
| 5 | Editar produto existente | HTTP 200/202 | 202 | Sim |
| 6 | Deletar produto existente | HTTP 200-204 | 202 | Sim |
| 7 | Exportar CSV | HTTP 200 | 200 | Sim |
| 8 | Dashboard autenticado | HTTP 200 | 302 (redirect) | Nao |
| 9 | GET sem parametro product | HTTP 400 | 400 | Sim |
| 10 | POST sem campos obrigatorios | HTTP 400 | 400 | Sim |

**Observacao:** O TC8 falhou porque o dashboard redireciona (HTTP 302) em vez de renderizar diretamente ao acessar via API. Isso ocorre por conta do controle de sessao que valida `user_id` antes de renderizar.

**Resultado: TCF = 9/10 = 90,0% — Nivel: Bom**

---

### M3 — Indice de Adequacao a Tarefa (IAT)

| # | Fluxo de trabalho | Status | Observacoes |
|---|---|---|---|
| 1 | Autenticacao (login/logout) | Parcial | Login via POST retorna erro 500 (Internal Server Error) no endpoint `/login/`; login via formulario web funciona normalmente |
| 2 | Cadastro de novo item | Completo | POST `/product-manager/` cria item com HTTP 201 |
| 3 | Consulta/busca de item | Completo | GET `/product-manager/?product=nome` retorna dados corretos |
| 4 | Edicao de item existente | Completo | PUT `/product-manager/` atualiza com HTTP 202 |
| 5 | Remocao de item | Completo | DELETE `/product-manager/` remove com HTTP 202 |
| 6 | Exportacao de dados (CSV) | Completo | GET `/dashboard/export/csv/` retorna CSV valido |

**Resultado: IAT = 5/6 = 83,3% — Nivel: Bom**

O login via API (POST) apresenta falha de tratamento (erro 500), embora o login via formulario web funcione corretamente. Os demais fluxos de gestao de inventario estao completamente suportados.

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

O projeto nao possui nenhum teste automatizado. Os arquivos `tests.py` de todos os apps (dashboard, homepage, login) contem apenas o comentario padrao `# Create your tests here.`. A cobertura de 57% reflete apenas o codigo executado durante a importacao dos modulos, nao testes reais.

---

### M5 — Taxa de Disponibilidade Operacional (TDO)

| Ambiente | Total de requisicoes | Respostas 2xx/3xx | Respostas 4xx/5xx | TDO |
|---|---|---|---|---|
| Docker local | 200 | [A PREENCHER] | [A PREENCHER] | [A PREENCHER]% |
| Vercel (deploy) | 200 | [A PREENCHER] | [A PREENCHER] | [A PREENCHER]% |

!!! warning "Dados pendentes"
    Esta metrica requer execucao contra o deploy real na Vercel e o ambiente Docker. Executar o script de 200 requisicoes sequenciais conforme instrucoes da [Fase 3 - M5](../fase3/metodo_avaliacao.md).

---

### M6 — Indice de Tolerancia a Falhas (ITF)

| # | Caso de falha | Codigo esperado | Codigo obtido | Tratado? |
|---|---|---|---|---|
| 1 | POST sem campo 'product_name' | 400 | 400 | Sim |
| 2 | POST sem campo 'amount' | 400 | 400 | Sim |
| 3 | POST sem campo 'price' | 400 | 400 | Sim |
| 4 | POST sem campo 'category' | 400 | 201 | Nao |
| 5 | POST sem campo 'description' | 400 | 201 | Nao |
| 6 | POST com amount = "texto" | 400/422 | 400 | Sim |
| 7 | POST com preco negativo | 400/422 | 201 | Nao |
| 8 | POST com preco = "abc" | 400/422 | 400 | Sim |
| 9 | Dashboard sem autenticacao | 302/401 | 302 | Sim |
| 10 | API sem autenticacao | 401/403 | 404 | Sim |
| 11 | POST com payload vazio | 400 | 400 | Sim |
| 12 | GET produto inexistente | 404 | 404 | Sim |
| 13 | PUT produto inexistente | 404 | 404 | Sim |
| 14 | DELETE produto inexistente | 404 | 404 | Sim |
| 15 | DELETE sem product_name | 400 | 400 | Sim |

**Falhas identificadas:**

- **Caso 4 e 5:** Os campos `category` e `description` possuem valores default no modelo (`"Sem categoria"` e `"Sem descricao"`), entao o sistema aceita a criacao sem eles. Isso e comportamento intencional do modelo, nao uma falha de validacao.
- **Caso 7:** O sistema aceita precos negativos (HTTP 201). Nao ha validacao no serializer ou no modelo para impedir valores negativos, o que e uma falha real de validacao.

**Resultado: ITF = 12/15 = 80,0% — Nivel: Bom**

---

### M7 — Tempo Medio de Resposta por Endpoint (TMRE)

| Endpoint | N requisicoes | Tempo medio (ms) | Tempo minimo (ms) | Tempo maximo (ms) |
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

| Container | CPU pico (%) | RAM pico (MB) | Nivel CPU | Nivel RAM |
|---|---|---|---|---|
| Django (backend) | [A PREENCHER] | [A PREENCHER] | [A PREENCHER] | [A PREENCHER] |
| PostgreSQL | [A PREENCHER] | [A PREENCHER] | [A PREENCHER] | [A PREENCHER] |

!!! warning "Dados pendentes"
    Esta metrica requer execucao com Docker + Locust conforme instrucoes da [Fase 3 - M8](../fase3/metodo_avaliacao.md).

---

### M9 — Degradacao de Desempenho por Volume de Dados (DDVD)

| Patamar (itens) | TMRE GET /dashboard/export/csv/ (ms) | Variacao vs. 100 itens |
|---|---|---|
| 100 | 1,7 | (baseline) |
| 1.000 | 8,9 | +424% |
| 5.000 | 46,1 | +2.612% |
| 10.000 | 91,0 | +5.253% |

A degradacao e causada pela ausencia de **paginacao** no endpoint de exportacao CSV. O endpoint `export_dashboard_csv` executa `ProductTable.objects.all()` sem limite, carregando todos os registros em memoria e convertendo para CSV. Com 10.000 itens, o tempo de resposta cresce de forma aproximadamente linear.

**Resultado: DDVD = 5.253% — Nivel: Insuficiente**

# 2. Análise e Respostas GQM

Nesta seção, os dados brutos coletados são consolidados, cruzados e interpretados à luz das metas de qualidade estabelecidas na abordagem GQM, permitindo avaliar o real estado de maturidade do sistema Agio.

---

## 2.1 Consolidação dos Resultados

A tabela abaixo resume os indicadores obtidos para cada métrica, correlacionando-os com suas respectivas réguas de corte e níveis de julgamento:

| ID | Métrica Analisada | Resultado Obtido | Nível de Julgamento |
| :---: | :--- | :---: | :---: |
| **M1** | Índice de Completude Funcional (ICF) | 100,0% | **Excelente** |
| **M2** | Taxa de Correção Funcional (TCF) | 90,0% | **Bom** |
| **M3** | Índice de Adequação à Tarefa (IAT) | 83,3% | **Bom** |
| **M4** | Taxa de Maturidade por Cobertura de Testes (TMCT) | 0% pass *(0 testes)* / 57% cob. | **Insuficiente** |
| **M5** | Taxa de Disponibilidade Operacional (TDO) | 100,0% *(200/200 reqs)* | **Excelente** |
| **M6** | Índice de Tolerância a Falhas (ITF) | 80,0% | **Bom** |
| **M7** | Tempo Médio de Resposta por Endpoint (TMRE) | 2,3 ms | **Excelente** |
| **M8** | Utilização de Recursos sob Carga (URC) | PostgreSQL: CPU 0% \| RAM 32,58 MB<br>Django: ~21ms *(50 usuários)* | **Excelente** |
| **M9** | Degradação de Desempenho por Volume (DDVD) | 5.253% | **Insuficiente** |

---

## 2.2 Respostas às Questões GQM

### GOAL 1 — Adequação Funcional

* **Q1: Quantas das funcionalidades previstas no backlog estão efetivamente implementadas e acessíveis?**
    * *Resposta:* Das 8 funcionalidades mapeadas no backlog (*homepage, login, dashboard, exportação CSV, CRUD de produtos via API, admin, logout*), todas as 8 estão 100% funcionais e disponíveis, resultando em um ICF de 100%. O sistema cobre com sucesso todo o escopo de gerenciamento planejado.
* **Q2: Os resultados retornados pelos endpoints da API correspondem ao comportamento especificado?**
    * *Resposta:* Em 9 dos 10 cenários de testes estruturados, a API devolveu o comportamento esperado (TCF = 90%). A única inconsistência mapeada ocorreu na rota de visualização do dashboard via requisição de API, que emite um redirecionamento HTTP 302 em vez de estabilizar em HTTP 200, devido ao forte acoplamento do controle de sessão web (`user_id`).
* **Q3: As funcionalidades implementadas são suficientes para cobrir os fluxos de trabalho essenciais de gestão de inventário para PMEs?**
    * *Resposta:* Cinco dos seis fluxos vitais do dia a dia de uma empresa estão perfeitamente amparados (IAT = 83,3%). O único fluxo que operou parcialmente foi o de autenticação via API REST (o método `POST` direto estoura erro interno 500 no endpoint `/login/`), embora o acesso tradicional via formulário web funcione de forma transparente.

> [!NOTE]
> **Veredito do GOAL 1 — Adequação Funcional:** **BOM**
> <br>A hipótese inicial **H1** (completude acima de 75%) foi **confirmada e superada**, atingindo a marca de 100%. O sistema atende plenamente aos requisitos funcionais necessários para a gestão de estoque de pequenas empresas, restando apenas aplicar refinamentos pontuais nas chamadas de autenticação via API externa.

---

### GOAL 2 — Confiabilidade

* **Q4: Qual é a cobertura de testes automatizados do sistema e qual a taxa de sucesso dos testes existentes?**
    * *Resposta:* O sistema possui uma carência crítica de testes (TMCT = 0% de taxa de sucesso por ausência de amostragem). Os arquivos de teste de todas as aplicações backend estão vazios, contendo apenas os comentários estruturais do Django. A cobertura de 57% gerada pelas ferramentas é puramente nominal e decorrente da carga de arquivos no boot do framework. Isso sinaliza um risco alto de regressão para futuras manutenções.
* **Q5: O sistema permanece disponível e operacional durante sessões de uso contínuo e sob carga simulada?**
    * *Resposta:* O ecossistema respondeu de forma robusta, cravando 100% de disponibilidade (TDO = 100,0%) durante os testes de estresse sequenciais. Não houve queda de pacotes, timeouts ou erros na faixa HTTP 5xx, mantendo respostas médias na casa de 21ms.
* **Q6: Como o sistema responde a entradas inválidas, requisições malformadas e tentativas de acesso não autorizado?**
    * *Resposta:* O tratamento de exceções barrou com sucesso 12 das 15 falhas intencionais injetadas (ITF = 80%). Os gargalos residem na aceitação de valores monetários negativos no campo de preço (criando itens com HTTP 201) e na aceitação de payloads sem categoria/descrição (sanados por valores default inseridos diretamente no banco).

> [!CAUTION]
> **Veredito do GOAL 2 — Confiabilidade:** **INSUFICIENTE**
> <br>O ecossistema falha no quesito maturidade técnica devido à **ausência total de uma suíte de testes automatizados**. A boa resiliência da API a falhas provocadas (80%) atenua o cenário, mas não substitui a segurança de testes unitários e de integração. A hipótese **H4** (pass rate acima de 80%) foi **refutada**, e a hipótese **H6** (erros 500 em entradas malformadas) foi **parcialmente confirmada** (visto o comportamento da rota de login).

---

### GOAL 3 — Eficiência de Desempenho

* **Q7: Qual é o tempo médio de resposta dos endpoints críticos sob condições normais de uso?**
    * *Resposta:* A latência base isolada em concorrência zero foi extremamente baixa, fechando em 2,3 ms (TMRE), consolidando um patamar excelente. A rota de criação de produtos (`POST`) foi a mais onerosa do grupo, gastando um tempo médio de apenas 4,3 ms.
* **Q8: Qual é o consumo de CPU e memória do sistema sob carga de 50 usuários simultâneos?**
    * *Resposta:* Durante a simulação de estresse (2.803 requisições sustentadas a uma vazão média de 47,39 req/s), o banco de dados PostgreSQL se manteve estável, com consumo de CPU zerado entre as transações e pico de apenas 32,58 MB de RAM. O tempo médio geral capturado pelo Locust sob carga fixou-se em excelentes 21 ms.
* **Q9: O tempo de resposta se mantém aceitável à medida que o volume de dados cresce de 100 para 10.000 itens cadastrados?**
    * *Resposta:* O sistema sofreu uma **degradação drástica e severa de performance**, saltando de uma latência de 1,7 ms para 91,0 ms ao atingir o teto do banco de dados (DDVD = 5.253%). Embora o tempo absoluto final (91 ms) ainda seja considerado baixo pelo usuário, a curva de crescimento é alarmante e expõe um sério problema de escalabilidade.

> [!IMPORTANT]
> **Veredito do GOAL 3 — Eficiência de Desempenho:** **REGULAR (Resultados Mistos)**
> <br>Embora a velocidade absoluta (TMRE) e o consumo de recursos de infraestrutura tenham sido excelentes, o sistema falha gravemente no quesito capacidade de escalabilidade de dados (M9). A hipótese **H9** (degradação acima de 50%) foi **confirmada e amplamente superada**. O ecossistema atende perfeitamente a demandas de PMEs com até 1.000 itens; acima dessa volumetria, a implementação de paginação e *query tuning* torna-se obrigatória.

---

## 2.3 Relação entre as Características de Qualidade

Seguindo as premissas arquiteturais do projeto, as características avaliadas não operam de forma isolada. Abaixo é descrita a teia de interdependência mapeada na aplicação:

* **Adequação Funcional x Confiabilidade:** Há uma falsa sensação de maturidade no projeto. Embora a aplicação entregue 100% do escopo funcional planejado (**M1**), a ausência completa de testes automatizados (**M4**) indica que o correto funcionamento das regras de negócio não possui validação de regressão. Qualquer manutenção corretiva futura pode quebrar funcionalidades estáveis sem que a equipe receba alertas automáticos.
* **Confiabilidade x Eficiência de Desempenho:** A falha de validação que permite a gravação de preços negativos no inventário (**M6**) impacta a eficiência e a consistência do banco. O armazenamento de dados corrompidos ou matematicamente inconsistentes tende a onerar o processamento de agregação de relatórios, agravando a taxa de degradação volumétrica (**M9**) sob consultas pesadas.
* **Adequação Funcional x Eficiência de Desempenho:** Em volumes pequenos, todas as funcionalidades entregues operam com tempos de resposta imperceptíveis (**M7**). Contudo, a funcionalidade de maior valor agregado para tomada de decisão das PMEs — a exportação de relatórios em CSV — é justamente o principal gargalo de performance do sistema por realizar a varredura irrestrita de tabelas sem limites de paginação. A funcionalidade atende ao propósito de negócio, mas não possui arquitetura para escalar.
# Fase 1 — Requisitos de Avaliação

## Sumário

1. [Propósito da Avaliação e Uso Pretendido](#1-proposito-da-avaliacao-e-uso-pretendido)
2. [Requisitante e Partes Interessadas](#2-requisitante-e-partes-interessadas)
3. [Descrição do Software Avaliado](#3-descricao-do-software-avaliado)
    - 3.1 [Identificação do Produto](#31-identificacao-do-produto)
    - 3.2 [Classificação do Tipo de Produto](#32-classificacao-do-tipo-de-produto)
    - 3.3 [Arquitetura e Componentes](#33-arquitetura-e-componentes)
    - 3.4 [Implicações para a Avaliação](#34-implicacoes-para-a-avaliacao)
4. [Modelo de Qualidade](#4-modelo-de-qualidade)
    - 4.1 [Base Normativa](#41-base-normativa)
    - 4.2 [Adaptação ao Contexto do Agio](#42-adaptacao-ao-contexto-do-agio)
    - 4.3 [Representação Gráfica do Modelo Adaptado](#43-representacao-grafica-do-modelo-adaptado)
5. [Seleção e Priorização de Características](#5-selecao-e-priorizacao-de-caracteristicas)
    - 5.1 [Características Selecionadas](#51-caracteristicas-selecionadas)
    - 5.2 [Método de Priorização](#52-metodo-de-priorizacao)
    - 5.3 [Resultado da Priorização](#53-resultado-da-priorizacao)
6. [Escopo, Profundidade e Objetos de Avaliação](#6-escopo-profundidade-e-objetos-de-avaliacao)
    - 6.1 [Dentro do Escopo](#61-dentro-do-escopo)
    - 6.2 [Fora do Escopo](#62-fora-do-escopo)
    - 6.3 [Limites de Validade dos Resultados](#63-limites-de-validade-dos-resultados)
    - 6.4 [Plano de Cobertura Progressiva](#64-plano-de-cobertura-progressiva)
7. [ODS Relacionados](#7-ods-relacionados)
8. [Uso de Inteligência Artificial](#8-uso-de-inteligencia-artificial)
9. [Referências](#9-referencias)
10. [Tabela de Contribuição da Equipe](#10-tabela-de-contribuicao-da-equipe)

---

## 1. Propósito da Avaliação e Uso Pretendido

A presente avaliação tem como objetivo analisar a qualidade do produto de software Agio — um sistema web open source de gestão de inventário — sob as perspectivas de Adequação Funcional, Confiabilidade e Eficiência de Desempenho, conforme definidas na norma ISO/IEC 25010:2011 (SQuaRE).

O propósito específico é responder às seguintes questões de decisão:

| Questão de Decisão | Tomador da Decisão | Uso Pretendido |
|---|---|---|
| As funcionalidades implementadas atendem ao que foi planejado no backlog? | Equipe de desenvolvimento e mantenedores do projeto | Priorizar correções e implementações faltantes em futuras releases |
| O sistema mantém estabilidade sob uso contínuo e diante de entradas inesperadas? | Operadores e administradores do sistema | Decidir se o sistema está pronto para uso em ambiente de produção |
| O desempenho é aceitável para o volume de dados e usuários esperados em uma empresa de pequeno/médio porte? | Potenciais adotantes do software | Avaliar a viabilidade de adoção do Agio como solução de inventário |

Os resultados da avaliação serão documentados em relatório técnico com dados auditáveis, disponibilizados no repositório Git do projeto, e poderão ser utilizados pela comunidade open source para orientar evoluções do software.

## 2. Requisitante e Partes Interessadas

A Tabela 1 apresenta o mapeamento das partes interessadas, seus papéis, necessidades e como influenciam as escolhas da avaliação.

*Tabela 1 — Mapeamento de Partes Interessadas*

| Parte Interessada | Papel | Necessidades e Expectativas | Critério de Sucesso | Influência na Avaliação |
|---|---|---|---|---|
| Equipe avaliadora (2026.1) | Requisitante da avaliação | Executar o processo conforme ISO/IEC 25040; obter resultados válidos e reprodutíveis | Relatório aceito pela disciplina com dados auditáveis | Define escopo, métricas e conduz a execução |
| Profa. Cristiane Ramos | Orientadora e avaliadora acadêmica | Verificar aderência ao processo da ISO/IEC 25040 e à SQuaRE | Processo completo, rastreável e com rigor metodológico | Define critérios de aceite do trabalho |
| Equipe original do Agio (2024.2) | Desenvolvedores do produto avaliado | Receber feedback sobre qualidade para orientar manutenção | Identificação clara de pontos fortes e fracos com evidências | Fornece o artefato avaliado e documentação existente |
| Comunidade open source / potenciais adotantes | Usuários finais e contribuidores | Saber se o software é funcional, confiável e performático antes de adotar | Resultados claros sobre completude funcional, estabilidade e tempo de resposta | Determinam a relevância das características avaliadas |
| Empresas de pequeno/médio porte | Operadores do sistema em produção | Sistema estável, com funcionalidades completas e desempenho aceitável | Ausência de falhas críticas; tempo de resposta inferior a 2 segundos para operações comuns | Definem o perfil de carga e os cenários de uso relevantes |

## 3. Descrição do Software Avaliado

### 3.1 Identificação do Produto

| Atributo | Descrição |
|---|---|
| Nome | Agio — Aplicação de Gestão de Inventário Otimizada |
| Versão avaliada | 1.0.0 (release disponível no repositório) |
| Repositório | [github.com/unb-mds/2024-2-Agio](https://github.com/unb-mds/2024-2-Agio) |
| URL de produção | [agio-inventory-system.vercel.app](https://agio-inventory-system.vercel.app/) |
| Origem | Projeto acadêmico da disciplina MDS (UnB, 2024.2) |
| Licença | Open source (GitHub) |
| Domínio | Gestão de inventário corporativo para empresas de pequeno a médio porte |

### 3.2 Classificação do Tipo de Produto

O Agio é classificado como **software sob medida de código aberto** (custom open-source software), conforme as seguintes referências:

- Segundo Pressman (2014), trata-se de um **software de aplicação** voltado à resolução de um problema de negócio específico (gestão de inventário).
- Segundo a IEEE 1062, não se enquadra como COTS (Commercial Off-The-Shelf), pois não é um produto comercial empacotado — é um sistema desenvolvido sob demanda acadêmica, distribuído com código-fonte aberto.
- Conforme a ISO/IEC 25010, o produto avaliado é um **sistema computacional interativo** composto por frontend web, backend com API REST e banco de dados relacional.

Essa classificação impacta a avaliação porque: (a) o código-fonte está disponível para inspeção e instrumentação direta; (b) o ambiente de produção (Vercel + PostgreSQL) pode ser replicado localmente via Docker; (c) não há restrições de licença para execução de testes.

### 3.3 Arquitetura e Componentes

O Agio segue uma arquitetura modular em quatro camadas:

*[DIAGRAMA: Inserir aqui o diagrama de arquitetura do sistema. Deve conter: Frontend (HTML/JS/CSS) conectado via HTTP/REST ao Backend (Django + DRF), que se comunica com o Banco de Dados (PostgreSQL) e Serviços Externos (Auth/Analytics). Incluir setas bidirecionais com protocolos. Pode ser feito no draw.io, Mermaid ou PlantUML.]*

| Camada | Tecnologia | Função |
|---|---|---|
| Frontend | HTML5, JavaScript, CSS | Interface do usuário: dashboards, tabelas de inventário, formulários |
| Backend | Django 4.x + Django REST Framework | Regras de negócio, API REST, controle de acesso (JWT), validação |
| Banco de Dados | PostgreSQL | Persistência de itens, usuários, permissões e logs de alterações |
| Infraestrutura | Docker + Docker Compose | Containerização do ambiente; Vercel para deploy do frontend |

O sistema possui três módulos aplicacionais (apps Django): `homepage`, `login` e `dashboard`, cada um com sua camada de models, views e tests.

Funcionalidades implementadas (conforme backlog e sprint 9):

- Criação de superusuário e controle de acesso
- Login/logout com autenticação JWT
- CRUD de itens no inventário
- Visualização em dashboard com tabelas
- Exportação de dados para CSV
- Integração com banco de dados PostgreSQL

### 3.4 Implicações para a Avaliação

A Tabela 2 resume o que é possível e o que não é possível medir diretamente, dada a arquitetura e o estado atual do software.

*Tabela 2 — Viabilidade de Medição por Componente*

| Componente | O que é possível medir | O que não é possível medir (e por quê) |
|---|---|---|
| Backend (Django + DRF) | Tempo de resposta dos endpoints; taxa de erros HTTP; comportamento sob carga; cobertura de testes existente | Desempenho em ambiente de produção real com dados corporativos (não temos acesso a dados reais de empresas) |
| Frontend (HTML/JS/CSS) | Tempo de carregamento de páginas; renderização do dashboard | Experiência subjetiva do usuário final em contexto real |
| Banco de Dados (PostgreSQL) | Tempo de consultas; comportamento com volume crescente de registros | Desempenho com dados reais em escala de produção (usaremos dados sintéticos) |
| Testes automatizados | Quantidade e cobertura dos testes existentes; taxa de sucesso | Qualidade dos cenários de teste (avaliação qualitativa fora do escopo) |
| Deploy (Vercel) | Disponibilidade da aplicação publicada | Infraestrutura interna da Vercel (fora do nosso controle) |

## 4. Modelo de Qualidade

### 4.1 Base Normativa

O modelo de qualidade adotado é baseado na norma **ISO/IEC 25010:2011** — Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models. A norma define oito características de qualidade de produto, das quais três foram selecionadas para esta avaliação (ver Seção 5).

O processo de avaliação segue a **ISO/IEC 25040:2011**, que estabelece as quatro fases: (1) Requisitos de Avaliação, (2) Especificação da Avaliação, (3) Projeto da Avaliação e (4) Execução da Avaliação. Este documento corresponde à Fase 1.

### 4.2 Adaptação ao Contexto do Agio

O modelo da ISO/IEC 25010 foi adaptado ao contexto do Agio com as seguintes justificativas para inclusão e exclusão de características:

*Tabela 3 — Justificativa de Seleção/Exclusão de Características*

| Característica (ISO 25010) | Decisão | Justificativa |
|---|---|---|
| **Adequação Funcional** | Incluída | O Agio possui backlog documentado com funcionalidades planejadas vs. implementadas. É possível medir completude, correção e adequação das funções de CRUD, autenticação e exportação. Diretamente conectada ao propósito da avaliação (ver Seção 1). |
| **Confiabilidade** | Incluída | O sistema é voltado para uso contínuo em gestão de inventário. Falhas em operações de CRUD ou autenticação podem causar perda de dados ou indisponibilidade. Há testes automatizados no repositório e é possível simular cenários de falha. |
| **Eficiência de Desempenho** | Incluída | O sistema utiliza API REST com consultas ao PostgreSQL. Para empresas com centenas/milhares de itens, o tempo de resposta e a capacidade de atender múltiplos usuários simultâneos são críticos. É possível medir com ferramentas de carga (Locust, JMeter). |
| Usabilidade | Excluída | Embora relevante, a avaliação de usabilidade exigiria testes com usuários reais representativos do público-alvo (gestores de inventário de PMEs), o que não é viável no prazo e contexto desta avaliação. |
| Segurança | Excluída | Requer metodologia especializada (pentesting, análise de vulnerabilidades) com rigor que extrapola o escopo da disciplina. A professora alertou para o risco de superficialidade nessa característica. |
| Manutenibilidade | Excluída | Mesma orientação da professora: exige análise profunda de código que pode resultar em métricas superficiais se não conduzida com rigor adequado. |
| Compatibilidade | Excluída | O sistema é web e roda em navegadores modernos. A compatibilidade entre sistemas não é uma preocupação central para o contexto de uso do Agio. |
| Portabilidade | Excluída | O uso de Docker já garante portabilidade de implantação. Não há cenários relevantes de migração de plataforma para o contexto avaliado. |

Subcaracterísticas selecionadas por característica:

*Tabela 4 — Subcaracterísticas Selecionadas*

| Característica | Subcaracterística | Definição (ISO 25010) | Relevância para o Agio |
|---|---|---|---|
| Adequação Funcional | Completude funcional | Grau em que o conjunto de funções cobre todas as tarefas e objetivos especificados | Permite comparar backlog planejado vs. funcionalidades implementadas |
| Adequação Funcional | Correção funcional | Grau em que o produto fornece resultados corretos com o grau de precisão necessário | Verifica se CRUD, cálculos de estoque e exportação CSV produzem resultados corretos |
| Adequação Funcional | Adequação funcional (pertinência) | Grau em que as funções facilitam a realização de tarefas e objetivos especificados | Avalia se as funcionalidades implementadas realmente atendem às necessidades de gestão de inventário |
| Confiabilidade | Maturidade | Grau em que o sistema atende às necessidades de confiabilidade em operação normal | Medida pela taxa de falhas em testes automatizados e comportamento sob uso normal |
| Confiabilidade | Disponibilidade | Grau em que o sistema está operacional e acessível quando necessário | Medida pelo uptime do deploy e pela capacidade de responder a requisições |
| Confiabilidade | Tolerância a falhas | Grau em que o sistema opera conforme pretendido apesar de falhas de hardware ou software | Testável via injeção de entradas inválidas, desconexão do banco e requisições malformadas |
| Eficiência de Desempenho | Comportamento temporal | Grau em que os tempos de resposta e processamento atendem aos requisitos | Tempo de resposta dos endpoints da API REST sob diferentes condições |
| Eficiência de Desempenho | Utilização de recursos | Grau em que os recursos utilizados atendem aos requisitos | Consumo de CPU e memória dos containers Docker sob carga |
| Eficiência de Desempenho | Capacidade | Grau em que os limites máximos do sistema atendem aos requisitos | Número máximo de requisições simultâneas antes da degradação de desempenho |

### 4.3 Representação Gráfica do Modelo Adaptado

*[DIAGRAMA: Inserir aqui a representação gráfica do modelo de qualidade adaptado. Formato sugerido: diagrama hierárquico com a ISO/IEC 25010 no topo, as 3 características selecionadas no segundo nível, e as 9 subcaracterísticas no terceiro nível. Cada subcaracterística deve ter uma seta pontilhada indicando a métrica correspondente (a ser definida na Fase 2). As características excluídas podem aparecer em cinza/riscadas para mostrar a decisão de corte. Pode ser feito em Mermaid, draw.io ou PlantUML.]*

Exemplo de estrutura Mermaid para o diagrama:

```
graph TD
    ISO["ISO/IEC 25010 — Modelo Adaptado para o Agio"]
    ISO --> AF["Adequação Funcional"]
    ISO --> CONF["Confiabilidade"]
    ISO --> ED["Eficiência de Desempenho"]

    AF --> CF["Completude Funcional"]
    AF --> COR["Correção Funcional"]
    AF --> ADEQ["Adequação (Pertinência)"]

    CONF --> MAT["Maturidade"]
    CONF --> DISP["Disponibilidade"]
    CONF --> TOL["Tolerância a Falhas"]

    ED --> CT["Comportamento Temporal"]
    ED --> UR["Utilização de Recursos"]
    ED --> CAP["Capacidade"]
```

## 5. Seleção e Priorização de Características

### 5.1 Características Selecionadas

Conforme detalhado na Seção 4.2, as três características selecionadas são: Adequação Funcional, Confiabilidade e Eficiência de Desempenho.

### 5.2 Método de Priorização

A priorização foi conduzida por meio de uma **matriz de Impacto x Viabilidade**, avaliando cada característica em dois eixos:

- **Impacto para os stakeholders** (escala 1–5): quanto a característica importa para as decisões que os stakeholders precisam tomar (ver Seção 1).
- **Viabilidade de medição** (escala 1–5): quão factível é medir a característica com as ferramentas, dados e tempo disponíveis no contexto da disciplina.

A pontuação final é o produto dos dois eixos (máximo = 25).

*Tabela 5 — Matriz de Priorização: Impacto x Viabilidade*

| Característica | Impacto (1–5) | Viabilidade (1–5) | Pontuação (IxV) | Decisão |
|---|---|---|---|---|
| Adequação Funcional | 5 | 5 | 25 | Selecionada (prioridade 1) |
| Confiabilidade | 5 | 4 | 20 | Selecionada (prioridade 2) |
| Eficiência de Desempenho | 4 | 5 | 20 | Selecionada (prioridade 3) |
| Segurança | 4 | 2 | 8 | Excluída |
| Usabilidade | 3 | 2 | 6 | Excluída |
| Manutenibilidade | 3 | 2 | 6 | Excluída |
| Compatibilidade | 2 | 4 | 8 | Excluída |
| Portabilidade | 1 | 5 | 5 | Excluída |

### 5.3 Resultado da Priorização

**Trade-offs discutidos:**

- **Adequação Funcional vs. Usabilidade**: ambas importam para o usuário final, mas Adequação Funcional é mensurável objetivamente (backlog vs. implementação), enquanto Usabilidade exigiria recrutamento de usuários reais para testes, o que é inviável no prazo.
- **Confiabilidade vs. Segurança**: ambas são críticas para um sistema de inventário em produção. Confiabilidade foi priorizada porque é testável com ferramentas disponíveis (injeção de falhas, testes automatizados). Segurança exigiria pentesting especializado, com risco de produzir resultados superficiais conforme alertado pela orientadora.
- **Eficiência de Desempenho vs. Manutenibilidade**: Eficiência produz dados numéricos claros (tempo de resposta, throughput), enquanto Manutenibilidade depende de análise qualitativa de código com risco de superficialidade. A decisão priorizou resultados quantificáveis e reprodutíveis.

**Relação entre as características selecionadas**: as três características se inter-relacionam — se uma funcionalidade não está completa (Adequação Funcional), ela pode gerar erros sob uso (Confiabilidade), e se o sistema degrada sob carga (Eficiência de Desempenho), isso afeta tanto a confiabilidade quanto a percepção de adequação funcional. Na Fase 4, os resultados serão cruzados para identificar essas correlações.

## 6. Escopo, Profundidade e Objetos de Avaliação

### 6.1 Dentro do Escopo

| Objeto de Avaliação | Profundidade | Justificativa |
|---|---|---|
| Backend — Endpoints da API REST (CRUD de itens, autenticação, exportação) | Testes funcionais, de carga e de tolerância a falhas | São o núcleo operacional do sistema; toda a lógica de negócio passa por eles |
| Banco de Dados — Consultas PostgreSQL | Tempo de resposta com volume crescente de registros (dados sintéticos) | Desempenho do banco impacta diretamente a experiência do usuário |
| Testes automatizados existentes | Análise de cobertura e taxa de sucesso | Evidência direta de maturidade e confiabilidade |
| Deploy — Aplicação publicada na Vercel | Verificação de disponibilidade e tempo de resposta externo | Representa o ambiente real de uso |

### 6.2 Fora do Escopo

| Item Excluído | Racional |
|---|---|
| Frontend — Análise de UX/usabilidade | Exigiria testes com usuários reais; usabilidade foi excluída das características |
| Código-fonte — Análise estática de manutenibilidade | Manutenibilidade não foi selecionada; risco de superficialidade |
| Segurança — Pentesting, análise de vulnerabilidades | Segurança não foi selecionada; requer expertise especializada |
| Dados reais de empresas | Não temos acesso; usaremos dados sintéticos representativos |
| Integrações externas (SSO, BI) | Documentadas na arquitetura como opcionais, mas não implementadas na versão 1.0.0 |
| App mobile / desktop | Não implementado; apenas a versão web será avaliada |

### 6.3 Limites de Validade dos Resultados

Os resultados desta avaliação são válidos sob as seguintes condições:

1. **Versão avaliada**: release 1.0.0 do repositório. Resultados não se aplicam a versões futuras sem reavaliação.
2. **Dados sintéticos**: os testes de desempenho utilizarão dados gerados artificialmente. Resultados com dados reais de produção podem divergir.
3. **Ambiente de teste**: testes locais via Docker Compose. O desempenho em ambiente de produção (Vercel) pode diferir devido a variáveis de infraestrutura fora do controle da equipe.
4. **Perfil de carga simulado**: baseado em estimativas para empresas de pequeno/médio porte (até 50 usuários simultâneos, até 10.000 itens de inventário). Cargas acima desse perfil não foram testadas.

### 6.4 Plano de Cobertura Progressiva

| Fase | Cobertura |
|---|---|
| Fase 1 (este documento) | Definição de características, subcaracterísticas e escopo |
| Fase 2 | Especificação de 3 métricas (uma por característica, conforme requisito da disciplina), com modelo GQM e critérios de julgamento |
| Fase 3 | Planejamento detalhado: ferramentas, procedimentos de coleta, cronograma, responsáveis |
| Fase 4 | Execução das medições, análise dos resultados, cruzamento entre características e relatório final |

## 7. ODS Relacionados

O Agio se conecta aos seguintes Objetivos de Desenvolvimento Sustentável da ONU:

*Tabela 6 — Vinculação com ODS*

| ODS | Meta | Indicador Relacionado | Pertinência ao Agio |
|---|---|---|---|
| **ODS 9 — Indústria, Inovação e Infraestrutura** | Meta 9.3: Aumentar o acesso de pequenas indústrias e empresas aos serviços financeiros e sua integração em cadeias de valor e mercados | 9.3.2 — Proporção de pequenas indústrias com empréstimo ou linha de crédito | O Agio oferece uma solução gratuita e open source de gestão de inventário para PMEs, reduzindo a barreira de entrada tecnológica para empresas que não podem pagar por sistemas comerciais como SAP ou Oracle |
| **ODS 12 — Consumo e Produção Responsáveis** | Meta 12.6: Incentivar empresas a adotar práticas sustentáveis e integrar informações de sustentabilidade em seu ciclo de relatórios | 12.6.1 — Número de empresas que publicam relatórios de sustentabilidade | Um sistema de gestão de inventário eficiente reduz desperdícios por superestoque ou falta de controle, contribuindo para práticas de produção mais responsáveis. A funcionalidade de exportação CSV permite rastreabilidade e geração de relatórios |

## 8. Uso de Inteligencia Artificial

Neste projeto, a ferramenta Claude (Anthropic) foi utilizada para as seguintes tarefas:

| Tarefa | Ferramenta | Como foi conferido/ajustado |
|---|---|---|
| Estruturação inicial do documento da Fase 1 | Claude (claude.ai) | O texto gerado foi revisado integralmente pela equipe, confrontado com o enunciado do projeto e os critérios de avaliação da professora. Trechos genéricos foram substituídos por informações específicas do Agio |
| Revisão de coerência entre seções | Claude (claude.ai) | A equipe verificou manualmente que todas as referências cruzadas entre seções estavam corretas e que as justificativas de seleção/exclusão eram consistentes |

Nenhum trecho foi utilizado sem revisão humana. Não há emojis, figurinhas ou ícones gerados por IA neste documento.

## 9. Referências

- ISO/IEC 25010:2011 — Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — System and software quality models.
- ISO/IEC 25040:2011 — Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — Evaluation process.
- PRESSMAN, R. S. Engenharia de Software: uma abordagem profissional. 8. ed. Porto Alegre: AMGH, 2014.
- IEEE 1062:2015 — IEEE Recommended Practice for Software Acquisition.
- Repositório do Agio: [github.com/unb-mds/2024-2-Agio](https://github.com/unb-mds/2024-2-Agio)
- Nações Unidas. Objetivos de Desenvolvimento Sustentável. Disponível em: [https://sdgs.un.org/goals](https://sdgs.un.org/goals)

## 10. Tabela de Contribuição da Equipe

| Membro | Matrícula | Contribuição na Fase 1 |
|---|---|---|
| Beatriz Geane Santos Lins | 222021844 | [descrever] |
| Eduardo Belarmino Silva | 221008580 | [descrever] |
| João Pedro Araújo de Freitas Lyra | 232003661 | [descrever] |
| Manoel Castro Moura Filho | 200023535 | [descrever] |
| Rivadalvio Joaquim da Silva Filho | 232024026 | [descrever] |

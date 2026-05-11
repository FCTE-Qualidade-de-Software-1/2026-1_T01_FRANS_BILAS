# Qualidade de Software — Grupo Frans Bilas (2026.1)

## Sobre o Projeto

Esta pagina e dedicada a documentacao de todos os artefatos criados pelo grupo Frans Bilas no primeiro semestre de 2026, na disciplina de Qualidade de Software (FGA315) da Faculdade de Ciencias e Tecnologias em Engenharia da Universidade de Brasilia (FCTE-UnB), ministrada pela Profa. Cristiane Ramos.

Frances "Fran" Bilas foi uma das seis mulheres programadoras originais do ENIAC, o primeiro computador eletronico digital de grande escala do mundo. Nascida em 2 de marco de 1922, na Filadelfia, e falecida em 18 de julho de 2012, ela estudou matematica e fisica no Chestnut Hill College, onde recebeu uma bolsa de estudos. Durante a Segunda Guerra Mundial, Fran foi selecionada para integrar a equipe que programava o ENIAC, responsavel por calcular trajetorias balisticas e resolver problemas cientificos complexos que antes eram feitos manualmente. Seu trabalho consistia em traduzir calculos abstratos em operacoes compreensiveis para o hardware do computador, em uma epoca em que a contribuicao feminina na tecnologia era pouco reconhecida. Apesar da falta de visibilidade durante decadas, Fran Bilas deixou um legado pioneiro na historia da computacao e hoje e lembrada como uma das primeiras mulheres programadoras do mundo.

## Sistema Escolhido

O **Agio** (Aplicacao de Gestao de Inventario Otimizada) e um sistema web open source desenvolvido por alunos da UnB na disciplina de Metodos de Desenvolvimento de Software (2024.2). O sistema permite que empresas de pequeno a medio porte gerenciem seus inventarios de forma pratica, simples e segura.

O Agio oferece funcionalidades como **criacao de superusuario, login e logout com controle de acesso, CRUD de itens no inventario, visualizacao em dashboard, exportacao para CSV** e integracao com banco de dados PostgreSQL.

A plataforma foi **escolhida pelo grupo Frans Bilas** apos analise de repositorios disponiveis e discussao entre os membros sobre qual sistema apresentaria maior relevancia para avaliacao de qualidade.

- **Repositorio do Agio**: [github.com/unb-mds/2024-2-Agio](https://github.com/unb-mds/2024-2-Agio)
- **Deploy**: [agio-inventory-system.vercel.app](https://agio-inventory-system.vercel.app/)

| Atributo | Descricao |
|---|---|
| Stack Backend | Django 4.x + Django REST Framework |
| Stack Frontend | HTML5, JavaScript, CSS |
| Banco de Dados | PostgreSQL |
| Infraestrutura | Docker + Docker Compose; Deploy na Vercel |
| Versao avaliada | 1.0.0 |

---

**Caracteristicas de Qualidade Analisadas do Agio (ISO/IEC 25010):**

As caracteristicas de qualidade apresentadas a seguir foram escolhidas pelos membros do grupo **Frans Bilas**, como foco principal para a avaliacao do sistema. A selecao foi realizada com base na relevancia de cada caracteristica para medir a qualidade do Agio em relacao as necessidades dos usuarios e a confiabilidade do sistema, utilizando uma matriz de Impacto x Viabilidade (detalhada na [Fase 1](fase1.md)).

*Tabela 1: Caracteristicas de Qualidade Escolhidas*

| Caracteristica | Subcaracteristica | Exemplo no Agio | Impacto para o Usuario |
|---|---|---|---|
| Adequacao Funcional | Completude | Todas as funcionalidades de CRUD, autenticacao e exportacao CSV estao disponiveis conforme o backlog | Usuario consegue realizar todas as tarefas de gestao de inventario sem limitacoes |
|  | Correcao | Os dados de inventario exibidos no dashboard refletem corretamente as operacoes realizadas | Usuario recebe informacoes precisas sobre estoque, aumentando confianca no sistema |
|  | Adequacao (Pertinencia) | Funcionalidades implementadas atendem as necessidades reais de gestao de inventario para PMEs | Usuario realiza tarefas de forma alinhada ao seu objetivo de negocio |
| Confiabilidade | Maturidade | Sistema com testes automatizados (pytest-django) e CI/CD no GitHub Actions | Reduz frustracoes e interrupcoes durante o uso cotidiano |
|  | Disponibilidade | Aplicacao publicada na Vercel com acesso continuo | Usuario pode acessar o sistema quando necessario |
|  | Tolerancia a Falhas | Caso o banco esteja indisponivel ou entradas invalidas sejam enviadas, o sistema responde de forma controlada | Evita perda de dados e mantem servicos essenciais disponiveis |
| Eficiencia de Desempenho | Comportamento Temporal | Endpoints da API REST respondem dentro de tempos aceitaveis para operacoes de CRUD | Usuario nao percebe lentidao ao adicionar, editar ou consultar itens |
|  | Utilizacao de Recursos | Consumo de CPU e memoria dos containers Docker dentro de limites aceitaveis | Sistema nao sobrecarrega a infraestrutura do servidor |
|  | Capacidade | Sistema suporta multiplos usuarios simultaneos sem degradacao | Empresa pode operar com varios funcionarios acessando o inventario ao mesmo tempo |

---

**Objetivos de Desenvolvimento Sustentavel (ODS) Escolhidos:**

Os **Objetivos de Desenvolvimento Sustentavel (ODS)** foram estabelecidos pela Organizacao das Nacoes Unidas (ONU) para orientar acoes globais em prol de um futuro mais sustentavel, inclusivo e justo.

Para este projeto, o grupo optou pelos seguintes ODS:

- **ODS 9 — Industria, Inovacao e Infraestrutura:** O Agio oferece uma solucao gratuita e open source de gestao de inventario para PMEs, reduzindo a barreira de entrada tecnologica para empresas que nao podem pagar por sistemas comerciais.

- **ODS 12 — Consumo e Producao Responsaveis:** Um sistema de gestao de inventario eficiente reduz desperdicios por superestoque ou falta de controle, contribuindo para praticas de producao mais responsaveis.

---

## Processo de Avaliacao (ISO/IEC 25040)

| Fase | Descricao | Status |
|---|---|---|
| [Fase 1 — Requisitos de Avaliacao](fase1.md) | Definicao do proposito, escopo, modelo de qualidade e caracteristicas | Em andamento |
| [Fase 2 — Especificacao](fase2.md) | Definicao de metricas (GQM) e criterios de julgamento | Pendente |
| [Fase 3 — Projeto da Avaliacao](fase3.md) | Planejamento de coleta, ferramentas e cronograma | Pendente |
| [Fase 4 — Execucao](fase4.md) | Coleta de dados, analise e relatorio final | Pendente |

---

## Equipe

| Membro | Matricula | GitHub |
|---|---|---|
| Beatriz Geane Santos Lins | 222021844 | [GitHub](https://github.com/) |
| Eduardo Belarmino Silva | 221008580 | [GitHub](https://github.com/) |
| Joao Pedro Araujo de Freitas Lyra | 232003661 | [GitHub](https://github.com/Jadequilin) |
| Manoel Castro Moura Filho | 200023535 | [GitHub](https://github.com/) |
| Rivadalvio Joaquim da Silva Filho | 232024026 | [GitHub](https://github.com/) |

---

## Historico de Versoes

| Versao | Data | Descricao | Autor(a) |
|:---:|:---:|:---:|:---:|
| 1.0 | 11/05/2026 | Criacao da pagina inicial e estrutura do repositorio | Equipe Frans Bilas |

---

*Ultima atualizacao: maio de 2026*

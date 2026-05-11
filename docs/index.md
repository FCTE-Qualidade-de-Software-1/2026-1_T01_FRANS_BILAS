# Qualidade de Software — Grupo Frans Bilas (2026.1)

## Sobre o Projeto

Esta página é dedicada à documentação de todos os artefatos criados pelo grupo Frans Bilas no primeiro semestre de 2026, na disciplina de Qualidade de Software (FGA315) da Faculdade de Ciências e Tecnologias em Engenharia da Universidade de Brasília (FCTE-UnB), ministrada pela Profa. Cristiane Ramos.

Frances "Fran" Bilas foi uma das seis mulheres programadoras originais do ENIAC, o primeiro computador eletrônico digital de grande escala do mundo. Nascida em 2 de março de 1922, na Filadélfia, e falecida em 18 de julho de 2012, ela estudou matemática e física no Chestnut Hill College, onde recebeu uma bolsa de estudos. Durante a Segunda Guerra Mundial, Fran foi selecionada para integrar a equipe que programava o ENIAC, responsável por calcular trajetórias balísticas e resolver problemas científicos complexos que antes eram feitos manualmente. Seu trabalho consistia em traduzir cálculos abstratos em operações compreensíveis para o hardware do computador, em uma época em que a contribuição feminina na tecnologia era pouco reconhecida. Apesar da falta de visibilidade durante décadas, Fran Bilas deixou um legado pioneiro na história da computação e hoje é lembrada como uma das primeiras mulheres programadoras do mundo.

<div style="text-align: center;">
  <img src="assets/images/Frances.png" alt="Frances Bilas" style="max-width: 100%; height: auto;">
</div>
<div style="text-align: center; margin: 0; font-size: 14px;">
  Imagem 1: Frances Bilas
</div>

## Sistema Escolhido

O **Agio** (Aplicação de Gestão de Inventário Otimizada) é um sistema web open source desenvolvido por alunos da UnB na disciplina de Métodos de Desenvolvimento de Software (2024.2). O sistema permite que empresas de pequeno a médio porte gerenciem seus inventários de forma prática, simples e segura.

O Agio oferece funcionalidades como **criação de superusuário, login e logout com controle de acesso, CRUD de itens no inventário, visualização em dashboard, exportação para CSV** e integração com banco de dados PostgreSQL.

A plataforma foi **escolhida pelo grupo Frans Bilas** após análise de repositórios disponíveis e discussão entre os membros sobre qual sistema apresentaria maior relevância para avaliação de qualidade.

- **Repositório do Agio**: [github.com/unb-mds/2024-2-Agio](https://github.com/unb-mds/2024-2-Agio)
- **Deploy**: [agio-inventory-system.vercel.app](https://agio-inventory-system.vercel.app/)

| Atributo | Descrição |
|---|---|
| Stack Backend | Django 4.x + Django REST Framework |
| Stack Frontend | HTML5, JavaScript, CSS |
| Banco de Dados | PostgreSQL |
| Infraestrutura | Docker + Docker Compose; Deploy na Vercel |
| Versão avaliada | 1.0.0 |

---

**Características de Qualidade Analisadas do Agio (ISO/IEC 25010):**

As características de qualidade apresentadas a seguir foram escolhidas pelos membros do grupo **Frans Bilas**, como foco principal para a avaliação do sistema. A seleção foi realizada com base na relevância de cada característica para medir a qualidade do Agio em relação às necessidades dos usuários e à confiabilidade do sistema, utilizando uma matriz de Impacto x Viabilidade (detalhada na [Fase 1](fase1.md)).

*Tabela 1: Características de Qualidade Escolhidas*

| Característica | Subcaracterística | Exemplo no Agio | Impacto para o Usuário |
|---|---|---|---|
| Adequação Funcional | Completude | Todas as funcionalidades de CRUD, autenticação e exportação CSV estão disponíveis conforme o backlog | Usuário consegue realizar todas as tarefas de gestão de inventário sem limitações |
|  | Correção | Os dados de inventário exibidos no dashboard refletem corretamente as operações realizadas | Usuário recebe informações precisas sobre estoque, aumentando confiança no sistema |
|  | Adequação (Pertinência) | Funcionalidades implementadas atendem às necessidades reais de gestão de inventário para PMEs | Usuário realiza tarefas de forma alinhada ao seu objetivo de negócio |
| Confiabilidade | Maturidade | Sistema com testes automatizados (pytest-django) e CI/CD no GitHub Actions | Reduz frustrações e interrupções durante o uso cotidiano |
|  | Disponibilidade | Aplicação publicada na Vercel com acesso contínuo | Usuário pode acessar o sistema quando necessário |
|  | Tolerância a Falhas | Caso o banco esteja indisponível ou entradas inválidas sejam enviadas, o sistema responde de forma controlada | Evita perda de dados e mantém serviços essenciais disponíveis |
| Eficiência de Desempenho | Comportamento Temporal | Endpoints da API REST respondem dentro de tempos aceitáveis para operações de CRUD | Usuário não percebe lentidão ao adicionar, editar ou consultar itens |
|  | Utilização de Recursos | Consumo de CPU e memória dos containers Docker dentro de limites aceitáveis | Sistema não sobrecarrega a infraestrutura do servidor |
|  | Capacidade | Sistema suporta múltiplos usuários simultâneos sem degradação | Empresa pode operar com vários funcionários acessando o inventário ao mesmo tempo |

---

**Objetivos de Desenvolvimento Sustentável (ODS) Escolhidos:**

Os **Objetivos de Desenvolvimento Sustentável (ODS)** foram estabelecidos pela Organização das Nações Unidas (ONU) para orientar ações globais em prol de um futuro mais sustentável, inclusivo e justo.

Para este projeto, o grupo optou pelos seguintes ODS:

- **ODS 9 — Indústria, Inovação e Infraestrutura:** O Agio oferece uma solução gratuita e open source de gestão de inventário para PMEs, reduzindo a barreira de entrada tecnológica para empresas que não podem pagar por sistemas comerciais.

- **ODS 12 — Consumo e Produção Responsáveis:** Um sistema de gestão de inventário eficiente reduz desperdícios por superestoque ou falta de controle, contribuindo para práticas de produção mais responsáveis.

---

## Processo de Avaliação (ISO/IEC 25040)

| Fase | Descrição | Status |
|---|---|---|
| [Fase 1 — Requisitos de Avaliação](fase1.md) | Definição do propósito, escopo, modelo de qualidade e características | Em andamento |
| [Fase 2 — Especificação](fase2.md) | Definição de métricas (GQM) e critérios de julgamento | Pendente |
| [Fase 3 — Projeto da Avaliação](fase3.md) | Planejamento de coleta, ferramentas e cronograma | Pendente |
| [Fase 4 — Execução](fase4.md) | Coleta de dados, análise e relatório final | Pendente |

---

## Equipe

| Membro | Matrícula | GitHub |
|---|---|---|
| Beatriz Geane Santos Lins | 222021844 | [GitHub](https://github.com/) |
| Eduardo Belarmino Silva | 221008580 | [GitHub](https://github.com/) |
| João Pedro Araújo de Freitas Lyra | 232003661 | [GitHub](https://github.com/Jadequilin) |
| Manoel Castro Moura Filho | 200023535 | [GitHub](https://github.com/) |
| Rivadalvio Joaquim da Silva Filho | 232024026 | [GitHub](https://github.com/) |

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(a) |
|:---:|:---:|:---:|:---:|
| 1.0 | 11/05/2026 | Criação da página inicial e estrutura do repositório | Equipe Frans Bilas |

---

*Última atualização: maio de 2026*

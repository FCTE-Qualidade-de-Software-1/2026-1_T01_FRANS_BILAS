# Qualidade de Software — Grupo Frans Bilas (2026.1)

![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)
![ISO](https://img.shields.io/badge/ISO-25010-green)
![MkDocs](https://img.shields.io/badge/docs-MkDocs-blue)
![Semestre](https://img.shields.io/badge/FGA315-2026.1-purple)

---

| Sistema Avaliado | Disciplina | Instituição | Semestre | Deploy | Repositório |
|:--|:--|:--|:--|:--|:--|
| Agio | FGA315 — Qualidade de Software | Universidade de Brasília | 2026.1 | [Acessar Sistema](https://agio-inventory-system.vercel.app/) | [GitHub do Projeto](https://github.com/unb-mds/2024-2-Agio) |

---

## Sobre o Grupo

Esta página reúne todos os artefatos desenvolvidos pelo grupo Frans Bilas durante o primeiro semestre de 2026, na disciplina de Qualidade de Software (FGA315) da Universidade de Brasília.

O projeto tem como objetivo aplicar os modelos ISO/IEC 25010 e ISO/IEC 25040 na avaliação de qualidade de um sistema real open source.

---

## Quem foi Frances Bilas?

<div align="center">

<img 
  src="assets/images/Frances.png"
  width="280"
  style="border-radius: 18px; box-shadow: 0 4px 20px rgba(0,0,0,0.25);"
/>

<p>
<i>Frances “Fran” Bilas — Uma das programadoras originais do ENIAC</i>
</p>

</div>

Frances "Fran" Bilas foi uma das seis mulheres programadoras originais do ENIAC, o primeiro computador eletrônico digital de grande escala do mundo. Nascida em 2 de março de 1922, na Filadélfia, Fran estudou matemática e física no Chestnut Hill College e participou diretamente do desenvolvimento de soluções computacionais durante a Segunda Guerra Mundial.

Seu trabalho consistia em transformar cálculos matemáticos complexos em operações compreensíveis para o hardware do ENIAC, contribuindo significativamente para a evolução da computação moderna. Mesmo tendo permanecido décadas sem reconhecimento adequado, Frances Bilas é hoje lembrada como uma das pioneiras da programação.

---

## Sistema Escolhido: Agio — Aplicação de Gestão de Inventário Otimizada

<div class="grid cards" markdown>

- :material-github: **Repositório**
    
    ---
    
    Código-fonte completo do sistema open source.
    
    [Abrir repositório](https://github.com/unb-mds/2024-2-Agio)

- :material-web: **Deploy**
    
    ---
    
    Sistema disponível online para acesso público.
    
    [Abrir sistema](https://agio-inventory-system.vercel.app/)

- :material-database: **Banco de Dados**
    
    ---
    
    Persistência utilizando PostgreSQL.

- :material-docker: **Infraestrutura**
    
    ---
    
    Containers Docker e Docker Compose.

</div>

---

O Agio é um sistema web open source desenvolvido por alunos da UnB na disciplina de Métodos de Desenvolvimento de Software (2024.2). O sistema permite que empresas de pequeno e médio porte realizem a gestão de inventário de forma prática, segura e eficiente.

---

## Funcionalidades do Sistema

<div class="grid cards" markdown>

- ✅ CRUD completo de itens
- 🔐 Login e autenticação
- 📊 Dashboard de visualização
- 📁 Exportação CSV
- 👤 Controle de acesso
- 🐘 Integração PostgreSQL

</div>

---

## Arquitetura e Tecnologias

| Backend | Frontend | Banco de Dados | Infraestrutura | Deploy | Versão |
|:--|:--|:--|:--|:--|:--|
| Django 4.x + DRF | HTML5, JavaScript e CSS | PostgreSQL | Docker + Docker Compose | Vercel | 1.0.0 |

---

## Características de Qualidade Avaliadas

As características selecionadas pelo grupo foram definidas utilizando uma matriz de **Impacto x Viabilidade**, considerando a relevância de cada atributo para a experiência do usuário e para a confiabilidade do sistema.

> Mais detalhes disponíveis na [Fase 1](fase1/proposito.md).

---

## Adequação Funcional

!!! info "Completude"

    Todas as funcionalidades essenciais de CRUD, autenticação e exportação CSV estão implementadas.

!!! info "Correção"

    O dashboard reflete corretamente os dados manipulados pelo usuário.

!!! info "Adequação"

    O sistema atende às necessidades reais de gestão de inventário para PMEs.

---

## Confiabilidade

!!! success "Maturidade"

    O projeto utiliza testes automatizados e integração contínua com GitHub Actions.

!!! success "Disponibilidade"

    O sistema está publicado na Vercel com acesso contínuo.

!!! success "Tolerância a Falhas"

    O sistema responde de forma controlada a falhas de banco ou entradas inválidas.

---

## Eficiência de Desempenho

!!! warning "Comportamento Temporal"

    As operações de CRUD possuem tempos de resposta aceitáveis.

!!! warning "Utilização de Recursos"

    O consumo de CPU e memória permanece dentro dos limites esperados.

!!! warning "Capacidade"

    O sistema suporta múltiplos usuários simultâneos sem degradação significativa.

---

## Objetivos de Desenvolvimento Sustentável (ODS)

<div class="grid cards" markdown>

- :material-factory: **ODS 9 — Indústria, Inovação e Infraestrutura**
    
    ---
    
    O Agio reduz barreiras tecnológicas ao oferecer uma solução gratuita e open source para gestão de inventário.

- :material-recycle: **ODS 12 — Consumo e Produção Responsáveis**
    
    ---
    
    O sistema contribui para redução de desperdícios e melhor controle de estoque.

</div>

---

## Processo de Avaliação — ISO/IEC 25040

| Etapa | Objetivo | Status |
|:--|:--|:--:|
| [Fase 1 — Requisitos de Avaliação](fase1/escopo.md) | Definição do escopo, propósito e modelo de qualidade | 🟡 Em andamento |
| [Fase 2 — Especificação](fase2/fase2.md) | Definição das métricas e critérios de julgamento | ⚪ Pendente |
| [Fase 3 — Projeto da Avaliação](fase3/fase3.md) | Planejamento da coleta e ferramentas | ⚪ Pendente |
| [Fase 4 — Execução](fase4/fase4.md) | Coleta, análise e relatório final | ⚪ Pendente |

---

## Equipe

| Integrante | Matrícula | GitHub |
|:--|:--|:--|
| Beatriz Geane Santos Lins | 222021844 | [GitHub](https://github.com/Beatriz-Ge) |
| Eduardo Belarmino Silva | 221008580 | [GitHub](https://github.com/) |
| João Pedro Araújo de Freitas Lyra | 232003661 | [GitHub](https://github.com/Jadequilin) |
| Manoel Castro Moura Filho | 200023535 | [GitHub](https://github.com/) |
| Rivadalvio Joaquim da Silva Filho | 232024026 | [GitHub](https://github.com/RivaFilho) |

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(a) |
|:--:|:--:|:--|:--|
| 1.0 | 11/05/2026 | Criação da página inicial e estrutura inicial do projeto | Equipe Frans Bilas |
| 1.0 | 12/05/2026 | Atualização da página inicial e estruturas do projeto | Equipe Frans Bilas |

---

<div align="center">

Documentação desenvolvida para a disciplina FGA315 — Qualidade de Software.

</div>
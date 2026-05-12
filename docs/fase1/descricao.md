# 🖥️ 3. Descrição do Software Avaliado

## 3.1 Identificação do Produto

| Projeto | Versão | Origem | Licença |
|:--|:--|:--|:--|
| Agio | 1.0.0 | Projeto acadêmico MDS — UnB (2024.2) | Código aberto |

---

| Sistema | Domínio | Deploy | Repositório |
|:--|:--|:--|:--|
| Aplicação de Gestão de Inventário Otimizada | Gestão de inventário corporativo para PMEs | [Acessar Sistema](https://agio-inventory-system.vercel.app/) | [GitHub](https://github.com/unb-mds/2024-2-Agio) |

---

## 3.2 Classificação do Tipo de Produto

O Agio é classificado como um software sob medida de código aberto (*custom open-source software*), conforme as seguintes referências:

!!! abstract "Classificação do Produto"

    - Segundo **Pressman (2014)**, o Agio é um software de aplicação voltado à resolução de um problema de negócio específico, neste caso, a gestão de inventário.

    - Segundo a **IEEE 1062**, o sistema não se enquadra como COTS (*Commercial Off-The-Shelf*), pois não é um produto comercial empacotado, mas sim um sistema desenvolvido sob demanda acadêmica e distribuído com código-fonte aberto.

    - Conforme a **ISO/IEC 25010**, o produto avaliado é um sistema computacional interativo composto por frontend web, backend com API REST e banco de dados relacional.

---

## 3.3 Implicações para a Avaliação

Essa classificação impacta diretamente o processo de avaliação porque:

<div class="grid cards" markdown>

- 🔍 O código-fonte está disponível para inspeção e instrumentação direta

- 🐳 O ambiente de produção pode ser replicado localmente via Docker

- ✅ Não existem restrições de licença para execução de testes

</div>

---

## 3.4 Arquitetura e Componentes

O Agio segue uma arquitetura modular dividida em quatro camadas principais:

<div class="grid cards" markdown>

- 🎨 Frontend
- ⚙️ Backend
- 🐘 Banco de Dados
- ☁️ Infraestrutura

</div>

---

## 3.5 Diagrama de Arquitetura do Agio

mermaid
graph LR
    subgraph Usuario
        U["Navegador Web"]
    end

    subgraph Frontend
        FE["HTML5 / JS / CSS"]
    end

    subgraph Backend
        API["Django + DRF"]
        AUTH["Autenticacao JWT"]
        BL["Regras de Negocio"]
    end

    subgraph Banco de Dados
        DB["PostgreSQL"]
    end

    subgraph Infraestrutura
        DOCKER["Docker Compose"]
        VERCEL["Vercel - Deploy"]
    end

    U -->|"HTTP"| FE
    FE -->|"REST API"| API
    API --> AUTH
    API --> BL
    API -->|"SQL Queries"| DB
    DOCKER -.->|"containeriza"| API
    DOCKER -.->|"containeriza"| DB
    VERCEL -.->|"hospeda"| FE

--- 

## 3.6 Componentes Arquiteturais

| Camada         | Tecnologia                         | Função                                                  |
| :------------- | :--------------------------------- | :------------------------------------------------------ |
| Frontend       | HTML5, JavaScript e CSS            | Interface do usuário: dashboards, tabelas e formulários |
| Backend        | Django 4.x + Django REST Framework | API REST, autenticação JWT e regras de negócio          |
| Banco de Dados | PostgreSQL                         | Persistência de itens, usuários e permissões            |
| Infraestrutura | Docker + Docker Compose            | Containerização e deploy do sistema                     |

---

## 3.7 Estrutura do Sistema

O Agio é organizado em três módulos principais (*apps Django*):

| Módulo | Responsabilidade |
|:--|:--|
| `homepage` | Página inicial e navegação principal |
| `login` | Autenticação, login e controle de acesso |
| `dashboard` | Gerenciamento e visualização do inventário |

---

Cada módulo segue a estrutura padrão do framework Django, contendo:

<div class="grid cards" markdown>

- 🧩 **Models**  
  Estrutura e persistência de dados

- 👁️ **Views**  
  Regras de exibição e controle das requisições

- 🧪 **Tests**  
  Testes automatizados do módulo

</div>

---

## Funcionalidades Implementadas

As funcionalidades identificadas no backlog e nas entregas da sprint 9 incluem:

| Funcionalidade | Descrição |
|:--|:--|
| 🔐 Controle de acesso | Criação de superusuário e autenticação |
| 👤 Login JWT | Login/logout com autenticação baseada em tokens |
| 📦 CRUD de itens | Cadastro, edição, remoção e consulta de itens |
| 📊 Dashboard | Visualização de dados do inventário |
| 📁 Exportação CSV | Geração de relatórios exportáveis |
| 🐘 PostgreSQL | Integração com banco de dados relacional |

---

## 3.8 Implicações para a Avaliação

A tabela abaixo resume os componentes que podem e os que não podem ser avaliados diretamente no contexto deste projeto.

| Componente                  | O que é possível medir                                                                     | Limitações                                            |
| :-------------------------- | :----------------------------------------------------------------------------------------- | :---------------------------------------------------- |
| Backend (Django + DRF)      | Tempo de resposta dos endpoints, erros HTTP, comportamento sob carga e cobertura de testes | Não há acesso a dados corporativos reais de produção  |
| Frontend (HTML/JS/CSS)      | Tempo de carregamento e renderização do dashboard                                          | Não é possível medir experiência subjetiva do usuário |
| Banco de Dados (PostgreSQL) | Tempo de consultas e crescimento de registros                                              | Os testes utilizarão dados sintéticos                 |
| Testes automatizados        | Cobertura e taxa de sucesso                                                                | A qualidade dos cenários está fora do escopo          |
| Deploy (Vercel)             | Disponibilidade da aplicação publicada                                                     | Infraestrutura da Vercel não é controlada pela equipe |

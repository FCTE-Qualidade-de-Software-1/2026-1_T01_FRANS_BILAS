# 2. Recursos e Ambiente de Avaliação

Esta seção descreve os recursos humanos e a infraestrutura de hardware e software necessários para garantir a correta execução, repetibilidade e auditoria das medições de qualidade.

---

## 2.1 Recursos Humanos

Abaixo estão mapeados os membros da equipe e suas respectivas atribuições operacionais e de consolidação durante o ciclo de avaliação:

| Membro | Responsabilidade na Avaliação |
| :--- | :--- |
| **João Pedro Araújo** | Execução das métricas **M1**, **M2** e **M3** (*Adequação Funcional*) e consolidação dos resultados funcionais. |
| **Rivadalvio Joaquim** | Execução das métricas **M7**, **M8** e **M9** (*Eficiência de Desempenho*) e desenvolvimento dos scripts de carga. |
| **Eduardo Belarmino** | Execução das métricas **M4**, **M5** e **M6** (*Confiabilidade*) e documentação das evidências de testes. |
| **Beatriz Geane** | Organização do ecossistema do GitHub Pages, geração de gráficos e refinamento das visualizações dos resultados. |
| **Manoel Castro** | Apoio geral na coleta de dados e validação cruzada. |

---

## 2.2 Ambiente de Hardware

Para mitigar variações espúrias nos testes de desempenho local, estabeleceu-se a seguinte configuração mínima para a máquina de testes:

| Recurso | Especificação Técnica Mínima |
| :--- | :--- |
| **Máquina de Teste** | Notebook ou Desktop com no mínimo 8GB de memória RAM, processador multi-core (mínimo 4 núcleos) e armazenamento em SSD. |
| **Sistema Operacional** | Windows 10/11 configurado com Docker Desktop **ou** distribuições Linux homologadas com Docker Engine nativo. |
| **Conectividade** | Conexão banda larga estável com a internet para comunicação com o deploy na Vercel e o repositório oficial no GitHub. |

---

## 2.3 Ambiente de Software

As ferramentas utilizadas foram selecionadas para garantir a automação do processo e a precisão na coleta dos indicadores quantitativos:

| Ferramenta | Versão | Finalidade Principal | Métrica(s) Relacionada(s) |
| :--- | :---: | :--- | :---: |
| **Docker / Compose** | >= 24.x | Conteinerização e isolamento do ambiente Agio (Django + PostgreSQL). | Todas |
| **Python** | >= 3.10 | Interpretador base para scripts de automação, chamadas de testes e geração de massa sintética. | M2, M5, M7, M8, M9 |
| **Postman** | >= 11.x | Execução e automação de requisições manuais, validação de regras e testes de estresse de API. | M1, M2, M3, M6 |
| **Locust** | >= 2.x | Framework para simulação e geração de carga com múltiplos usuários simultâneos em tempo real. | M5, M8 |
| **coverage.py** | >= 7.x | Instrumentação e medição da cobertura de código das suítes de testes automatizados backend. | M4 |
| **pytest-django** | (bundled no projeto) | Framework de testes embutido no projeto para execução da suíte de testes existente. | M2, M4 |
| **Git / GitHub** | — | Controle de versão, armazenamento de logs brutos, artefatos e versionamento das evidências. | Todas |

---

## 2.4 Massa de Dados

Para as métricas de **Eficiência de Desempenho (M7, M8 e M9)**, será utilizada uma massa de dados sintéticos gerada por um script customizado em Python através da biblioteca `Faker`. Os registros simulados seguirão estritamente o modelo de dados da entidade de itens do Agio:

| Campo do Modelo | Tipo de Dado | Estratégia de Geração Sintética |
| :--- | :---: | :--- |
| **nome** | `string` | `faker.commerce.product_name()` gerando nomes textuais de produtos. |
| **descrição** | `string` | Texto de descrição aleatório contendo entre 50 e 200 caracteres. |
| **quantidade** | `integer` | Valor numérico inteiro gerado aleatoriamente no intervalo de 1 a 1000. |
| **preço** | `decimal` | Valor decimal de ponto flutuante flutuando aleatoriamente entre 0.01 e 9999.99. |

Patamares de volume: 100, 1.000, 5.000 e 10.000 itens.
A massa de dados será armazenada no repositorio Git em formato CSV para auditória (conforme premissa do projeto).

---

## 2.5 Pré-requisitos para Execução

Antes de iniciar a Fase 4, o avaliador deve:

1. Clonar o repositório do Agio: `git clone https://github.com/unb-mds/2024-2-Agio.git`
2. Executar `docker-compose up --build` e verificar que o sistema está operacional.
3. Criar superusuario: `docker exec -it <container> python manage.py createsuperuser`
4. Instalar dependências de teste: `pip install locust coverage requests faker`
5. Confirmar acesso ao deploy no Vercel: `https://agio-inventory-system.vercel.app/`

# 2. Recursos e Ambiente de Avaliacao

## 2.1 Recursos Humanos

| Membro | Responsabilidade na Fase 4 |
|---|---|
| Joao Pedro Araujo | Execucao das metricas M1, M2, M3 (Adequacao Funcional); consolidacao dos resultados |
| Rivadalvio Joaquim | Execucao das metricas M7, M8, M9 (Eficiencia de Desempenho); scripts de carga |
| Eduardo Belarmino | Execucao das metricas M4, M5, M6 (Confiabilidade); documentacao de evidencias |
| Beatriz Geane | Organizacao do GitPages; graficos e visualizacoes dos resultados |
| Manoel Castro | Apoio na coleta de dados e participacao nas reunioes |

---

## 2.2 Ambiente de Hardware

| Recurso | Especificacao |
|---|---|
| Maquina de teste | Notebook com minimo 8GB RAM, processador multi-core, SSD |
| Sistema operacional | Windows 10/11 com Docker Desktop ou Linux com Docker Engine |
| Conectividade | Internet para acesso ao deploy na Vercel e ao repositorio GitHub |

---

## 2.3 Ambiente de Software

| Ferramenta | Versao | Finalidade | Metrica(s) |
|---|---|---|---|
| Docker Desktop | >= 24.x | Containerizacao do ambiente Agio (Django + PostgreSQL) | Todas |
| Python | >= 3.10 | Scripts de automacao, testes, geracao de dados sinteticos | M2, M5, M7, M8, M9 |
| Postman | >= 11.x | Execucao de requisicoes manuais e testes de API | M1, M2, M3, M6 |
| Locust | >= 2.x | Teste de carga com multiplos usuarios simultaneos | M5, M8 |
| coverage.py | >= 7.x | Medicao de cobertura de codigo dos testes automatizados | M4 |
| pytest-django | (bundled no projeto) | Execucao dos testes automatizados existentes | M2, M4 |
| Git / GitHub | - | Versionamento e armazenamento de evidencias e dados brutos | Todas |

---

## 2.4 Massa de Dados

Para as metricas de Eficiencia de Desempenho (M7, M8, M9), sera utilizada massa de dados sinteticos gerada por script Python. Os dados seguem o modelo de item do Agio:

| Campo | Tipo | Geracao |
|---|---|---|
| nome | string | `faker.commerce.product_name()` ou nomes aleatorios |
| descricao | string | Texto aleatorio de 50-200 caracteres |
| quantidade | inteiro | Aleatorio entre 1 e 1000 |
| preco | decimal | Aleatorio entre 0.01 e 9999.99 |

Patamares de volume: 100, 1.000, 5.000 e 10.000 itens.

A massa de dados sera armazenada no repositorio Git em formato CSV para auditoria (conforme premissa do projeto).

---

## 2.5 Pre-requisitos para Execucao

Antes de iniciar a Fase 4, o avaliador deve:

1. Clonar o repositorio do Agio: `git clone https://github.com/unb-mds/2024-2-Agio.git`
2. Executar `docker-compose up --build` e verificar que o sistema esta operacional.
3. Criar superusuario: `docker exec -it <container> python manage.py createsuperuser`
4. Instalar dependencias de teste: `pip install locust coverage requests faker`
5. Confirmar acesso ao deploy na Vercel: `https://agio-inventory-system.vercel.app/`

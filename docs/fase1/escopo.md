# 🎯 6. Escopo, Profundidade e Objetos de Avaliação

## 6.1 Dentro do Escopo

Os componentes abaixo serão diretamente avaliados durante o processo definido pela ISO/IEC 25040.

| Objeto de Avaliação | Profundidade da Avaliação | Justificativa |
|:--|:--|:--|
| Backend — Endpoints da API REST | Testes funcionais, testes de carga e tolerância a falhas | Núcleo operacional do sistema e principal responsável pela lógica de negócio |
| Banco de Dados — PostgreSQL | Medição de tempo de resposta e comportamento sob crescimento de dados | Impacta diretamente o desempenho geral da aplicação |
| Testes automatizados existentes | Análise de cobertura e taxa de sucesso | Evidência direta de maturidade e confiabilidade |
| Deploy publicado na Vercel | Verificação de disponibilidade e tempo de resposta externo | Representa o ambiente real de utilização do sistema |

---

<div class="grid cards" markdown>

- 🧩 **API REST**
  
  CRUD, autenticação e exportação de dados

- 🐘 **Banco PostgreSQL**
  
  Consultas e persistência de dados

- ✅ **Testes Automatizados**
  
  Cobertura e estabilidade do sistema

- 🌐 **Deploy em Produção**
  
  Disponibilidade e acesso externo

</div>

---

## 6.2 Fora do Escopo

Os itens abaixo não serão avaliados nesta fase do projeto.

| Item Excluído | Justificativa |
|:--|:--|
| Frontend — UX e Usabilidade | Demandaria testes com usuários reais |
| Código-fonte — Manutenibilidade | Característica não selecionada |
| Segurança — Pentesting e vulnerabilidades | Exige metodologia especializada |
| Dados reais de empresas | Não há acesso a bases reais |
| Integrações externas (SSO/BI) | Não implementadas na versão analisada |
| Aplicativo mobile/desktop | Apenas a versão web será considerada |

---

!!! warning "Limitações do Escopo"

    A avaliação concentra-se exclusivamente nas características
    selecionadas pela equipe e definidas no modelo de qualidade.

    Aspectos como segurança, experiência do usuário e manutenção
    do código-fonte não fazem parte desta análise.

---

## 6.3 Limites de Validade dos Resultados

Os resultados obtidos serão considerados válidos apenas dentro das seguintes condições experimentais.

<div class="grid cards" markdown>

- 📦 **Versão Avaliada**
  
  Release `1.0.0` do repositório oficial do Agio

- 🧪 **Dados Sintéticos**
  
  Dados artificiais serão utilizados nos testes de desempenho

- 🐳 **Ambiente Local**
  
  Execução via Docker Compose em ambiente controlado

- 👥 **Carga Simulada**
  
  Até 50 usuários simultâneos e 10.000 itens cadastrados

</div>

---

!!! note "Importante"

    Resultados obtidos em ambiente acadêmico podem divergir
    do comportamento observado em produção real,
    especialmente sob cargas superiores ou uso corporativo contínuo.

---

## 6.4 Plano de Cobertura Progressiva

A avaliação será conduzida de forma incremental ao longo das quatro fases definidas pela ISO/IEC 25040.

| Fase | Cobertura Prevista |
|:--|:--|
| **Fase 1** | Definição do escopo, características e objetos de avaliação |
| **Fase 2** | Definição das métricas, modelo GQM e critérios de julgamento |
| **Fase 3** | Planejamento de coleta, ferramentas e cronograma |
| **Fase 4** | Execução das medições e análise dos resultados |

---
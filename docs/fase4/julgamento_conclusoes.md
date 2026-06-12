# 3. Julgamento, Conclusões e Sugestões de Melhoria

## 3.1 Julgamento Final da Qualidade

### Coerência com o Propósito da Avaliação (Fase 1)

Conforme definido no planejamento inicial, esta avaliação buscou responder a três questões essenciais de decisão para o negócio e para a engenharia do projeto:

| Questão de Decisão (Fase 1) | Resultado Consolidado | Julgamento Técnico e Prático |
| :--- | :---: | :--- |
| **As funcionalidades atendem ao backlog?** | `ICF = 100%`<br>`TCF = 90%`<br>`IAT = 83,3%` | **Viável para uso básico.** O sistema cobre a totalidade das funcionalidades planejadas, entregando o comportamento correto na grande maioria dos cenários de teste. Apresenta ressalvas apenas no fluxo de autenticação via API externa. |
| **O sistema é estável para produção?** | `TMCT = 0%`<br>`TDO = 100%`<br>`ITF = 80%` | 🔴 **Não está pronto para produção.** Embora a disponibilidade seja excelente (100%) e a tolerância a falhas provocadas seja boa (80%), a ausência total de testes automatizados impõe um risco crítico de regressão. O sistema também carece de validações matemáticas essenciais (aceita preços negativos). |
| **O desempenho é aceitável para PMEs?** | `TMRE = 2,3ms`<br>`DDVD = 5.253%` | **Adequado apenas para microvolumes.** A velocidade de resposta é excelente para bases pequenas (até 1.000 itens cadastrados). Contudo, a performance degrada criticamente a partir daí devido à falta de paginação, limitando o uso para inventários muito reduzidos. |

---

## 3.2 Resumo por Característica

A tabela abaixo sintetiza o veredicto de qualidade para cada uma das macrocaracterísticas da ISO/IEC 25010 avaliadas no sistema Agio v1.0.0:

| Característica de Qualidade | Nível Geral | Justificativa Técnica |
| :--- | :---: | :--- |
| 🎯 **Adequação Funcional** | 🔵 **Bom** | Completude excelente (`100%`), taxa de correção robusta (`90%`) e boa adequação à tarefa diária (`83,3%`). O único ponto crítico de atenção é a falha (HTTP 500) no login via rota direta de API. |
| 🛡️ **Confiabilidade** | 🔴 **Insuficiente** | Apesar da excelente estabilidade e disponibilidade em tempo de execução (`TDO = 100%`), a falta absoluta de testes automatizados escritos (`TMCT = 0%`) compromete severamente a maturidade do software. O sistema também permite falhas de consistência lógica ao aceitar preços negativos. |
| ⚡ **Eficiência de Desempenho** | 🟡 **Regular** | Os tempos de resposta em cenários isolados são excepcionais (`TMRE = 2,3ms`), mas a taxa de degradação volumétrica é alarmante (`DDVD = 5.253%`). O sistema não possui escalabilidade arquitetural sem uma reestruturação de rotas. |

---

## 3.3 Sugestões de Melhoria e Plano de Ação

Para elevar o nível de maturidade do sistema Agio e viabilizar sua implantação segura em ambientes corporativos, propõe-se o seguinte plano de correções priorizado:

| Prioridade | Ação Corretiva Recomendada | Métrica Alvo | Impacto Técnico Esperado |
| :---: | :--- | :---: | :--- |
| 🔴 **Alta** | Implementar paginação no endpoint de listagem e exportação de CSV. Substituir chamadas irrestritas do tipo `ProductTable.objects.all()` pela utilização de `.paginate()` ou da classe `Paginator` nativa do Django. | **M9**<br>*(DDVD)* | Reduzir a taxa de degradação volumétrica de 5.253% para menos de 50%, viabilizando o suporte a inventários de grande porte (10.000+ itens). |
| 🔴 **Alta** | Construir uma suíte base de testes automatizados (unitários e de integração), cobrindo no mínimo as operações de CRUD, fluxos de autenticação e geração de arquivos CSV. | **M4**<br>*(TMCT)* | Mitigar riscos de regressão no código, elevando o indicador de zero para pelo menos 80% de *pass rate* com mais de 50% de cobertura real de linhas. |
| 🔴 **Alta** | Adicionar validação de consistência monetária na camada de *Serializer* do Django REST Framework: impedir a gravação de registros caso o campo `price` seja $< 0$. | **M6**<br>*(ITF)* | Proteger a integridade lógica e fiscal do banco de dados, elevando o Índice de Tolerância a Falhas para mais de 87%. |
| 🟡 **Média** | Corrigir o tratamento de exceção na rota de login (`POST`), sanando o estouro de erro interno (HTTP 500) para responder corretamente payloads em formato JSON. | **M3**<br>*(IAT)* | Garantir o desacoplamento do backend e estabilizar a Taxa de Adequação à Tarefa em 100%. |
| 🟡 **Média** | Configurar os campos `category` e `description` como explicitamente obrigatórios no *Serializer*, ou atualizar a documentação do sistema informando que são metadados opcionais. | **M6**<br>*(ITF)* | Alinhar a expectativa de preenchimento do usuário com as regras internas de tratamento de dados do sistema. |
| 🟢 **Baixa** | Adotar e padronizar o uso de tokens JWT nativos para a proteção de todos os endpoints expostos pela API REST, substituindo o modelo atual dependente de sessões web do Django. | **M6**<br>*(ITF)* | Elevar o patamar de segurança da arquitetura e alinhar o projeto às melhores práticas de desenvolvimento de APIs. |

---

## 3.4 Verificação das Hipóteses

| Código | Hipótese Formulada na Fase 2 | Indicador Vinculado | Status da Hipótese |
| :---: | :--- | :---: | :---: |
| **H1** | Espera-se completude do backlog acima de 75% devido às 9 sprints. | `ICF = 100%` | 🟢 **Confirmada e Superada** |
| **H2** | Taxa de correção acima de 80% para operações básicas de CRUD. | `TCF = 90%` | 🟢 **Confirmada** |
| **H3** | Fluxos de trabalho básicos de inventário cobertos. | `IAT = 83,3%` | 🟢 **Confirmada** |
| **H4** | *Pass rate* de testes acima de 80%, mas volumetria e cobertura baixas. | `TMCT = 0%` | 🔴 **Refutada** *(Não há testes escritos)* |
| **H5** | Taxa de disponibilidade em ambiente local superior a 99%. | `TDO = 100%` | 🟢 **Confirmada e Superada** |
| **H6** | Presença de erros HTTP 500 em cenários de entradas inválidas. | `ITF = 80%` | 🟡 **Parcialmente Confirmada** *(Apenas a rota de login falhou)* |
| **H7** | Tempo médio de resposta mantido abaixo de 1.000 ms sob uso normal. | `TMRE = 2,3ms` | 🟢 **Confirmada com Margem** |
| **H8** | Consumo de CPU mantido abaixo do teto limite de 70%. | `URC (CPU) = 0%` | 🟢 **Confirmada com Margem** |
| **H9** | Degradação de performance superior a 50% diante de bases volumosas. | `DDVD = 5.253%` | 🟢 **Confirmada** *(Impacto acima do esperado)* |

---

## 3.5 Conclusão Geral

O sistema Agio v1.0.0 apresenta um perfil de qualidade característico de projetos acadêmicos em estágio inicial de maturidade: **excelente cobertura de escopo funcional, mas com lacunas severas de engenharia nas camadas de confiabilidade, segurança e escalabilidade**.

A alta taxa de completude (`100%`) comprova que o ciclo de 9 sprints foi altamente eficaz em transformar requisitos de negócio em código disponível. O sistema entrega uma experiência ágil, leve e responsiva para usuários que operam com pequenos volumes de estoque. 

Contudo, a ausência de uma suíte de testes automatizados e o crescimento linear e agressivo do tempo de processamento em consultas volumosas impedem a classificação do software como uma solução pronta para ambientes de produção estáveis.

---

## 3.6 Recomendação Final de Engenharia

!!! info "Perfil de Adoção Recomendado"

    O Agio v1.0.0 é considerado **apto e recomendado** para adoção imediata em micro e pequenas empresas cujo volume total de inventário não ultrapasse o limite de **500 itens cadastrados**.

    Recomenda-se, preferencialmente, a utilização do sistema por meio da interface web tradicional.

!!! warning "Restrição de Implantação"

    **Não é recomendada** a implantação do sistema em ambientes corporativos ou organizações de médio porte sem a implementação prévia das melhorias classificadas como **Alta Prioridade**, descritas na seção 3.3.

    Entre essas melhorias, destacam-se:

    - implementação de paginação;
    - validação adequada de *payloads*.

    A ausência desses mecanismos expõe a organização a riscos de inconsistência financeira no estoque e possíveis indisponibilidades do servidor decorrentes do esgotamento de recursos computacionais.

# Intelligent Insights para monitorar e solucionar problemas de desempenho do banco de dados (preview)

- Artigo
- 16/08/2024
- 9 colaboradores

Comentários

Neste artigo[O que o recurso Insights inteligentes pode fazer por você?](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-overview?view=azuresql#what-can-intelligent-insights-do-for-you)[Como o Intelligent Insights funciona?](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-overview?view=azuresql#how-does-intelligent-insights-work)[Opções do Intelligent Insights](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-overview?view=azuresql#intelligent-insights-options)[Configurar a exportação do log do Intelligent Insights](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-overview?view=azuresql#configure-the-export-of-the-intelligent-insights-log)Mostrar mais 6

**Aplica-se a:** ![img](https://learn.microsoft.com/pt-br/azure/azure-sql/media/applies-to/yes-icon.svg?view=azuresql)[Banco de Dados SQL do Azure](https://learn.microsoft.com/pt-br/sql/sql-server/sql-docs-navigation-guide#applies-to) ![img](https://learn.microsoft.com/pt-br/azure/azure-sql/media/applies-to/yes-icon.svg?view=azuresql)[Instância Gerenciada de SQL do Azure](https://learn.microsoft.com/pt-br/sql/sql-server/sql-docs-navigation-guide#applies-to)

O Intelligent Insights do Banco de Dados SQL e da Instância Gerenciada de SQL do Azure permite saber o que está acontecendo com o desempenho do banco de dados.

O Intelligent Insights usa uma inteligência interna para monitorar continuamente o uso de banco de dados por meio de inteligência artificial e detecta os eventos de interrupção que causam baixo desempenho. Quando detectados, é executada uma análise detalhada que gera um log de recursos do Intelligent Insights chamado de SQLInsights [não relacionado aos [Insights de SQL do Azure Monitor (versão prévia)](https://learn.microsoft.com/pt-br/azure/azure-sql/database/monitoring-sql-database-azure-monitor?view=azuresql)] com uma [avaliação inteligente dos problemas](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-troubleshoot-performance?view=azuresql). Essa avaliação consiste em uma análise da causa raiz do problema de desempenho do banco de dados e possíveis recomendações para melhorias de desempenho.



## O que o recurso Insights inteligentes pode fazer por você?

O Intelligent Insights é uma capacidade exclusiva de inteligência interna do Azure e fornece o seguinte valor:

- Monitoramento proativo
- Insights de desempenho personalizado
- Detecção prévia de degradação de desempenho do banco de dados
- Análise da causa raiz dos problemas detectados
- Recomendações de melhoria de desempenho
- Capacidade de expansão em centenas de milhares de bancos de dados
- Impacto positivo nos recursos de DevOps e no custo total de propriedade



## Como o Intelligent Insights funciona?

O Intelligent Insights analisa o desempenho do banco de dados comparando a carga de trabalho dele na última hora com a carga de trabalho de linha de base dos últimos sete dias. A carga de trabalho do banco de dados é composta por consultas determinadas a serem mais significativas ao desempenho do banco de dados, como as consultas mais repetidas e maiores. Como cada banco de dados é exclusivo com base em sua estrutura, dados, uso e aplicativo, cada linha de base de carga de trabalho gerada é específica e exclusiva para essa carga de trabalho. O recurso Insights inteligentes, independentemente da linha de base da carga de trabalho, também monitora limites operacionais absolutos e detecta problemas com tempos de espera excessivos, exceções críticas e problemas com parametrizações de consulta que podem afetar o desempenho.

Após a detecção de um problema de degradação do desempenho de várias métricas observadas usando inteligência artificial, a análise é executada. O log de diagnóstico é gerado com um insight inteligente sobre o que está acontecendo com seu banco de dados. O Insights inteligentes facilita o acompanhamento do problema de desempenho do banco de dados, da primeira ocorrência à solução. Cada problema detectado é rastreado em todo o ciclo de vida, da detecção inicial do problema e verificação da melhora de desempenho até sua conclusão.

![Fluxo de trabalho de análise de desempenho do banco de dados](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/intelligent-insights-overview/intelligent-insights-concept.png?view=azuresql)

A métrica usada para medir e detectar problemas de desempenho do banco de dados é baseada na duração da consulta, em solicitações que atingem o tempo limite, tempos de espera excessivo e solicitações com erros. Para obter mais informações sobre métricas, consulte [Métricas de detecção](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-overview?view=azuresql#detection-metrics).

As degradações de desempenho do banco de dados identificadas são registradas no log do SQLInsights do Intelligent Insights com entradas inteligentes que consistem nas seguintes propriedades:

Expandir a tabela

| Propriedade                          | Detalhes                                                     |
| :----------------------------------- | :----------------------------------------------------------- |
| Informações de banco de dados        | Metadados sobre um banco de dados no qual foi detectado um insight, como o URI do recurso. |
| Intervalo de tempo observado         | Hora de início e término do período do insight detectado.    |
| Métricas afetadas                    | Métricas que fizeram com que uma visão mais detalhada fosse gerada:Aumento da duração da consulta [segundos].Espera excessiva [segundos].Solicitações com tempo limite [percentual].Solicitações com erro [percentual]. |
| Valor do impacto                     | Valor de uma métrica medida.                                 |
| Consultas afetadas e códigos de erro | Hash de consulta ou código de erro. Podem ser usados para correlacionar facilmente a consultas afetadas. São fornecidas métricas que consistem em aumento de duração da consulta, tempo de espera, contagens de tempo limite ou códigos de erro. |
| Detecções                            | Detecção identificada no banco de dados durante o tempo de um evento. Há 15 padrões de detecção. Para obter mais informações, consulte [Solucionar problemas de desempenho do banco de dados com o Insights inteligentes](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-troubleshoot-performance?view=azuresql). |
| Análise da causa raiz                | Análise da causa raiz do problema identificado em um formato legível por humanos. Alguns insights podem conter recomendação de melhoria de desempenho sempre que possível. |

O Intelligent Insights se destaca na detecção e na solução de problemas de desempenho do banco de dados. Para usar o Intelligent Insights ao solucionar problemas de desempenho do banco de dados, consulte [Solucionar problemas de desempenho com o Intelligent Insights](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-troubleshoot-performance?view=azuresql).



## Opções do Intelligent Insights

As opções disponíveis do Intelligent Insights são:

Expandir a tabela

| Opção do Intelligent Insights                                | Suporte para Banco de Dados SQL do Azure | Suporte às instâncias gerenciadas do Azure SQL |
| :----------------------------------------------------------- | :--------------------------------------- | :--------------------------------------------- |
| **Configurar o Intelligent Insights** - Configure a análise do Intelligent insights para seus bancos de dados. | Sim                                      | Sim                                            |
| **Transmitir informações para a Análise de SQL do Azure** -- Transmita informações para a Análise de SQL do Azure. | Sim                                      | Sim                                            |
| **Transmitir informações para os Hubs de Eventos do Azure** – Transmita informações para os Hubs de Eventos para obter outras integrações personalizadas. | Sim                                      | Sim                                            |
| **Transmitir informações para o Armazenamento do Azure** - Transmita informações para o Armazenamento do Azure para obter uma análise adicional e arquivamento de longo prazo. | Sim                                      | Sim                                            |

 Observação

O Intelligent Insights é uma versão prévia do recurso e não está disponível nas seguintes regiões: Oeste da Europa, Norte da Europa, Oeste dos EUA 1 e Leste dos EUA 1.



## Configurar a exportação do log do Intelligent Insights

A saída do Intelligent Insights pode ser transmitida para um dos vários destinos para análise:

- A saída transmitida para um espaço de trabalho da Análise de Log pode ser usada com a [Análise de SQL do Azure](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/azure-sql) para exibir informações por meio da interface do usuário do portal do Azure. Esta é a solução do Azure integrada e a maneira mais comum de exibir os insights.
- A saída transmitida para os Hubs de Eventos do Azure pode ser usada para o desenvolvimento de cenários de monitoramento e alerta personalizados
- A saída transmitida para o Armazenamento do Azure pode ser usada para desenvolvimento de aplicativos personalizados para relatórios personalizados, arquivamento de dados de longo prazo etc.

A integração da Análise de SQL do Azure, dos Hubs de Eventos do Azure, do Armazenamento do Azure ou de produtos de terceiros para consumo é feita primeiro pela habilitação dos logs do Intelligent Insights (o log do "SQLInsights") na página **Configurações de diagnóstico** de um banco de dados e pela configuração dos dados de log do Intelligent Insights para transmissão a um desses destinos.

Para obter mais informações sobre como habilitar o log do Intelligent Insights e configurar dados de log de recursos e métricas para transmissão para um produto de consumo, consulte [Log de diagnóstico e métricas](https://learn.microsoft.com/pt-br/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?view=azuresql).



### Configuração com a Análise de SQL do Azure

A solução da Análise de SQL do Azure fornece interface gráfica do usuário e recursos de relatórios e alertas sobre o desempenho do banco de dados usando os dados do log de recursos do Intelligent Insights.

Para adicionar a Análise de SQL do Azure ao painel do portal do Azure no marketplace e criar um espaço de trabalho, consulte [Configurar a Análise de SQL do Azure](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/azure-sql#configuration)

Para usar o Intelligent Insights com a Análise de SQL do Azure, configure os dados de log do Intelligent Insights para serem transmitidos para o espaço de trabalho da Análise de SQL do Azure criado em uma etapa anterior; consulte [Log de diagnósticos e métricas](https://learn.microsoft.com/pt-br/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?view=azuresql).

O exemplo a seguir mostra um Intelligent Insights exibido por meio da Análise de SQL do Azure:

![Relatório de Insights inteligentes](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/intelligent-insights-overview/intelligent-insights-azure-sql-analytics.png?view=azuresql)



### Configuração com os Hubs de Eventos

Para usar o Intelligent Insights com os Hubs de Eventos e configurar os dados de log do Intelligent Insights para serem transmitidos para Hubs de Eventos, consulte [Log de diagnósticos e métricas](https://learn.microsoft.com/pt-br/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?view=azuresql) e [Transmitir logs de diagnóstico do Azure para Hubs de Eventos](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/resource-logs#send-to-azure-event-hubs).

Para usar os Hubs de Eventos para configurar o monitoramento e alertas personalizados, consulte [O que fazer com métricas e logs de diagnóstico no Hub de Eventos](https://learn.microsoft.com/pt-br/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?view=azuresql#what-to-do-with-metrics-and-resource-logs-in-event-hubs).



### Configuração com o Armazenamento do Microsoft Azure

Para usar o Intelligent Insights com o Armazenamento e configurar os dados de log do Intelligent Insights para serem transmitidos para o Armazenamento, consulte [Log de diagnósticos e métricas](https://learn.microsoft.com/pt-br/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?view=azuresql) e [Transmitir para o Armazenamento do Azure](https://learn.microsoft.com/pt-br/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?view=azuresql#stream-into-azure-storage).



### Integrações personalizadas de log do Insights inteligentes

Para usar o Intelligent Insights com ferramentas de terceiros, ou para desenvolvimento de monitoramento e alerta personalizados, consulte [Usar o log de diagnóstico de desempenho de banco de dados do Intelligent Insights](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-use-diagnostics-log?view=azuresql).



## Métricas de detecção

Métricas usadas para modelos de detecção que geram insights inteligentes são baseadas em monitoramento:

- Duração da consulta
- Solicitações de tempo limite
- Tempo de espera excessivo
- Solicitações com erro

Solicitações de duração e tempo limite de consulta são usadas como modelos principais na detecção de problemas de desempenho de carga de trabalho de banco de dados. Elas são usadas porque medem diretamente o que está acontecendo com a carga de trabalho. Para detectar todos os casos possíveis de degradação do desempenho de carga de trabalho, tempo de espera excessivo e solicitações com erros são usados como modelos adicionais para indicar problemas que afetam o desempenho da carga de trabalho.

O sistema automaticamente considera alterações na carga de trabalho e no número de solicitações de consulta feitas ao banco de dados para determinar dinamicamente os limites normais e fora do comum de desempenho do banco de dados.

Todas as métricas são consideradas em conjunto em vários relacionamentos por meio de um modelo de dados derivado cientificamente que categoriza cada problema de desempenho detectado. As informações fornecidas por meio de um insight inteligente incluem:

- Detalhes do problema de desempenho detectado.
- Uma análise da causa raiz do problema detectado.
- Recomendações sobre como melhorar o desempenho do banco de dados monitorado, quando possível.



## Duração da consulta

O modelo de degradação da duração da consulta analisa consultas individuais e detecta o aumento no tempo necessário para compilar e executar uma consulta em comparação à linha de base de desempenho.

Se a inteligência interna detectar um aumento significativo no tempo de execução ou na compilação da consulta que afete o desempenho da carga de trabalho, essas consultas serão sinalizadas como problemas de degradação de desempenho de duração da consulta.

O log de diagnóstico do Intelligent Insights gera o hash de consulta da consulta com degradação de desempenho. O hash de consulta indica se a degradação do desempenho foi relacionada a um aumento no tempo de execução ou compilação de consulta, que aumentou o tempo de duração da consulta.



## Solicitações de tempo limite

O modelo de degradação das solicitações de tempo limite analisa consultas individuais e detecta qualquer aumento nos tempos limite no nível de execução da consulta e nos limites de solicitação geral no nível do banco de dados em comparação ao período de linha de base de desempenho.

Algumas das consultas podem atingir o tempo limite até mesmo antes de atingirem o estágio de execução. Por meio de trabalhos cancelados e solicitações feitas, a inteligência interna mede e analisa todas as consultas que chegaram ao banco de dados, tenham atingido o estágio de execução ou não.

Depois que o número de tempos limite das consultas executadas ou o número de trabalhadores com solicitação anuladas cruza o limite gerenciado do sistema, um log de diagnóstico é preenchido com insights inteligentes.

Os insights gerados contêm o número de solicitações que atingiram o tempo limite e o número de consultas que atingiram o tempo limite. A indicação da degradação de desempenho está relacionada ao aumento de tempo limite no estágio de execução ou ao nível de banco de dados geral fornecido. Quando o aumento nos tempos limite é considerado significativo para o desempenho do banco de dados, essas consultas são sinalizadas como problemas de degradação de desempenho de tempo limite.



## Tempos excessivos de espera

O modelo de tempo de espera excessivo monitora as consultas de banco de dados individuais. Ele detecta estatísticas de espera de consulta incomumente altas que cruzaram os limites absolutos gerenciado pelo sistema. São observadas as seguintes métricas de tempo de espera excessivo utilizando [Estatísticas de Espera de Repositório de Consultas (sys.query_store_wait_stats)](https://learn.microsoft.com/pt-br/sql/relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql):

- Atingindo os limites do recurso
- Atingindo os limites de recurso do pool elástico
- Número excessivo de threads de trabalho ou sessão
- Bloqueio excessivo do banco de dados
- Demanda de memória
- Outras estatísticas de espera

Atingir os limites de recurso ou os limites de recursos do pool elástico denota que o consumo de recursos disponíveis em uma assinatura ou no pool elástico cruzou limites absolutos. Essas estatísticas indicam degradação do desempenho de carga de trabalho. Um número excessivo de threads de trabalho ou sessão denota uma condição em que o número de threads de trabalho ou sessões iniciadas cruzou os limites absolutos. Essas estatísticas indicam degradação do desempenho de carga de trabalho.

Bloqueio de banco de dados excessivo indica uma condição em que a contagem de bloqueios em um banco de dados cruzou os limites absolutos. Esta estatística indica uma degradação de desempenho da carga de trabalho. A pressão de memória é uma condição em que o número de threads solicitando concessões de memória cruzou um limite absoluto. Esta estatística indica uma degradação de desempenho da carga de trabalho.

A detecção de outras estatísticas de espera indica uma condição em que métricas diversas medidas por meio das Estatísticas de Espera de Repositório de Consultas cruzaram um limite absoluto. Essas estatísticas indicam degradação do desempenho de carga de trabalho.

Depois que forem detectados tempos de espera excessivo, dependendo dos dados disponíveis, o log de diagnóstico de Insights inteligentes produz hashes das consultas afetadas e que afetam o sistema degradadas no desempenho, dos detalhes das métricas que fazem as consultas esperarem em execução e do tempo de espera medido.



## Solicitações com erros

O modelo de degradação de solicitações com erros monitora consultas individuais e detecta um aumento no número de consultas que apresentaram erros em comparação com o período da linha de base. Este modelo também monitora exceções críticas que cruzaram limites absolutos gerenciados pela inteligência interna. O sistema automaticamente considera o número de solicitações de consulta feitas ao banco de dados e considera quaisquer alterações de carga de trabalho no período monitorado.

Quando o aumento medido em solicitações com erros em relação o número total de solicitações feitas é considerado significativo para o desempenho da carga de trabalho, as consultas afetadas são sinalizadas como problemas de degradação do desempenho de solicitações com erros.

O log do Intelligent Insights gera a contagem de solicitações com erros. Indica se a degradação do desempenho estava relacionada a um aumento nas solicitações com erros ou a cruzar um limite de exceção crítico monitorado e tempo medido da degradação do desempenho.

Se qualquer uma das exceções críticas monitoradas cruzar os limites absolutos gerenciados pelo sistema, um insight inteligente será gerado com detalhes da exceção crítica.



## Próximas etapas

- Saiba como [Monitorar bancos de dados utilizando a Análise de SQL](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/azure-sql).
- Saiba como [Solucionar problemas de desempenho com o Intelligent Insights](https://learn.microsoft.com/pt-br/azure/azure-sql/database/intelligent-insights-troubleshoot-performance?view=azuresql).
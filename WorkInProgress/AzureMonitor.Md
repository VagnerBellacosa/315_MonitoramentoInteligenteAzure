# Visão geral do Azure Monitor

[Arquitetura de alto nível](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#high-level-architecture)

[Fontes de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#data-sources)

[Coleta de dados e roteamento](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#data-collection-and-routing)

[Plataforma de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#data-platform)

O Azure Monitor é uma solução de monitoramento abrangente para coletar, analisar e responder à dados de monitoramento dos ambientes de nuvem e locais. Você pode usar o Azure Monitor para maximizar a disponibilidade e o desempenho de seus aplicativos e serviços. Ele ajuda você a entender como seus aplicativos estão sendo executados e permite que você responda manual e programaticamente a eventos do sistema.

O Azure Monitor coleta e agrega os dados de cada camada e cada componente do seu sistema em vários locatários e assinaturas do Azure e fora do Azure. Ele o armazena em uma plataforma de dados comum para consumo por um conjunto comum de ferramentas que podem correlacionar, analisar, visualizar e/ou responder aos dados. Você também pode integrar outras ferramentas que são Microsoft e que não são da Microsoft.

[![Diagrama que mostra uma exibição abstrata do que o Azure Monitor faz, conforme descrito no parágrafo anterior.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/azure-monitor-high-level-abstraction-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/azure-monitor-high-level-abstraction-opt.svg#lightbox)

O diagrama acima mostra uma exibição abstrata do processo de monitoramento. Uma análise mais detalhada da arquitetura do Azure Monitor é mostrada na seção [Arquitetura de alto nível](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#high-level-architecture) abaixo.



## Arquitetura de alto nível

O Azure Monitor pode monitorar esses tipos de recursos no Azure, em outras nuvens ou localmente:

- Aplicativos
- Máquinas virtuais
- Sistemas operacionais convidados
- Contêineres incluindo métricas do Prometheus
- Bancos de dados
- Eventos de segurança em combinação com o Azure Sentinel
- Eventos de rede e integridade em combinação com Observador de Rede
- Fontes personalizadas que usam as APIs para obter dados no Azure Monitor

Também é possível exportar dados de monitoramento do Azure Monitor para outros sistemas para que você possa:

- Integrar com outras ferramentas de monitoramento e visualização de código aberto e de terceiros
- Integrar com emissão de tíquetes e outros sistemas de ITSM

Se você for um usuário do System Center Operations Manager (SCOM), o Azure Monitor agora incluirá uma versão prévia da [Instância Gerenciada SCOM (SCOM MI)](https://learn.microsoft.com/pt-br/azure/azure-monitor/vm/scom-managed-instance-overview) do Azure Monitor. A MI do Operations Manager é uma versão hospedada da nuvem do Operations Manager e permite que você mova sua instalação do Operations Manager local para o Azure.

O diagrama a seguir mostra uma exibição de arquitetura de alto nível do Azure Monitor.

[![Diagrama que mostra uma visão geral do Azure Monitor com as fontes de dados à esquerda enviando dados para uma plataforma de dados central e recursos do Azure Monitor à direita que usam os dados coletados.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/overview-simple-20230707-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/overview-blowout-20230707-opt.svg#lightbox)

Clique no diagrama para ver uma versão expandida mais detalhada mostrando uma divisão maior de fontes de dados e métodos de coleta de dados.

O diagrama ilustra os componentes do sistema do Azure Monitor:

- **[Fontes de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/data-sources)** são os tipos de recursos que estão sendo monitorados.
- Os dados são coletados e roteados para a **plataforma de dados**. Clicar no diagrama mostra essas opções, que também são destacadas em detalhes mais adiante neste artigo.
- A **[plataforma de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/data-platform)** armazena os dados de monitoramento coletados. A plataforma de dados principais do Azure Monitor tem armazenamentos para métricas, logs, rastreamentos e alterações. A MI do System Center Operations Manager usa seu próprio banco de dados hospedado na Instância Gerenciada de SQL.
- A seção **consumo** mostra os componentes que usam dados da plataforma de dados.
  - Os principais métodos de consumo do Azure Monitor incluem ferramentas para fornecer **insights**, **visualizar** e **analisar** dados. As ferramentas de visualização se baseiam nas ferramentas de análise e nos insights baseados nas ferramentas de visualização e análise.
  - Há mecanismos adicionais para ajudá-lo a **responder** aos dados de monitoramento de entrada.
- O caminho da **MI do SCOM** usa o console tradicional do Operations Manager com o qual os clientes do SCOM já estão familiarizados.
- As opções de interoperabilidade são mostradas na seção **integrar**. Nem todos os serviços se integram em todos os níveis. A MI do SCOM só se integra ao Power BI.



## Fontes de dados

O Azure Monitor pode coletar [dados de várias fontes](https://learn.microsoft.com/pt-br/azure/azure-monitor/data-sources).

O diagrama abaixo mostra uma versão expandida dos tipos de fonte de dados dos quais o Azure Monitor pode coletar dados de monitoramento.

[![Diagrama que mostra uma visão geral das fontes de dados do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/data-sources-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/data-sources-blowup-type-2-opt.svg#lightbox)

Clique no diagrama acima para ver uma versão maior do diagrama de fontes de dados no contexto.

Você pode integrar dados de monitoramento de aplicativo, infraestrutura e fonte de dados personalizada de fora do Azure, incluindo de nuvens locais e não Microsoft.

O Azure Monitor coleta esses tipos de dados:

Expandir a tabela

| Tipo de Dados                 | Descrição e subtipos                                         |
| :---------------------------- | :----------------------------------------------------------- |
| Aplicativo/cargas de trabalho | **Aplicativo** – Dados de desempenho, integridade e atividade do aplicativo.  **Cargas de trabalho** – Cargas de trabalho de IaaS, como SQL Server, Oracle ou SAP em execução em uma Máquina Virtual hospedada. |
| Infraestrutura                | **Contêiner** – dados sobre contêineres, como o [Serviço de Kubernetes do Azure](https://learn.microsoft.com/pt-br/azure/aks/intro-kubernetes), [Prometheus](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/prometheus-metrics-overview) e os aplicativos em execução dentro de contêineres.  **Sistema operacional** – dados sobre o sistema operacional convidado no qual o seu aplicativo é executado. |
| Plataforma Azure              | **Recurso do Azure** – dados sobre a operação de um recurso do Azure de dentro do recurso, incluindo alterações. Os Logs de Recursos são um exemplo.  **Assinatura do Azure** – a operação e o gerenciamento de uma assinatura do Azure e dados sobre a integridade e a operação do próprio Azure. O log de atividades é um exemplo.  **Locatário do Azure** - Dados sobre a operação de serviços do Azure no nível do locatário, como o Microsoft Entra ID. |
| Origens Personalizadas        | Dados que entram no sistema usando o – API REST do Azure Monitor – API de Coleta de Dados |

Para obter informações detalhadas sobre cada uma das fontes de dados, confira [fontes de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/data-sources).

A MI do SCOM (como o SCOM local) coleta apenas fontes de carga de trabalho de IaaS e sistema operacional.



## Coleta de dados e roteamento

O Azure Monitor coleta e roteia dados de monitoramento usando alguns mecanismos diferentes, dependendo dos dados que estão sendo roteados e do destino. Assim como um sistema rodoviário melhorou ao longo dos anos, nem todas as estradas levam a todos os locais. Algumas são herdadas, algumas novas e algumas são melhores de se tomar do que outras, considerando como o Azure Monitor evoluiu ao longo do tempo. Para obter mais informações, confira **[fontes de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/data-sources)**.

[![Diagrama que mostra uma visão geral da coleta e roteamento de dados do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/data-collection-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/data-collection-blowup-type-2-opt.svg#lightbox)

Clique no diagrama para ver uma versão maior da coleta de dados no contexto.

Expandir a tabela

| Método de coleta                                             | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Instrumentação de aplicativos](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-insights-overview) | O Application Insights é habilitado por meio da [Instrumentação Automática (agente)](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/codeless-overview) ou da adição do SDK do Application Insights ao código do aplicativo. Além disso, o Application Insights está em processo de implementação da [Telemetria Aberta](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/opentelemetry-overview). Para obter mais informações, consulte [Como fazer para instrumentar um aplicativo?](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-insights-overview#how-do-i-instrument-an-application). |
| [Agentes](https://learn.microsoft.com/pt-br/azure/azure-monitor/agents/agents-overview) | Os agentes podem coletar dados de monitoramento de aplicativos do sistema operacional convidado do Azure e de máquinas virtuais híbridas. |
| [Regras de coleta de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/data-collection-rule-overview) | Use regras de coleta de dados para especificar quais dados devem ser coletados, como transformá-los e para onde enviá-los. |
| Configuração zero                                            | Os dados são enviados automaticamente para um destino sem a configuração do usuário. As métricas de plataforma são o exemplo mais comum. |
| [Configurações de Diagnóstico](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/diagnostic-settings) | Use as configurações de diagnóstico para determinar para onde enviar dados de log de atividades e de log de recursos na plataforma de dados. |
| [API REST do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/logs-ingestion-api-overview) | A API de Ingestão de Logs no Azure Monitor permite enviar dados para um workspace do Log Analytics nos Logs do Azure Monitor. Você também pode enviar métricas para o repositório de Métricas do Azure Monitor usando a API de métricas personalizadas. |

Uma maneira comum de rotear dados de monitoramento para outras ferramentas que não são da Microsoft é usar *hubs de eventos*. Veja mais na seção [Integrar](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#integrate) abaixo.

A MI do SCOM (como o SCOM local) usa um agente para coletar dados, que ele envia para um servidor de gerenciamento em execução em uma MI do SCOM no Azure.

Para obter informações detalhadas sobre a coleta de dados, confira [coleta de dados](https://learn.microsoft.com/pt-br/azure/azure-monitor/best-practices-data-collection).



## Plataforma de dados

O Azure Monitor armazena dados em armazenamentos de dados para cada um dos três pilares de observabilidade, além de um adicional:

- Métricas
- logs
- rastreamentos distribuídos
- alterações

Cada repositório é otimizado para tipos específicos de cenários de dados e de monitoramento.

[![Diagrama que mostra uma visão geral da plataforma de dados do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/data-platform-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/data-platform-blowup-type-2-opt.svg#lightbox)

Selecione o diagrama anterior para ver a Plataforma de Dados no contexto de todo o Azure Monitor.

Expandir a tabela

| Pilar da observabilidade/ Armazenamento de dados             | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Métricas do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/data-platform-metrics) | As métricas são valores numéricos que descrevem um aspecto de um sistema em um ponto específico no tempo. As [Métricas do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/data-platform-metrics) são um banco de dados de série temporal otimizado para analisar dados com carimbo de data/hora. O Azure Monitor coleta métricas em intervalos regulares. As métricas são identificadas com um carimbo de data/hora, um nome, um valor e um ou mais rótulos de definição. Elas podem ser agregadas por meio de algoritmos, comparadas com outras métricas e analisadas quanto às tendências ao longo do tempo. Dão suporte a métricas nativas do Azure Monitor e [métricas do Prometheus](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/prometheus-metrics-overview). |
| [Logs do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/data-platform-logs) | Os logs são eventos registrados do sistema. Os logs podem conter diferentes tipos de dados, ser estruturados ou texto de forma livre e contêm um carimbo de data/hora. O Azure Monitor armazena dados de log estruturados e não estruturados de todos os tipos nos [Logs do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/data-platform-logs). Você pode rotear dados para [workspaces do Log Analytics](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/log-analytics-overview) para fins de consulta e análise. |
| Rastreamentos                                                | O [rastreamento distribuído](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/distributed-tracing) permite que você veja o caminho de uma solicitação à medida que ela percorre diferentes serviços e componentes. O Azure Monitor obtém dados de rastreamento distribuídos dos [aplicativos instrumentados](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-insights-overview#how-do-i-instrument-an-application). Os dados de rastreamento são armazenados em um workspace separado nos Logs do Azure Monitor. |
| Alterações                                                   | As alterações são uma série de eventos no seu aplicativo e recursos. Elas são rastreadas e armazenadas quando você usa o serviço [Análise de alterações](https://learn.microsoft.com/pt-br/azure/azure-monitor/change/change-analysis), que usa o [Azure Resource Graph](https://learn.microsoft.com/pt-br/azure/governance/resource-graph/overview) como repositório. A Análise de Alterações ajuda você a entender quais alterações, como a implantação de código atualizado, podem ter causado problemas nos sistemas. |

O rastreamento distribuído é uma técnica usada para rastrear solicitações enquanto elas viajam por um sistema distribuído. Ele permite que você veja o caminho de uma solicitação à medida que ela percorre diferentes serviços e componentes. Ele ajuda você a identificar gargalos de desempenho e solucionar problemas em um sistema distribuído.

Para um arquivamento de longo prazo menos caro dos dados de monitoramento para fins de auditoria ou conformidade, você pode exportar para o [Armazenamento do Microsoft Azure](https://learn.microsoft.com/pt-br/azure/storage/).

A MI do SCOM é semelhante ao SCOM local. Ele armazena suas informações em um Banco de Dados SQL, mas usa a Instância Gerenciada de SQL porque está no Azure.



## Consumo

As seções a seguir descrevem métodos e serviços que consomem dados de monitoramento da plataforma de dados do Azure Monitor.

Todas as áreas na seção de *consumo* do diagrama têm uma interface do usuário que aparece no portal do Azure.

A parte superior da seção de consumo se aplica somente ao núcleo do Azure Monitor. A MI do SCOM usa o Console de Operações tradicional em execução na nuvem. Ele também pode enviar dados de monitoramento para o Power BI para visualização.



### O Portal do Azure

O portal do Azure é um console unificado baseado na Web que fornece uma alternativa para as ferramentas de linha de comando. Com o portal do Azure, você pode gerenciar sua assinatura do Azure usando uma interface gráfica do usuário. Você pode criar, gerenciar e monitorar tudo, desde aplicativos Web simples a implantações em nuvem complexas no portal. A seção *Monitoramento* do portal do Azure fornece uma interface visual que dá acesso aos dados coletados para recursos do Azure e uma maneira fácil de acessar as ferramentas, os insights e as visualizações no Azure Monitor.

[![Captura de tela que mostra a seção Monitor do portal do Azure.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/azure-portal.png)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/azure-portal.png#lightbox)



### Insights

Alguns provedores de recursos do Azure têm visualizações coletadas que fornecem uma experiência de monitoramento personalizada e exigem configuração mínima. Os insights são visualizações grandes, escalonáveis e coletadas.

[![Diagrama que mostra a parte insights da seção Consumo do sistema do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/insights-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/insights-blowup-type-2-opt.svg#lightbox)

A tabela a seguir descreve alguns dos maiores insights:

Expandir a tabela

| Insight                                                      | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Application Insights](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-insights-overview) | O Application Insights monitora a disponibilidade, o desempenho e o uso de seus aplicativos Web. |
| [Insights do contêiner](https://learn.microsoft.com/pt-br/azure/azure-monitor/containers/container-insights-overview) | Os Insights do Contêiner oferecem visibilidade de desempenho nas cargas de trabalho de contêiner implantadas em clusters do Kubernetes gerenciado hospedados no Serviço de Kubernetes do Azure. Os Insights do Contêiner coletam logs e métricas de contêineres de controladores, nós e contêineres disponíveis no Kubernetes por meio da API de Métricas. Após habilitar o monitoramento a partir de clusters do Kubernetes, essas métricas e logs serão coletados automaticamente para você por meio de uma versão em contêiner do agente do Log Analytics para Linux. |
| [Insights da VM](https://learn.microsoft.com/pt-br/azure/azure-monitor/vm/vminsights-overview) | Os insights da VM monitoram as VMs do Azure. Ele analisa o desempenho e a integridade de suas VMs do Windows e Linux e identifica os diferentes processos delas e as dependências de processos externos interconectadas. A solução inclui suporte para monitorar o desempenho e as dependências de aplicativos nas VMs hospedadas localmente ou em outro provedor de nuvem. |
| [Insights de rede](https://learn.microsoft.com/pt-br/azure/network-watcher/network-insights-overview) | O Network Insights fornece, por meio de topologias, uma representação visual abrangente da integridade e das métricas de todos os recursos de rede implementados, sem exigir nenhuma configuração. Ele também fornece acesso a recursos de monitoramento de rede, como o Monitor da Conexão, o log de fluxo de grupos de segurança de rede (NSGs), a Análise de Tráfego e outros recursos de diagnóstico. |

Para obter mais informações, confira a [lista de insights e visualizações coletadas na visão geral do Insights do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/insights-overview).



### Visualizar

[![Diagrama que mostra a parte Visualizar da seção Consumo do sistema do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/visualize-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/visualize-blowup-type-2-opt.svg#lightbox)

As Visualizações, como tabelas e gráficos, são ferramentas eficientes para resumir dados de monitoramento e apresentá-los para públicos diferentes. O Azure Monitor tem recursos próprios para visualizar os dados de monitoramento e usa outros serviços do Azure para disponibilizá-los para diferentes públicos-alvo. O Power BI e o Grafana não fazem parte oficialmente do produto Azure Monitor, mas são uma integração principal e fazem parte da história do Azure Monitor.

Expandir a tabela

| Visualização                                                 | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Dashboards](https://learn.microsoft.com/pt-br/azure/azure-monitor/visualize/tutorial-logs-dashboards) | Os painéis do Azure permitem combinar diferentes tipos de dados em um painel no portal do Azure. Você pode compartilhar o painel com outros usuários do Azure. Você pode adicionar a saída de qualquer consulta de log ou gráfico de métricas a um painel do Azure. Por exemplo, é possível criar um painel que combine blocos que mostrem um gráfico de métricas, uma tabela de logs de atividades, um gráfico de uso do Application Insights e a saída de uma consulta de log. |
| [Pastas de trabalho](https://learn.microsoft.com/pt-br/azure/azure-monitor/visualize/workbooks-overview) | As pastas de trabalho oferecem uma tela flexível para análise de dados e a criação de relatórios visuais avançados no portal do Azure. Você pode usá-la para consultar dados de várias fontes de dados. As Pastas de Trabalho podem combinar e correlacionar dados de vários conjuntos de dados em uma visualização, proporcionando uma representação visual fácil do sistema. As Pastas de Trabalho são interativas e podem ser compartilhadas entre as equipes com a atualização de dados em tempo real. Use as pastas de trabalho fornecidas com os Insights, utilize a biblioteca de modelos ou crie suas próprias. |
| [Power BI](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/log-powerbi) | O Power BI é um serviço de análise de negócios que fornece visualizações interativas em várias fontes de dados. É um meio eficaz de disponibilizar dados para outras pessoas dentro e fora da sua organização. Você pode configurar o Power BI para importar dados de log automaticamente do Azure Monitor a fim de aproveitar essas visualizações. |
| [Grafana](https://learn.microsoft.com/pt-br/azure/azure-monitor/visualize/grafana-plugin) | Grafana é uma plataforma aberta que se destaca em painéis operacionais. Todas as versões do Grafana incluem o plug-in de fonte de dados do Azure Monitor para visualizar suas métricas e logs do Azure Monitor. O Grafana gerenciado do Azure também otimiza essa experiência para armazenamentos de dados nativos do Azure, como o Azure Monitor e o Azure Data Explorer. Dessa forma, você pode se conectar facilmente a todo recurso em sua assinatura e exibir todos os dados de monitoramento resultantes em um painel conhecido do Grafana. Ele também dá suporte à fixação de gráficos de métricas e logs do Azure Monitor em painéis do Grafana.  O Grafana tem plug-ins populares e modelos de painel para ferramentas do APM não Microsoft como o Dynatrace, o New Relic e o AppDynamics. Você pode usar esses recursos para visualizar dados da plataforma do Azure junto a outras métricas de alto nível na pilha coletada por essas outras ferramentas. Elas também contam com os plug-ins CloudWatch da AWS e BigQuery do GCP para monitoramento multinuvem em um único painel. |



### Analisar

O portal do Azure contém ferramentas internas que permitem analisar dados de monitoramento.

[![Diagrama que mostra a parte Analisar da seção Consumo do sistema do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/analyze-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/analyze-blowup-type-2-opt.svg#lightbox)

Expandir a tabela

| Ferramenta                                                   | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Metrics Explorer](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/analyze-metrics) | Use uma interface do usuário do explorador de métricas do Azure Monitor no portal do Azure para investigar a integridade e a utilização de seus recursos. O Metrics Explorer ajuda a traçar gráficos, correlacionar tendências visualmente e investigar picos e quedas nos valores de métrica. O Metrics Explorer contém recursos para aplicar dimensões e filtragem e personalizar gráficos. Esses recursos ajudam você a analisar exatamente os dados necessários de maneira visualmente intuitiva. |
| [Log Analytics](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/log-analytics-overview) | A interface do usuário do Log Analytics no portal do Azure ajuda você a consultar os dados de log coletados pelo Azure Monitor para que você possa recuperar, consolidar e analisar rapidamente os dados coletados. Depois de criar consultas de teste, você poderá analisar diretamente os dados com as ferramentas do Azure Monitor ou salvar as consultas para uso com visualizações ou regras de alerta. Os workspaces do Log Analytics são baseados no Azure Data Explorer, usando um poderoso mecanismo de análise e a avançada KQL (Linguagem de Consulta Kusto). Os Logs do Azure Monitor usam uma versão da Linguagem de Consulta Kusto adequada para consultas de log simples e funcionalidades avançadas, como agregações, junções e análise inteligente. Você pode [começar a usar a KQL](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/get-started-queries) de forma rápida e fácil. OBSERVAÇÃO: às vezes, o termo "Log Analytics" é usado para significar o armazenamento da plataforma de dados de Logs do Azure Monitor e a interface do usuário que acessa esse repositório. Anterior a 2019, o termo "Log Analytics" se referia a ambos. Ainda é comum encontrar conteúdo usando esse enquadramento em vários blogs e documentação na Internet. |
| [Análise de Alterações](https://learn.microsoft.com/pt-br/azure/azure-monitor/change/change-analysis) | A Análise de Alterações é um provedor de recursos do Azure no nível da assinatura que verifica as alterações de recursos na assinatura e fornece dados para ferramentas de diagnóstico para ajudar os usuários a entender quais alterações podem ter causado problemas. A interface do usuário da Análise de Alterações no portal do Azure fornece informações sobre a causa de problemas de site dinâmico, interrupções ou falhas de componente. A Análise de Alterações usa o [Azure Resource Graph](https://learn.microsoft.com/pt-br/azure/governance/resource-graph/overview) para detectar vários tipos de alterações, desde a camada de infraestrutura até a implantação do aplicativo. |



### Responder

Uma solução de monitoramento eficaz responde proativamente a eventos críticos, sem a necessidade de um indivíduo ou equipe observar o problema. A resposta pode ser um texto ou email para um administrador ou um processo automatizado que tenta corrigir uma condição de erro.

[![Diagrama que mostra a parte Responder da seção Consumo do sistema do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/respond-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/respond-blowup-type-2-opt.svg#lightbox)

[**AIOps (Inteligência Artificial para Operações de TI)**](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/aiops-machine-learning) pode melhorar a qualidade e a confiabilidade do serviço usando o aprendizado de máquina para processar e agir automaticamente nos dados coletados de aplicativos, serviços e recursos de TI no Azure Monitor. Ele automatiza tarefas controladas por dados, prevê o uso da capacidade, identifica problemas de desempenho e detecta anomalias em aplicativos, serviços e recursos de TI. Esses recursos simplificam o monitoramento e as operações de TI sem a necessidade de experiência em aprendizado de máquina.

**[Alertas do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/alerts-overview)** notificam você sobre condições críticas e podem executar ações corretivas. As regras de alerta podem ser baseadas em dados de métrica ou de log.

- As regras de alerta de métrica fornecem alertas quase em tempo real com base nas métricas coletadas.
- As regras de alerta de pesquisa de log com base em logs permitem uma lógica complexa entre dados de várias fontes.

As regras de alerta usam [grupos de ações](https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/action-groups), que podem executar ações como enviar notificações por email ou SMS. Os grupos de ações podem enviar notificações usando webhooks para disparar processos externos ou integrar-se às ferramentas de gerenciamento de serviços de TI. Os grupos de ações, as ações e os conjuntos de destinatários podem ser compartilhados entre várias regras.

[![Captura de tela que mostra a interface do usuário de alertas do Azure Monitor no portal do Azure.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/alerts.png)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/alerts.png#lightbox)

Atualmente, a MI do SCOM usa seu próprio mecanismo de alerta SCOM tradicional separado no Console de Operações.

O **[dimensionamento automático](https://learn.microsoft.com/pt-br/azure/azure-monitor/autoscale/autoscale-overview)** permite que você controle dinamicamente o número de recursos em execução para lidar com a carga no seu aplicativo. Você pode criar regras que usam métricas do Azure Monitor para determinar o momento de adicionar recursos automaticamente quando a carga aumentar ou remover recursos que estão ociosos. Você pode especificar um número mínimo e máximo de instâncias e a lógica de quando aumentar ou diminuir recursos para economizar dinheiro e aumentar o desempenho.

![Diagrama conceitual mostrando como o dimensionamento automático cresce](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/autoscale.png)

**[Aplicativos Lógicos do Azure](https://learn.microsoft.com/pt-br/azure/logic-apps/logic-apps-overview)** também é uma opção. Para obter mais informações, consulte a seção [Integrar](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview#integrate) abaixo.



## Integração

Talvez seja necessário integrar o Azure Monitor a outros sistemas ou criar soluções personalizadas que usam seus dados de monitoramento. Esses serviços do Azure funcionam com o Azure Monitor para fornecer recursos de integração. Abaixo estão apenas algumas das integrações possíveis.

[![Diagrama que mostra a parte Integrar da seção Consumo do sistema do Azure Monitor.](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/integrate-box-opt.svg)](https://learn.microsoft.com/pt-br/azure/azure-monitor/media/overview/integrate-box-opt.svg#lightbox)

Expandir a tabela

| Serviço do Azure                                             | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Hubs de Evento](https://learn.microsoft.com/pt-br/azure/event-hubs/event-hubs-about) | Os Hubs de Eventos do Azure são uma plataforma de streaming e um serviço de ingestão de eventos. Eles podem transformar e armazenar dados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/envio em lote. Use os Hubs de Eventos para transmitir dados do Azure Monitor a ferramentas de monitoramento e SIEM de parceiros. |
| [Armazenamento do Azure](https://learn.microsoft.com/pt-br/azure/storage/common/storage-introduction) | Exporte dados para o armazenamento do Azure para arquivamento mais barato e de longo prazo de dados de monitoramento para fins de auditoria ou conformidade. |
| [Parceiros hospedados e gerenciados](https://learn.microsoft.com/pt-br/azure/partner-solutions/partners##observability) | Muitos parceiros externos se integram ao Azure Monitor. O Azure Monitor também fez parceria com alguns provedores de monitoramento para fornecer uma [versão hospedada no Azure de seus produtos](https://learn.microsoft.com/pt-br/azure/partner-solutions/partners#observability) para facilitar a interoperabilidade. Exemplos incluem Elastic, Datadog, Logz.io e Dynatrace. |
| [API](https://learn.microsoft.com/pt-br/rest/api/monitor/)   | Várias APIs estão disponíveis para ler e gravar logs e métricas do e para o Azure Monitor, além de acessar os alertas gerados. Você também pode configurar e recuperar alertas. Com as APIs, você tem possibilidades ilimitadas para criar soluções personalizadas que se integram ao Azure Monitor. |
| [Aplicativos Lógicos do Azure](https://learn.microsoft.com/pt-br/azure/logic-apps/logic-apps-overview) | Os Aplicativos Lógicos do Azure são um serviço que você pode usar para automatizar tarefas e processos de negócios usando fluxos de trabalho que se integram a diversos sistemas e serviços com pouco ou nenhum código. Há atividades disponíveis que leem e gravam métricas e logs no Azure Monitor. Você pode usar os Aplicativos Lógicos para [personalizar respostas e executar outras ações em resposta aos alertas do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/alerts-logic-apps). Você também pode executar outras [ações mais complexas](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/logicapp-flow-connector) quando a infraestrutura do Azure Monitor ainda não fornecer um método interno. |
| [Azure Functions](https://learn.microsoft.com/pt-br/azure/azure-functions/functions-overview) | Semelhante aos Aplicativos Lógicos do Azure, Azure Functions oferecem a capacidade de pré-processar e pós-processar dados de monitoramento e executar ações complexas além do escopo de alertas típicos do Azure Monitor. Azure Functions usa código, no entanto, fornecendo flexibilidade adicional sobre os Aplicativos Lógicos. |
| Azure DevOps e GitHub                                        | O Application Insights do Azure Monitor oferece a capacidade de criar a [Integração de Itens de Trabalho](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/release-and-work-item-insights?tabs=work-item-integration) com o monitoramento da inserção de dados nele. As opções adicionais incluem [anotações de versão](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/release-and-work-item-insights?tabs=release-annotations) e [monitoramento contínuo](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/release-and-work-item-insights?tabs=continuous-monitoring). |

Integrações adicionais não mostradas no diagrama que podem ser de interesse.

Expandir a tabela

| Integração                                                   | Descrição                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Defender para Nuvem](https://learn.microsoft.com/pt-br/azure/defender-for-cloud/defender-for-cloud-introduction) | Colete e analise eventos de segurança e execute a análise de ameaças. Confira [Coleta de dados no Defender para Nuvem](https://learn.microsoft.com/pt-br/azure/defender-for-cloud/monitoring-components). |
| [Microsoft Sentinel](https://learn.microsoft.com/pt-br/azure/sentinel/) | Conecta-se com fontes diferentes, incluindo o Office 365 e o Amazon Web Services CloudTrail. Confira [Conectar fontes de dados](https://learn.microsoft.com/pt-br/azure/sentinel/connect-data-sources). |
| [Microsoft Intune](https://learn.microsoft.com/pt-br/mem/intune/fundamentals/what-is-intune) | Crie uma configuração de diagnóstico para enviar logs para o Azure Monitor. Confira [Enviar dados de log para armazenamento, Hubs de Eventos ou análise de logs no Intune (versão prévia)](https://learn.microsoft.com/pt-br/mem/intune/fundamentals/review-logs-using-azure-monitor). |
| [ITSM](https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/itsmc-overview) | O [Conector do gerenciamento de serviços de TI (ITSM)](https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/itsmc-overview) permite que você conecte o Azure e um produto/serviço de ITSM com suporte. |

Essas são apenas algumas opções. Há muitas outras empresas terceirizadas que se integram ao Azure e ao Azure Monitor em vários níveis. Use o seu mecanismo de pesquisa favorito para localizá-los.



## Perguntas frequentes

Esta seção fornece respostas para perguntas comuns.



### Qual é a diferença entre o Azure Monitor, o Log Analytics e o Application Insights?

Em setembro de 2018, a Microsoft combinou o Azure Monitor, o Log Analytics e o Application Insights em um serviço para fornecer monitoramento de ponta a ponta avançado de seus aplicativos e dos componentes dos quais eles dependem. Os recursos do Log Analytics e do Application Insights não foram alterados, embora alguns recursos tenham passado para a marca do Azure Monitor para refletir melhor seu novo escopo. O mecanismo de dados de log e a linguagem de consulta do Log Analytics agora são chamados de Logs do Azure Monitor.



### Quanto custa o Azure Monitor?

O custo do Azure Monitor baseia-se no uso de recursos diferentes e é determinado principalmente pela quantidade de dados coletados. Consulte [Custo e uso do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/usage-estimated-costs) para obter detalhes sobre como os custos são determinados e [Otimização de custos no Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/best-practices-cost) para obter recomendações sobre como reduzir seus gastos gerais.



### Há uma versão local do Azure Monitor?

Não. O Azure Monitor é um serviço de nuvem escalonável que processa e armazena grandes quantidades de dados, embora Azure Monitor possa monitorar recursos locais e em outras nuvens.



### O Azure Monitor se integra ao System Center Operations Manager?

Você pode conectar seu grupo de gerenciamento do System Center Operations Manager existente com o Azure Monitor para coletar dados de agentes para Logs do Azure Monitor. Esse recurso permite usar soluções e consultas de log para analisar os dados coletados de agentes. Você também pode configurar agentes existentes do System Center Operations Manager para enviar dados diretamente para o Azure Monitor. Confira [Conectar o Operations Manager com o Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/agents/om-agents).

A Microsoft também oferece a Instância Gerenciada System Center Operations Manager (SCOM MI) como uma opção para migrar uma configuração tradicional do SCOM para a nuvem com alterações mínimas. Para obter mais informações, consulte [Sobre a Instância Gerenciada SCOM do Azure Monitor](https://learn.microsoft.com/pt-br/system-center/scom/operations-manager-managed-instance-overview).



## Próximas etapas

- [Introdução ao Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/getting-started)
- [Fontes de dados de monitoramento para o Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/data-sources)
- [Coleta de dados no Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/essentials/data-collection)
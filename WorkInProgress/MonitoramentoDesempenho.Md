# Monitoramento de desempenho e disponibilidade híbrida

Hubs de eventos do Azure

Azure Log Analytics

Azure Monitor

Armazenamento do Azure

Máquinas Virtuais do Azure

Essa arquitetura de referência mostra como usar o Azure Monitor para monitorar o desempenho e a disponibilidade de cargas de trabalho do sistema operacional (SO) executadas em VMs (máquinas virtuais). As VMs podem estar no Microsoft Azure, em ambientes locais ou em nuvens que não são do Azure.



## Arquitetura

[![Diagrama que ilustra as funções de monitoramento e disponibilidade do Azure Monitor para cargas de trabalho do sistema operacional no Azure, em ambientes locais e com provedores de nuvem de terceiros. Os dados estão sendo enviados para um workspace do Log Analytics. Os dados são usados pelos serviços Application Insights, Análise, Visualização, Alertas e Escala Automática como parte do Azure Monitor](https://learn.microsoft.com/pt-br/azure/architecture/hybrid/images/hybrid-perf-monitoring.svg)](https://learn.microsoft.com/pt-br/azure/architecture/hybrid/images/hybrid-perf-monitoring.svg#lightbox)

*Baixe um [Arquivo Visio](https://arch-center.azureedge.net/hybrid-perf-monitoring.vsdx) dessa arquitetura.*



### Workflow

- **Escritório principal local – VM 1**. Esse componente é um aplicativo Web com acesso à Internet e uma página da Web voltada para o público, além de agentes do Log Analytics e de dependência instalados. Para obter informações sobre agentes, consulte [Visão geral do agente do Log Analytics](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/log-analytics-agent) e [Visão geral dos agentes do Azure Monitor, Agente de dependência](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/agents-overview#dependency-agent).
- **Escritório principal local – VM 2**. Esse ambiente de lógica de negócios não tem acesso à Internet. No entanto, ele tem agentes do Log Analytics e de dependência instalados.
- **Escritório principal local – VM 3**. Esse componente é um repositório de dados sem acesso à Internet, mas com agentes do Log Analytics e de dependência instalados.
- **Escritório principal local – Gateway do Log Analytics**. O gateway do Log Analytics coleta dados de log e métrica das três VMs locais e os entrega no *workspace do Log Analytics* por meio do TCP (Protocolo de Controle de Transmissão) na porta 443.
- **Escritório principal local - Firewall**. O tráfego de e para o ambiente local é roteado por meio do firewall.
- **Gateway**. O gateway fornece conectividade com a filial.
- **Filial local – VM 4**. Esse componente é o aplicativo de negócios que está sendo executado sem acesso à Internet, mas com agentes de dependência e do Log Analytics instalados. O agente do Log Analytics instalado na VM está configurado para transferir dados diretamente para o workspace do Log Analytics sem a necessidade de um gateway do Log Analytics.
- **Filial local – Gateway**. Esse gateway conecta a filial ao escritório principal local por meio de uma VPN (Rede Virtual Privada).
- **Provedor de nuvem de terceiros – VM 5**. Esse componente é um aplicativo Web com acesso à Internet e uma página da Web voltada para o público, além de agentes do Log Analytics e de dependência instalados.
- **Provedor de nuvem de terceiros – VM 6**. Esse componente é um ambiente de armazenamento de dados sem acesso à Internet, mas com agentes do Log Analytics e de dependência instalados. Não há conectividade direta dos ambientes de provedor de nuvem de terceiros para os ambientes locais.
- **Azure - VMSS**. Esse é um conjunto de dimensionamento criado usando os Conjuntos de Dimensionamento de Máquinas Virtuais do Azure. Ele executa um aplicativo de negócios com os agentes de diagnóstico e análise de log instalados.
- **Azure - Servidor de aplicativo**. Esse servidor tem uma única VM executando um aplicativo de negócios, com o Log Analytics e os agentes de diagnóstico instalados.
- **Métricas do Azure Monitor**. Os dados coletados pelas métricas do Azure Monitor são armazenados em um banco de dados de série temporal otimizado para analisar dados com carimbo de data/hora. Ele também armazena métricas enviadas de VMs locais e VMs do Azure.
- **Azure Monitor - Workspace do Log Analytics**. Esse workspace armazena logs enviados de VMs locais, VMs do Azure e VMs em provedores de nuvem de terceiros. O workspace é um recurso do Azure em que os dados são agregados e que serve como um limite administrativo para acessar esses dados. Outros serviços do Azure Monitor se conectam ao workspace do Log Analytics e usam os dados para várias finalidades. Para saber mais, confira [Como criar uma implantação de Logs do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/design-logs-deployment).
- **Azure Monitor - Insights - Application Insights**. O Application Insights fornece análises de aplicativos e insights sobre seu uso. Nesta arquitetura de exemplo, um teste de ping de disponibilidade verifica a disponibilidade do aplicativo Web local. As regras de alerta são habilitadas para fornecer notificação de um teste com falha. Para obter mais informações, consulte [O que é o Application Insights?](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-insights-overview) e [Monitorar a disponibilidade de qualquer site](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/monitor-web-app-availability).
- **Azure Monitor – Insights – Azure Monitor para VMs**. O Azure Monitor para VMs monitora o desempenho e a integridade das máquinas virtuais e dos conjuntos de dimensionamento de máquinas virtuais. O monitoramento inclui os processos em execução e as dependências de outros recursos. Nesse cenário, o Azure Monitor para VMs fornecerá insights sobre suas máquinas virtuais. Para obter mais informações, consulte [O que é o Azure Monitor para VMs?](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/vminsights-overview).
- **Azure Monitor – Análise**. Os dados de log e métrica das VMs são consultados nas métricas do Azure Monitor e no workspace do Log Analytics usando a KQL (Linguagem de Consulta Kusto). Os resultados fornecem insights sobre a infraestrutura, a topologia e os recursos. Para obter mais informações, consulte [Kusto: visão geral](https://learn.microsoft.com/pt-br/azure/data-explorer/kusto/query/) e [Exemplos de consulta de log do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/log-query/examples).
- **Azure Monitor -Visualizações**. O Azure Monitor usa ferramentas de visualização para examinar os componentes de aplicativo e infraestrutura e as comunicações entre os serviços no Azure Monitor. As ferramentas de visualização incluem o **Mapa do Aplicativo no Application Insight do Azure**, **o recurso Mapa do Azure Monitor para VMs**, **as Pastas de Trabalho do Azure Monitor** e várias exibições de painel disponíveis no Azure Monitor. Para obter mais informações, consulte [Usar o recurso Mapa do Azure Monitor para VMs para entender os componentes do aplicativo](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/vminsights-maps), [Criar e compartilhar painéis de dados do Log Analytics](https://learn.microsoft.com/pt-br/azure/azure-monitor/learn/tutorial-logs-dashboards) e [Pastas de Trabalho do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/workbooks-overview).
- **Azure Monitor - Integrações**. O Azure Monitor se integra a uma variedade de ferramentas e extensões de parceiros e terceiros. Essas ferramentas e extensões aprimoram e se baseiam na funcionalidade existente do Azure Monitor, como análise e visualizações.
- **Azure Monitor – Ações – Alertas**. Variações nos dados de métrica e log podem indicar a ocorrência de eventos. As regras definem as variações de dados que disparam alertas, fornecem notificações e iniciam respostas de correção. Nessa arquitetura, quando um alerta é disparado, os runbooks de automação corrigem automaticamente as VMs locais e as VMs do Azure. Ações de webhook, integração de Gerenciamento de Serviços e outros tipos de ação também estão disponíveis. Para obter mais informações, confira [Criar, exibir e gerenciar alertas de métrica usando o Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/alerts-metric) e [Criar, exibir e gerenciar alertas de log usando o Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/alerts-log).
- **Azure Monitor – Ações – Escala automática**. A Escala automática adiciona ou remove instâncias de VM de acordo com a demanda, o que mantém o desempenho e aumenta a relação custo-benefício. Nessa arquitetura, o Dimensionamento automático tem condições definidas em torno da carga média da CPU (em porcentagem). Quando as condições forem atendidas, a Escala automática do Azure Monitor ajustará o conjunto de dimensionamento de acordo com a demanda. Para saber mais, confira a [Visão geral do dimensionamento automático no Microsoft Azure](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/autoscale-overview).



### Componentes

Essa arquitetura consiste nos seguintes componentes:

- [Máquinas Virtuais do Azure](https://azure.microsoft.com/products/virtual-machines)
- [Azure Monitor](https://azure.microsoft.com/products/monitor)
- [Azure Policy](https://azure.microsoft.com/products/azure-policy)
- [Hubs de eventos do Azure](https://azure.microsoft.com/products/event-hubs)
- [Armazenamento do Azure](https://azure.microsoft.com/product-categories/storage)



## Recomendações

As práticas recomendadas a seguir são recomendações que se aplicam à maioria dos cenários. Siga essas práticas, a menos que você tenha um requisito específico que as substitua.



### Espaço de Trabalho do Log Analytics

Considere as seguintes recomendações ao criar o workspace do Log Analytics:

- Coloque o workspace e os recursos na mesma região do Azure, se a latência for um fator importante.
- Comece com um único workspace do Log Analytics e aumente o número de workspaces à medida que os requisitos mudam.
- Se você tiver equipes e recursos geograficamente dispersos, talvez precise de um workspace por região.
- Seu workspace não precisa estar na mesma assinatura que os recursos que você está executando.



### Alertas

Para cenários mais simples, você pode usar métricas para sinalizar alertas em vez de logs. Métricas:

- Forneça uma contagem ou *valor numérico* para eventos como uso da CPU, memória disponível ou espaço em disco lógico.
- Ter baixa latência.
- Ofereça maior granularidade, por exemplo, intervalos por segundo ou por minuto.
- Notificar você sobre um problema rapidamente.

Para coletar indicadores de desempenho personalizados ou métricas específicas de negócios para fornecer insights mais profundos, use métricas personalizadas. Para obter mais informações, confira [Métricas personalizadas no Azure Monitor (Versão preliminar)](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/metrics-custom-overview).

Os alertas de métricas não são a resposta em todas as situações. Talvez você ainda queira usar alertas baseados em log quando precisar de mais personalização ou correlações mais poderosas.



### Análise e diagnóstico

Considere as seguintes recomendações para análise e diagnóstico:

- Use logs para uma análise mais profunda. Os logs podem:
  - Forneça detalhes detalhados sobre eventos (em comparação com métricas).
  - Acontece de forma intermitente.
  - Facilite diagnósticos mais profundos após um sinalizador de métrica inicial.
- Personalize a coleta de dados de log (que é semelhante às métricas) usando a API do Coletor de Dados HTTP para enviar dados de log para um workspace do Log Analytics. Para mais informações, consulte [Enviar dados de log para o Azure Monitor com a API do Coletor de Dados HTTP (visualização preliminar pública)](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/data-collector-api).
- Analise seus aplicativos de forma proativa com o recurso de **detecção inteligente** do Application Insight. A detecção inteligente aplica os recursos de aprendizado de máquina do Azure e a análise estatística para detectar problemas como anomalias de desempenho ou falha, vazamentos de memória ou degradação geral do aplicativo. Para saber mais, confira [Detecção Inteligente no Application Insights](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/proactive-diagnostics).
- Use o **Azure Monitor para VMs - Mapa** para revisar conexões entre servidores, processos, latência de conexão de entrada e saída e portas em qualquer arquitetura conectada ao TCP. Nenhuma configuração é necessária além da instalação de um agente. Com o **Azure Monitor para VMs – Mapa**, você pode interagir com seus servidores como sistemas interconectados.



### Consultas do Log Analytics

Consulte os dados em um **workspace do Log Analytics** usando o KQL para pesquisar termos, eventos específicos ou estados para identificar tendências e analisar padrões. Use o **Gerenciador de consultas** para procurar e selecionar consultas pré-escritas, modificá-las ou criar suas próprias. Você pode executar, salvar, compartilhar e exportar consultas de dentro de um workspace e fixar suas consultas favoritas em um painel para reutilização.



### Instalação do agente

Instale agentes automaticamente e em escala, em vez de individualmente, usando opções de automação, como Azure Policy, Azure PowerShell, modelos do gerenciador de recursos ou DSC (Configuração de Estado Desejado). Para obter mais informações, consulte [Habilitar o Azure Monitor para VMs usando o Azure Policy](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/vminsights-enable-at-scale-policy), [Habilitar o Azure Monitor para VMs usando o Azure PowerShell](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/vminsights-enable-at-scale-powershell) e [Habilitar o Azure Monitor para VMs para uma máquina virtual híbrida – Configuração de Estado Desejado](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#desired-state-configuration).



### Painel

Para aplicativos críticos, crie uma exibição do **Painel do Azure**. Compartilhe ou disponibilize seu painel em uma tela compartilhada, em tempo real, para pessoas que precisam de dados críticos de aplicativos.



## Considerações

Estas considerações implementam os pilares do Azure Well-Architected Framework, que é um conjunto de princípios de orientação que podem ser usados para aprimorar a qualidade de uma carga de trabalho. Para obter mais informações, confira [Microsoft Azure Well-Architected Framework](https://learn.microsoft.com/pt-br/azure/well-architected/).



### Confiabilidade

A confiabilidade garante que seu aplicativo possa cumprir os compromissos que você assume com os seus clientes. Para obter mais informações, confira [Visão geral do pilar de confiabilidade](https://learn.microsoft.com/pt-br/azure/architecture/framework/resiliency/overview).

As considerações a seguir ajudam a garantir a disponibilidade em seu ambiente.

- Testes de disponibilidade. O teste de ping de URL usado nessa arquitetura é o teste de disponibilidade de

   

  fora para dentro

   

  mais simples. No entanto, outras opções estão disponíveis, como:

  - Teste na Web de várias etapas. Reproduz gravações de solicitações da Web sequenciadas para testar cenários complexos. Os testes da Web de várias etapas são criados no Microsoft Visual Studio Enterprise e, em seguida, carregados no portal para execução.
  - Testes de disponibilidade de acompanhamento personalizados. Use o método `TrackAvailability()` para enviar os resultados do teste para o Application Insights.

- Alertas. Quando você cria um teste de disponibilidade no Application Insights, as notificações de alerta de evento são habilitadas por padrão. Você pode editar as regras de alerta especificando o tipo e os detalhes da notificação em **Alertas do**>**Azure Monitor**.



### Segurança

A segurança fornece garantias contra ataques deliberados e o abuso de seus dados e sistemas valiosos. Para saber mais, confira [Visão geral do pilar de segurança](https://learn.microsoft.com/pt-br/azure/architecture/framework/security/overview).

Os itens a seguir são considerações para tornar seu ambiente mais seguro.

- Espaço de Trabalho do Log Analytics. Os modos de acesso são definidos como um dos seguintes contextos:
  - Contexto do workspace. Todos os logs que o workspace tem permissão para acessar podem ser consultados. Esta é uma abordagem de acesso vertical. Por exemplo, uma equipe de segurança pode precisar de acesso a todos os dados de recursos de cima para baixo.
  - Contexto do recurso. Somente logs de recursos específicos podem ser consultados. Por exemplo, uma equipe de aplicativos pode receber acesso aos logs do recurso específico em que está trabalhando.
- Proteja os dados em trânsito para o Log Analytics. Os dados em trânsito são protegidos usando o TLS 1.2 mínimo. Você não precisa habilitar esse recurso explicitamente. Para saber mais, consulte a [segurança de dados do Log Analytics](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/data-security).
- Proteja os dados em repouso no Log Analytics. Os dados em repouso no Log Analytics são protegidos, de acordo com o Armazenamento do Azure, usando a criptografia AES de 256 bits por padrão.
- Detecção Inteligente. Use a Detecção Inteligente no Application Insights para analisar a telemetria gerada pelo aplicativo e detectar problemas de segurança. Para obter mais informações, consulte [Pacote de detecção de segurança de aplicativo (versão preliminar).](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/proactive-application-security-detection-pack)
- Integre o Azure Monitor às ferramentas de SIEM (Gerenciamento de Eventos e Informações de Segurança). Rotear dados de monitoramento para um hub de eventos com o Azure Monitor para integrar ferramentas externas de monitoramento e SIEM. Para obter mais informações, confira [Transmitir dados de monitoramento do Azure para o hub de eventos ou parceiro externo](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/stream-monitoring-data-event-hubs).



### Otimização de custo

A otimização de custos é a análise de maneiras de reduzir as despesas desnecessárias e melhorar a eficiência operacional. Para obter mais informações, confira [Visão geral do pilar de otimização de custo](https://learn.microsoft.com/pt-br/azure/architecture/framework/cost/overview).

Os itens a seguir são considerações para controlar e gerenciar custos em seu ambiente.

- Azure Monitor. Os custos do Azure Monitor são baseados no consumo, geralmente chamados de *pagamento conforme o uso*.
- Log Analytics. Você paga pela **ingestão** e **retenção de dados**. Você pode estimar e prever o número de VMs e a quantidade de dados (em gigabytes) que espera coletar de cada VM. Uma VM típica do Azure consome entre 1 gigabyte (GB) e 3 GB de dados por mês. Se você estiver avaliando o uso de dados com logs do Azure Monitor, use as estatísticas de dados do seu próprio ambiente e obtenha um desconto com **Reservas de capacidade**.
- Application Insights. Esse componente é cobrado de acordo com o volume de dados de telemetria que seu aplicativo envia e o número de testes da Web executados.
- Consultas de métrica. As consultas de métrica são cobradas pelo número de chamadas feitas.
- Alertas. Os alertas são cobrados com base no tipo e no número de sinais monitorados.
- Notificações. As notificações são cobradas de acordo com o tipo e o número de notificações que você enviar.
- Azure Monitor. A seção **Uso e custos estimados** do Azure Monitor estima seus custos mensais com base nos últimos 31 dias de uso.
- Para obter mais informações, consulte os [preços do Azure Monitor](https://azure.microsoft.com/pricing/details/monitor/) e a [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/?service=monitor).



### Excelência operacional

A excelência operacional abrange os processos de operações que implantam um aplicativo e o mantêm em execução na produção. Para obter mais informações, confira [Visão geral do pilar de excelência operacional](https://learn.microsoft.com/pt-br/azure/architecture/framework/devops/overview).



#### Capacidade de gerenciamento

Veja a seguir considerações para tornar seu ambiente mais gerenciável.

- Pastas de Trabalho do Azure. Use pastas de trabalho para ajudar a realizar análises adicionais e criar relatórios avançados. As pastas de trabalho combinam texto, consultas de log, métricas e parâmetros em relatórios interativos. Os membros da equipe com acesso aos mesmos recursos do Azure podem editar pastas de trabalho. Para obter mais informações, confira [Criar relatórios interativos do Azure Monitor para VMs com pastas de trabalho](https://learn.microsoft.com/pt-br/azure/azure-monitor/insights/vminsights-workbooks).
- Integrações de parceiro. Integre o Azure Monitor a ferramentas de parceiros e terceiros para ajudar com análises, visualizações, alertas ou ao Gerenciamento de Serviços e ao Azure Pipelines. Para saber mais, consulte [Integrações de parceiros do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/partners).
- Integre o Azure Monitor ao Microsoft System Center. Integre o Azure Monitor ao pacote de produtos do System Center. Para saber mais, confira [Conectar o Operations Manager ao Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/om-agents).
- Enviar dados dos Hubs de Eventos do Azure. Para integrar o Azure Monitor com ferramentas externas de visualização e monitoramento, consulte [Transmitir dados de monitoramento do Azure para um hub de eventos ou parceiro externo](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/stream-monitoring-data-event-hubs).
- Gateway do Log Analytics. Para ambientes menores, como de filial, use o agente para transferir dados para o workspace do Log Analytics, em vez de para um gateway. Para obter mais informações, consulte [Estabelecer conectividade com o Log Analytics do Azure](https://learn.microsoft.com/pt-br/services-hub/health/establish-connectivity-to-azure).



#### DevOps

Veja a seguir considerações para integrar seu ambiente a processos e soluções de DevOps.

- Application Insights. Integre o Application Insights ao Azure Pipelines para ajudar a fazer melhorias no desempenho e na usabilidade. O Application Insights é capaz de detectar automaticamente anomalias no desempenho. Ele se conecta a várias ferramentas de desenvolvimento, como Azure DevOps Services e GitHub.

- Instrumentação de aplicativos.

   

  Instrumente

   

  aplicativos modificando o código do aplicativo para habilitar a telemetria com o Application Insights. Os seguintes métodos são maneiras de instrumentar aplicativos:

  - Em tempo de execução. Instrumentar seu aplicativo Web no servidor em tempo de execução é ideal para aplicativos que já estão implantados, pois evita a necessidade de atualizar o código. Os cenários adequados incluem:
    - Aplicativos ASP.NET ou ASP.NET Core da Microsoft hospedados em aplicativos Web do Azure
    - Aplicativos ASP.NET hospedados no IIS (Serviços de Informações da Internet) da Microsoft em uma máquina virtual ou conjunto de dimensionamento de máquinas virtuais
    - Aplicativos ASP.NET hospedados no IIS ou em uma VM local
    - Azure Functions baseado em Java
    - Aplicativos Node.js nos Serviços de Aplicativo do Linux
    - Microsserviços hospedados no AKS
  - No momento do desenvolvimento. Adicione o Application Insights ao seu código para personalizar a coleta de telemetria e enviar mais dados. As linguagens e plataformas compatíveis incluem:
    - Aplicativos ASP.NET
    - Aplicativos do ASP.NET Core
    - Aplicativos de Console .NET
    - Java
    - Node.js
    - Python

- Use o ITSMC (Conector de Gerenciamento de Serviços de TI) para se conectar a ferramentas externas de ITSM (Gerenciamento de Serviços de TI). O ITSMC conecta o Azure a produtos e serviços de ITSM compatíveis, onde os itens de trabalho relacionados a problemas normalmente residem. Para obter mais informações, consulte [Conectar o Azure às ferramentas de ITSM usando o Conector de Gerenciamento de Serviços de TI](https://learn.microsoft.com/pt-br/azure/azure-monitor/platform/itsmc-overview).



### Eficiência de desempenho

A eficiência do desempenho é a capacidade de dimensionar a carga de trabalho de maneira eficiente para atender às demandas exigidas pelos usuários. Para saber mais, confira [Visão geral do pilar de eficiência de desempenho](https://learn.microsoft.com/pt-br/azure/architecture/framework/scalability/overview).

Veja a seguir considerações para dimensionar seu ambiente.

- Automatize a instalação e a configuração de seus recursos e aplicativos.

- Aplicações geograficamente dispersas em grande escala. Use o

   

  Rastreamento Distribuído

   

  no Application Insights para acompanhar dependências e chamadas em vários componentes de aplicativo, recursos de back-end e ambientes de microsserviços. Com o

   

  Rastreamento Distribuído

   

  , você pode depurar aplicativos que chamam além dos limites do processo, fora da pilha local. (Você não precisa habilitar o

   

  Rastreamento Distribuído

  , ele está disponível automaticamente como parte do App Insights.)

  - Duas opções para consumir dados de rastreamento distribuídos são:
    - Experiência de diagnóstico de transação. Essa experiência é semelhante a uma pilha de chamadas com uma dimensão de tempo adicionada. A experiência de diagnóstico de transação fornece visibilidade em uma única transação/solicitação. É útil para encontrar a causa raiz de problemas de confiabilidade e gargalos de desempenho de acordo com a solicitação. Para obter mais informações, confira [O que é Rastreamento Distribuído?](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/distributed-tracing-telemetry-correlation)
    - Experiência de mapa do aplicativo. Isso agrega muitas transações para demonstrar como os sistemas interagem topologicamente e fornecem desempenho médio e taxas de erro. Para obter mais informações, consulte [Mapa do aplicativo: triagem de aplicativos distribuídos](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-map?tabs=net).



## Próximas etapas

Saiba mais sobre as tecnologias dos componentes:

- [Hubs de Eventos do Azure: uma plataforma de streaming de Big Data e um serviço de ingestão de eventos](https://learn.microsoft.com/pt-br/azure/event-hubs/event-hubs-about)
- [Visão geral do Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/overview)
- [Visão geral do Log Analytics no Azure Monitor](https://learn.microsoft.com/pt-br/azure/azure-monitor/logs/log-analytics-overview)
- [O que são conjuntos de escala de máquina virtual?](https://learn.microsoft.com/pt-br/azure/virtual-machine-scale-sets/overview)
- [Visão geral do dimensionamento automático no Microsoft Azure](https://learn.microsoft.com/pt-br/azure/azure-monitor/autoscale/autoscale-overview)
- [O que é o Application Insights?](https://learn.microsoft.com/pt-br/azure/azure-monitor/app/app-insights-overview)



## Recursos relacionados

Explorar arquiteturas relacionadas:

- [Processamento de eventos sem servidor](https://learn.microsoft.com/pt-br/azure/architecture/reference-architectures/serverless/event-processing)
- [Monitoramento do Azure Data Explorer](https://learn.microsoft.com/pt-br/azure/architecture/solution-ideas/articles/monitor-azure-data-explorer)
- [Monitorar um aplicativo de microsserviços no AKS](https://learn.microsoft.com/pt-br/azure/architecture/microservices/logging-monitoring)
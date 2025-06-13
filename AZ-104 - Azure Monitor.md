# Azure Monitor para o Exame AZ-104

Este guia é focado em preparar candidatos para o exame **AZ-104: Microsoft Azure Administrator**, abordando os principais conceitos e tarefas práticas relacionadas ao **Azure Monitor**, uma ferramenta essencial para monitoramento de recursos no Azure. Ele cobre criação, configuração, análise de métricas e logs, alertas e dicas específicas para o exame.

## 1. Introdução ao Azure Monitor

O **Azure Monitor** é uma solução centralizada para coletar, analisar e agir com base em dados de telemetria de recursos no Azure e em ambientes híbridos. Ele é fundamental para o exame AZ-104, pois envolve monitoramento de desempenho, diagnóstico de problemas e configuração de alertas.

### Conceitos-Chave
- **Métricas**: Dados numéricos em tempo real (ex.: CPU, memória), armazenados por 93 dias.
- **Logs**: Dados detalhados de eventos, armazenados em espaços de trabalho do Log Analytics.
- **Alertas**: Notificações baseadas em condições de métricas ou logs.
- **Application Insights**: Monitoramento de aplicativos para desempenho e experiência do usuário.
- **Log Analytics**: Ferramenta para consultas de logs usando Kusto Query Language (KQL).
- **Workbooks**: Relatórios interativos para visualização de dados.

**Dica para o exame**: Entenda a diferença entre métricas (tempo real, numéricas) e logs (detalhados, baseados em eventos).

## 2. Configurando o Azure Monitor

### Passos para Configuração
1. **Acessar o Azure Monitor**:
   - No portal do Azure, vá para "Monitor" para acessar métricas, logs e alertas.
2. **Criar um Espaço de Trabalho do Log Analytics**:
   - Navegue até "Log Analytics Workspaces" > Criar.
   - Escolha assinatura, grupo de recursos, nome e região.
3. **Habilitar Coleta de Dados**:
   - Configure o **Azure Monitor Agent** para VMs ou servidores locais.
   - Use **Data Collection Rules (DCR)** para definir quais dados coletar (ex.: logs de sistema, contadores de desempenho).
4. **Configurar Diagnostic Settings**:
   - Envie logs e métricas de recursos (ex.: VMs, contas de armazenamento) para o Log Analytics.
5. **Visualização**:
   - Crie painéis personalizados ou use **Workbooks** para visualizações interativas.

### Configurações de Rede
- **Conectividade**: O Azure Monitor não requer configurações de rede específicas, mas o agente precisa de acesso à internet ou a endpoints do Azure.
- **Segurança**: Use RBAC para controlar o acesso ao espaço de trabalho do Log Analytics.

**Dica para o exame**: Saiba como criar e configurar um espaço de trabalho do Log Analytics e associá-lo a recursos.

## 3. Métricas no Azure Monitor

### Características
- **Armazenamento**: 93 dias por padrão.
- **Granularidade**: Dados coletados a cada minuto (ou menos, dependendo do recurso).
- **Exemplos**:
  - Percentual de CPU de uma VM.
  - Latência de solicitações em um aplicativo.
  - Taxa de transferência de um disco.

### Tarefas Comuns
- **Acessar Métricas**:
  - No portal, vá para um recurso > "Monitoramento" > "Métricas".
  - Use o **Metrics Explorer** para selecionar métricas e personalizar gráficos.
- **Filtrar e Agrupar**:
  - Filtre por recurso, namespace ou intervalo de tempo.
  - Agrupe por dimensões (ex.: por VM em um grupo de recursos).

**Dica para o exame**: Pratique o uso do Metrics Explorer para criar gráficos e entender namespaces de métricas.

## 4. Logs e Log Analytics

### Log Analytics
- **O que é**: Serviço para armazenar e consultar logs usando KQL.
- **Exemplo de Consulta KQL**:
  ```kql
  AzureMetrics
  | where ResourceName == "myVM"
  | where MetricName == "Percentage CPU"
  | summarize avg(Value) by bin(TimeGenerated, 1h)
  ```
- **Casos de uso**: Diagnosticar falhas, auditar eventos, identificar tendências.

### Configuração
- Crie um espaço de trabalho do Log Analytics.
- Conecte recursos via **Diagnostic Settings** ou agentes.
- Habilite extensões para coletar logs específicos (ex.: logs de IIS, eventos do Windows).

**Dica para o exame**: Domine consultas KQL básicas (filtrar, agrupar, resumir) e saiba como configurar Diagnostic Settings.

## 5. Configurando Alertas

### Tipos de Alertas
- **Alertas de Métricas**: Baseados em valores numéricos (ex.: CPU > 80%).
- **Alertas de Log**: Baseados em resultados de consultas KQL.
- **Alertas de Atividade**: Baseados em eventos do Azure (ex.: criação de recursos).

### Passos para Criar
1. No portal, vá para "Monitor" > "Alertas" > "Nova regra de alerta".
2. **Escopo**: Selecione o recurso (ex.: VM, espaço de trabalho).
3. **Condição**: Defina o limite (ex.: CPU > 80% por 5 minutos) ou consulta KQL.
4. **Ação**: Crie um **Action Group** para notificações (e-mail, SMS) ou ações (ex.: Função do Azure).
5. **Detalhes**: Defina nome, severidade (Sev 0 a Sev 4) e descrição.

**Dica para o exame**: Entenda como criar Action Groups e associá-los a regras de alerta. Saiba diferenciar severidades.

## 6. Monitoramento de Aplicativos com Application Insights

### Características
- Monitora desempenho, falhas e uso de aplicativos.
- Coleta dados como tempo de resposta, taxas de erro e dependências.

### Configuração
- Crie um recurso do Application Insights no portal.
- Adicione o SDK ao aplicativo ou habilite o monitoramento automático.
- Configure painéis para visualizar métricas de aplicativos.

**Dica para o exame**: Saiba que o Application Insights é voltado para aplicativos, enquanto o Azure Monitor cobre infraestrutura.

## 7. Tarefas Práticas para o Exame

### Comandos Úteis do Azure CLI
```bash
# Criar um espaço de trabalho do Log Analytics
az monitor log-analytics workspace create --resource-group <nome-grupo> --workspace-name <nome-workspace> --location <regiao>

# Listar métricas
az monitor metrics list --resource <id-recurso> --metric "Percentage CPU" --interval PT1H

# Criar uma regra de alerta
az monitor metrics alert create --name <nome-alerta> --resource-group <nome-grupo> --condition "avg Percentage CPU > 80" --scopes <id-recurso> --action <id-action-group>
```

### Tarefas no Portal
- **Criar Painéis**: Adicione gráficos de métricas e resultados de consultas KQL.
- **Configurar Alertas**: Crie regras para monitoramento proativo.
- **Executar Consultas KQL**: Use o Log Analytics para diagnosticar problemas.

## 8. Dicas para o Exame AZ-104
- **Pratique KQL**: Aprenda consultas básicas para filtrar, agrupar e resumir dados.
- **Domine Alertas**: Saiba criar e gerenciar regras de alerta e Action Groups.
- **Métricas vs. Logs**: Entenda quando usar cada um e suas limitações.
- **Cenários Práticos**: Esteja preparado para cenários como "identificar alta utilização de CPU" ou "configurar alertas para falhas".
- **Pratique no Portal**: Use uma conta gratuita ou sandbox para explorar o Azure Monitor.

## 9. Recursos Adicionais
- **Microsoft Learn**: Acesse módulos sobre o Azure Monitor no caminho de aprendizado do AZ-104.
- **Documentação do Azure**: Consulte a documentação oficial do Azure Monitor.
- **Laboratórios Práticos**: Use Qwiklabs ou o Azure Sandbox para prática.

**Dica final**: Foque em cenários práticos, como configurar alertas, interpretar métricas e escrever consultas KQL. Familiarize-se com a interface do Azure Monitor no portal para ganhar confiança no exame.

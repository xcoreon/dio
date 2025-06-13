# Gerenciando Máquinas Virtuais no Azure para o Exame AZ-104

Este guia é focado em preparar candidatos para o exame **AZ-104: Microsoft Azure Administrator**, abordando os principais conceitos e tarefas práticas relacionadas ao gerenciamento de máquinas virtuais (VMs) no Microsoft Azure. Ele cobre os tópicos mais relevantes do exame, como criação, configuração, monitoramento, dimensionamento e segurança de VMs.

## 1. Introdução às Máquinas Virtuais no Azure

Máquinas virtuais (VMs) no Azure são recursos de computação que permitem executar sistemas operacionais e aplicativos em um ambiente virtualizado. Elas são fundamentais para o exame AZ-104, pois envolvem configurações de rede, armazenamento, dimensionamento e segurança.

### Conceitos-Chave
- **Regiões e Zonas de Disponibilidade**: Escolha a região e zona para alta disponibilidade e resiliência.
- **Tamanhos de VM**: Escolha entre séries como D, E, F, etc., com base em CPU, memória e armazenamento.
- **Imagens de VM**: Use imagens do Azure Marketplace (Windows/Linux) ou crie imagens personalizadas.
- **Azure Hybrid Benefit**: Reduz custos ao usar licenças existentes do Windows Server ou SQL Server.

**Dica para o exame**: Entenda as diferenças entre **Stop (Desalocado)** e **Stop (Alocado)** para gerenciar custos. VMs desalocadas não geram custos de computação, mas podem manter custos de armazenamento.

## 2. Criando e Configurando VMs

### Passos para Criar uma VM
1. **Acesse o Portal do Azure**:
   - Navegue até "Máquinas Virtuais" e clique em "Criar".
2. **Configurações Básicas**:
   - **Assinatura e Grupo de Recursos**: Escolha ou crie um grupo de recursos.
   - **Nome da VM**: Defina um nome único.
   - **Região**: Selecione a região apropriada.
   - **Imagem**: Escolha Windows, Linux ou uma imagem personalizada.
   - **Tamanho**: Selecione o tamanho da VM (ex.: `D2s_v3` para uso geral).
   - **Autenticação**: Use senha ou chave SSH para Linux.
3. **Configurações Avançadas**:
   - **Discos**: Escolha entre HDD, SSD Standard ou SSD Premium.
   - **Rede**: Configure grupo de segurança de rede (NSG) e sub-rede.
   - **Extensões**: Adicione extensões como antivírus ou monitoramento.
4. **Revisar e Criar**: Valide as configurações e implante a VM.

### Configurações de Rede
- **Grupo de Segurança de Rede (NSG)**: Crie regras para permitir/negá tráfego (ex.: porta 3389 para RDP, 22 para SSH).
- **Endereço IP Público**: Atribua IPs públicos ou use um balanceador de carga.
- **DNS**: Configure nomes DNS para facilitar o acesso.

**Dica para o exame**: Saiba como configurar regras de NSG e associá-las a VMs ou sub-redes. Entenda as portas padrão (RDP: 3389, SSH: 22, HTTP: 80).

## 3. Gerenciando Discos de VMs

### Tipos de Discos
- **Discos do Sistema Operacional**: Armazenam o SO da VM.
- **Discos de Dados**: Armazenam dados do usuário.
- **Discos Temporários**: Não persistentes, usados para dados temporários.

### Tarefas Comuns
- **Adicionar Disco**:
  - No portal, vá até a VM > Discos > Adicionar disco de dados.
  - Escolha o tipo (SSD Premium, HDD Standard) e tamanho.
- **Snapshots**: Crie instantâneos para backup ou para criar imagens.
- **Managed Disks vs. Unmanaged Disks**:
  - **Managed Disks**: Gerenciados pelo Azure, recomendados para simplicidade e escalabilidade.
  - **Unmanaged Disks**: Gerenciados pelo usuário em contas de armazenamento, menos comuns.

**Dica para o exame**: Entenda como redimensionar discos sem tempo de inatividade e como usar snapshots para recuperação.

## 4. Dimensionamento e Alta Disponibilidade

### Conjuntos de Escala de Máquinas Virtuais (VMSS)
- **O que é**: Um grupo de VMs idênticas que escalam automaticamente com base em regras.
- **Configuração**:
  - Defina regras de escalonamento (ex.: aumentar VMs se CPU > 70%).
  - Configure balanceadores de carga para distribuir tráfego.
- **Casos de uso**: Aplicativos web, workloads que requerem escalabilidade.

### Conjuntos de Disponibilidade
- **O que é**: Agrupa VMs em domínios de falha e atualização para evitar downtime.
- **Configuração**:
  - Defina domínios de falha (FD) e atualização (UD).
  - Recomenda-se usar com balanceadores de carga.

**Dica para o exame**: Saiba a diferença entre VMSS (escalabilidade horizontal) e Conjuntos de Disponibilidade (resiliência).

## 5. Monitoramento e Backup

### Azure Monitor
- **Métricas**: Monitore CPU, memória e uso de disco.
- **Alertas**: Configure alertas para eventos críticos (ex.: CPU > 80%).
- **Logs**: Use o Log Analytics para consultas detalhadas.

### Azure Backup
- **Configuração**:
  - Crie um cofre de recuperação de serviços (Recovery Services Vault).
  - Configure políticas de backup para VMs.
- **Restauração**: Restaure VMs ou discos individuais a partir de pontos de recuperação.

**Dica para o exame**: Saiba como configurar backups e restaurar VMs usando o Azure Backup.

## 6. Segurança e Conformidade

### Melhores Práticas
- **Azure Security Center**: Use recomendações para melhorar a segurança (ex.: habilitar criptografia de disco).
- **Azure Disk Encryption**: Proteja discos com chaves gerenciadas pelo cliente ou pela plataforma.
- **RBAC (Controle de Acesso Baseado em Funções)**: Atribua permissões específicas para gerenciar VMs.
- **Atualizações**: Use o Azure Update Management para gerenciar patches.

**Dica para o exame**: Entenda como integrar o Azure Security Center e aplicar políticas de conformidade.

## 7. Tarefas Práticas para o Exame

### Comandos Úteis do Azure CLI
```bash
# Criar uma VM
az vm create --resource-group <nome-grupo> --name <nome-vm> --image UbuntuLTS --admin-username <usuario> --admin-password <senha>

# Iniciar/Parar uma VM
az vm start --resource-group <nome-grupo> --name <nome-vm>
az vm stop --resource-group <nome-grupo> --name <nome-vm>

# Listar VMs
az vm list --resource-group <nome-grupo> --output table
```

### Tarefas no Portal
- **Redimensionar uma VM**: Alterar o tamanho da VM para atender a novas demandas.
- **Configurar NSG**: Criar regras para permitir tráfego específico.
- **Adicionar Extensões**: Instalar o agente de monitoramento ou scripts personalizados.

## 8. Dicas para o Exame AZ-104
- **Pratique no Portal do Azure**: Use uma conta gratuita ou sandbox para criar e gerenciar VMs.
- **Entenda Custos**: Saiba como otimizar custos (ex.: desligar VMs, usar discos gerenciados).
- **Conceitos de Rede**: Domine NSGs, VNETs e IPs públicos.
- **Alta Disponibilidade**: Entenda VMSS e Conjuntos de Disponibilidade.
- **Segurança**: Familiarize-se com RBAC, Azure Security Center e criptografia.

## 9. Recursos Adicionais
- **Microsoft Learn**: Acesse o caminho de aprendizado para o AZ-104.
- **Documentação do Azure**: Consulte a documentação oficial para VMs.
- **Laboratórios Práticos**: Use plataformas como Qwiklabs ou laboratórios da Microsoft para prática.

**Dica final**: Para o exame, foque em cenários práticos, como configurar uma VM para um aplicativo web ou solucionar problemas de conectividade de rede.

Relatorio tecnico
Repositório contendo a prática de simulação de ambiente hierárquico com configuração de VLANs de acesso (Alunos e Visitantes) no Cisco Packet Tracer.

Relatório Técnico: Configuração de VLANs de Acesso em Ambiente Hierárquico1. Visão Geral do ProjetoEste projeto contempla a implementação e segregação de redes de camada 2 por meio da configuração de VLANs do tipo Acesso em switches de infraestrutura simulada no Cisco Packet Tracer.
O objetivo principal é garantir a correta segmentação e o isolamento de tráfego entre a rede de alunos e a rede de visitantes nos switches da camada de acesso.2.

Parâmetros e Mapeamento TécnicoTabela de Definição de VLANsID da VLANNome da VLANFinalidade / Público10AlunosTráfego administrativo e pedagógico associado aos computadores (PCs).20VisitantesTráfego de convidados/visitantes associado aos notebooks (Laptops).
Mapeamento das Interfaces de AcessoEquipamentoPadrão de InterfacesModo de OperaçãoVLAN AssociadaDispositivo Final ConectadoSwitches de AcessoPortas Ímpares (1/0/1, 1/0/3, 1/0/5...)AccessVLAN 10Computadores (PCs)Switches de AcessoPortas Pares (1/0/2, 1/0/4, 1/0/6...)AccessVLAN 20Notebooks (Laptops)3. Diagrama da TopologiaAbaixo está representada a topologia de redes hierárquica configurada no Cisco Packet Tracer:


Step 2: Criar e nomear as VLANs

vlan 10

 name Alunos
 
exit

vlan 20
 name Visitantes
exit
 Step 3: Configurar o intervalo de portas ímpares para a VLAN 10 (Alunos)
interface range GigabitEthernet 1/0/1 , GigabitEthernet 1/0/3 , GigabitEthernet 1/0/5 , GigabitEthernet 1/0/7 , GigabitEthernet 1/0/9 , GigabitEthernet 1/0/11 , GigabitEthernet 1/0/13 , GigabitEthernet 1/0/15 , GigabitEthernet 1/0/17 , GigabitEthernet 1/0/19 , GigabitEthernet 1/0/21 , GigabitEthernet 1/0/23
 switchport mode access
 switchport access vlan 10
exit

! Step 4: Configurar o intervalo de portas pares para a VLAN 20 (Visitantes)
interface range GigabitEthernet 1/0/2 , GigabitEthernet 1/0/4 , GigabitEthernet 1/0/6 , GigabitEthernet 1/0/8 , GigabitEthernet 1/0/10 , GigabitEthernet 1/0/12 , GigabitEthernet 1/0/14 , GigabitEthernet 1/0/16 , GigabitEthernet 1/0/18 , GigabitEthernet 1/0/20 , GigabitEthernet 1/0/22 , GigabitEthernet 1/0/24
 switchport mode access
 switchport access vlan 20
exit

! Step 5: Salvar as alterações no startup-config
end

5. Validação da ConfiguraçãoA validação do mapeamento das portas de acesso e do status das VLANs foi realizada executando o comando de inspeção abaixo no modo privilegiado:show vlan brief
Evidência de ExecuçãoConfirmação de alocação das interfaces nas respetivas VLANs (active):Projeto desenvolvido para a Atividade Prática de Simulação de Redes Hierárquicas.

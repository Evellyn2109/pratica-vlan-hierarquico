Prática de Simulação de Ambiente Hierárquico: Configuração de VLANs de Acesso

Este repositório contém a documentação técnica e o tutorial passo a passo para a configuração de VLANs de acesso em switches de uma rede hierárquica simulada no Cisco Packet Tracer.

📸 1. Evidências de Configuração (CLI dos Switches)

Nesta seção estão registradas as capturas de tela dos switches após a execução dos comandos de validação (show vlan brief).
<img width="702" height="705" alt="image" src="https://github.com/user-attachments/assets/fa5a4ccd-9bba-435e-941b-3a7284556453" />

<img width="698" height="704" alt="image" src="https://github.com/user-attachments/assets/56e6943f-5bf8-4cc2-a547-4b782438fc29" />


Validação do mapeamento das portas FastEthernet ímpares para a VLAN 10 (Alunos) e pares para a VLAN 20 (Visitantes).

Switch de Distribuição / Core (SW-DIS0)

<img width="705" height="706" alt="image" src="https://github.com/user-attachments/assets/8fa56b19-1693-4cba-be8f-81cdca7d121b" />

Status das VLANs e interfaces GigabitEthernet no switch da camada de distribuição.

 2. Topologia do Ambiente Hierárquico

A topologia segue o modelo hierárquico Cisco de 3 camadas (Core, Distribuição e Acesso), separando o tráfego dos usuários finais nas interfaces dos switches de acesso:

                 +-----------------------+
                 |       SW-CORE         |
                 |     (Camada Core)     |
                 +-----------+-----------+
                             |
                 +-----------+-----------+
                 |        SW-DIS0        |
                 | (Camada Distribuição) |
                 +-----------+-----------+
                             |
               +-------------+-------------+
               |                           |
     +---------+---------+       +---------+---------+
     |    SW-ACESS1      |       |    SW-ACESS2      |
     | (Camada Acesso)   |       | (Camada Acesso)   |
     +----+---------+----+       +----+---------+----+
          |         |                 |         |
       Portas    Portas            Portas    Portas
      Ímpares     Pares           Ímpares     Pares
         |          |                |          |
     [ Alunos ] [Visitantes]     [ Alunos ] [Visitantes]
     (Desktops) (Notebooks)      (Desktops) (Notebooks)


 3. Mapeamento e Documentação Técnica

ID da VLAN

Nome

Tipo de Interface

Portas Associadas

Dispositivos Conectados

10

Alunos

Access (Acesso)

Fa0/1, Fa0/3, Fa0/5, Fa0/7, Fa0/9, Fa0/11, Fa0/13, Fa0/15, Fa0/17, Fa0/19, Fa0/21, Fa0/23

Computadores (Desktops)

20

Visitantes

Access (Acesso)

Fa0/2, Fa0/4, Fa0/6, Fa0/8, Fa0/10, Fa0/12, Fa0/14, Fa0/16, Fa0/18, Fa0/20, Fa0/22, Fa0/24

Notebooks

1

default

Native

Gig0/1, Gig0/2 (Uplinks mantidos fora do escopo desta etapa)

Conexões de Interligação

🛠️ 4. Script de Comandos Cisco IOS

Abaixo está a sequência completa de comandos necessária para replicar a configuração nos switches da camada de acesso.

Etapa A: Criação e Nomeação das VLANs

! Entrar no modo de operacao privilegiado
enable

! Entrar no modo de configuracao global
configure terminal

! Criacao da VLAN 10 para Alunos
vlan 10
 name Alunos

! Criacao da VLAN 20 para Visitantes
vlan 20
 name Visitantes
exit


Etapa B: Configuração das Portas Ímpares (VLAN 10 - Alunos)

! Selecionar o intervalo de portas impares
interface range fastEthernet 0/1, fastEthernet 0/3, fastEthernet 0/5, fastEthernet 0/7, fastEthernet 0/9, fastEthernet 0/11, fastEthernet 0/13, fastEthernet 0/15, fastEthernet 0/17, fastEthernet 0/19, fastEthernet 0/21, fastEthernet 0/23

! Definir o modo da porta como acesso
 switchport mode access

! Vincular as portas a VLAN 10
 switchport access vlan 10
exit


Etapa C: Configuração das Portas Pares (VLAN 20 - Visitantes)

! Selecionar o intervalo de portas pares
interface range fastEthernet 0/2, fastEthernet 0/4, fastEthernet 0/6, fastEthernet 0/8, fastEthernet 0/10, fastEthernet 0/12, fastEthernet 0/14, fastEthernet 0/16, fastEthernet 0/18, fastEthernet 0/20, fastEthernet 0/22, fastEthernet 0/24

! Definir o modo da porta como acesso
 switchport mode access

! Vincular as portas a VLAN 20
 switchport access vlan 20
exit


Etapa D: Salvando a Configuração na Memória NVRAM

! Retornar ao modo privilegiado
end

! Salvar configuracoes
copy running-config startup-config


5. Validação da Configuração

Para verificar se o procedimento foi aplicado com sucesso, utilize o comando:

SW-ACESS1# show vlan brief


Resultado esperado:

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gig0/1, Gig0/2
10   Alunos                           active    Fa0/1, Fa0/3, Fa0/5, Fa0/7
                                                Fa0/9, Fa0/11, Fa0/13, Fa0/15
                                                Fa0/17, Fa0/19, Fa0/21, Fa0/23
20   Visitantes                       active    Fa0/2, Fa0/4, Fa0/6, Fa0/8
                                                Fa0/10, Fa0/12, Fa0/14, Fa0/16
                                                Fa0/18, Fa0/20, Fa0/22, Fa0/24
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    

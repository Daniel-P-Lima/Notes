![[Redes Convergentes]]
### **1) Objetivos gerais** 

- Garantir conectividade segura e eficiente entre os dois sites.
- Fornecer segregação de rede adequada para os dois departamentos em cada site.
- Centralizar serviços corporativos no datacenter do Site da Matriz.
- Garantir alta disponibilidade, segurança e desempenho da rede.
### **2) Descrição do Cenário** 

A empresa ACME SA  possui duas localidades onde estão alocados seus departamentos e colaboradores. O primeiro, a Matriz, situada em São Paulo, possui cerca de 150 usuários enquanto o segundo, a Filial, situada em Curitiba, possui 100 usuários. Cada local possui 2 departamentos que devem ter suas redes independentes, mas interconectadas.  Localmente em cada site há um sistema ERP (HTTP). Na matriz, ainda há um servidor DNS que é utilizado para resolver os nomes referentes aos servidores ERP de ambos sites:  www.acme.com.br e 
www.acmefilial.com.br. Em ambos os locais, em termos de acessos externos à Internet, os usuários podem acessar apenas serviços baseados em HTTP, HTTPS e DNS e ping, para testes de conectividade. Além disso, há um serviço de telefonia IP baseado em SIP(UDP-5060,5061)/RTP(UDP-10000 a 11000)  que interconecta os ramais (softphones) internamente e entre os sites. Usar IP privados internamente. Recomenda-se nas redes ponto-a-ponto usar prefixo /30. Cada departamento está situado num andar. Cada andar terá um switch de acesso.

### **3) Conexão Entre os Sites**

- **Link Principal:** Conexão através de VPN sobre a Internet.
- **Link de Backup:** Conexão de redundância para garantir continuidade de serviço em caso de falha do link principal.

## Topologia do Projeto 
![[Captura de Tela 2024-10-13 às 22.14.03.png]]
### MATRIZ
#### Escolha de IP's privados para matriz:
- Para a primeira VLAN, a VLAN 10, do departamento 1 foi usado a rede IP 192.168.100.0/25, com o gateway padrão sendo 192.168.100.1
- Para a segunda VLAN, a VLAN 20, do departamento 2 foi usado a rede IP 192.168.100.128/25, com o gateway padrão sendo 192.168.100.129
- Para as duas VLAN's, a máscara /25 é equivalente a 255.255.255.128
##### Topologia da Matriz
![[Captura de Tela 2024-10-13 às 22.20.26.png]]

### VLAN's na matriz
- No SWITCH camada 2 em nossa matriz foram criadas as VLAN's, definindo as portas do SWITCH conectadas as máquinas corretas.
##### SWITCH - Primeiro Andar
![[Captura de Tela 2024-10-13 às 22.22.23.png]]
#### Máquinas Primeiro Andar
Cada uma separada por VLAN's diferentes
##### Máquina 1 - VLAN 10
![[Captura de Tela 2024-10-13 às 22.27.08.png]]
##### Máquina 2 - VLAN 20
![[Captura de Tela 2024-10-13 às 22.28.18.png]]
##### SWITCH - Segundo Andar
![[Captura de Tela 2024-10-13 às 22.25.21.png]]
#### Máquinas Segundo Andar
Cada uma separada por VLAN's diferentes
##### Máquina 1 - VLAN 10
![[Captura de Tela 2024-10-13 às 22.29.52.png]]
##### Máquina 2 - VLAN 20
![[Captura de Tela 2024-10-13 às 22.31.45.png]]
### SWITCH's Camada Três
Para os SWITCH's camada três as configurações foram um pouco diferentes já que, é necessário criar uma rota das VLAN's para poder identificar os pacotes e também, definir as entradas corretas como modo trunk. Também se deve criar as VLAN's.
Para a conexão dos SWITCH's com o roteador da matriz também usamos redes /30, com a máscara de 255.255.255.252, sendo o padrão para redes ponto a ponto (_P2P_)
##### Rede Ponto a Ponto
![[Captura de Tela 2024-10-13 às 22.45.00.png]]
##### Primeiro SWITCH Camada Três
![[Captura de Tela 2024-10-13 às 22.34.37.png]]
##### Segundo SWITCH Camada Três
![[Captura de Tela 2024-10-13 às 22.36.44.png]]

### Roteador Matriz
Para o roteador na matriz temos três rotas estáticas, duas são referentes as rotas das VLAN's para envio de pacotes entre elas e a terceira rota definida como rota _default_ para qualquer pacote ser enviado a rumo da internet
![[Captura de Tela 2024-10-13 às 22.38.39.png]]
### Data Center Matriz
Nosso datacenter temos o ERP, DNS e voiP. 
##### SWITCH Data Center
![[Captura de Tela 2024-10-13 às 22.47.40.png]]
##### ERP - Data Center Matriz
![[Captura de Tela 2024-10-13 às 22.49.36.png]]
##### DNS - Data Center Matriz
Esse é o servidor DNS que está configurado para acesso aos links www.acme.com.br e www.acmefilial.com.br com alguma diferença que será abordada mais pra frente
![[Captura de Tela 2024-10-13 às 22.52.43.png]]
##### Configuração do DNS
![[Captura de Tela 2024-10-13 às 22.55.59.png]]
##### voIP - Data Center Matriz
![[Captura de Tela 2024-10-13 às 22.56.43.png]]

### FILIAL
#### Escolha de IP's privados para filial:
- Para a primeira VLAN, a VLAN 10, do departamento 1 foi usado a rede IP 192.168.10.0/25, com o gateway padrão sendo 192.168.10.1
- Para a segunda VLAN, a VLAN 20, do departamento 2 foi usado a rede IP 192.168.10.128/25, com o gateway padrão sendo 192.168.10.129
- Para as duas VLAN's, a máscara /25 é equivalente a 255.255.255.128
##### Topologia da Filial
![[Captura de Tela 2024-10-13 às 22.59.57.png]]
### VLAN's na filial
- No SWITCH camada 2 em nossa matriz foram criadas as VLAN's, definindo as portas do SWITCH conectadas as máquinas corretas.
##### SWITCH - Primeiro Andar
![[Captura de Tela 2024-10-13 às 23.03.24.png]]
#### Máquinas Primeiro Andar
Cada uma separada por VLAN's diferentes
##### Máquina 1 - VLAN 10
![[Captura de Tela 2024-10-13 às 23.03.51.png]]
##### Máquina 2 - VLAN 20
![[Captura de Tela 2024-10-13 às 23.04.15.png]]
##### SWITCH - Segundo Andar
![[Captura de Tela 2024-10-13 às 23.04.44.png]]
#### Máquinas Segundo Andar
Cada uma separada por VLAN's diferentes
##### Máquina 1 - VLAN 10
![[Captura de Tela 2024-10-13 às 23.05.28.png]]
##### Máquina 2 - VLAN 20
![[Captura de Tela 2024-10-13 às 23.06.04.png]]
### SWITCH's Camada Três
Para os SWITCH's camada três as configurações foram um pouco diferentes já que, é necessário criar uma rota das VLAN's para poder identificar os pacotes e também, definir as entradas corretas como modo trunk. Também se deve criar as VLAN's.
Para a conexão dos SWITCH's com o roteador da matriz também usamos redes /30, com a máscara de 255.255.255.252, sendo o padrão para redes ponto a ponto (_P2P_)
##### Rede Ponto a Ponto
![[Captura de Tela 2024-10-13 às 23.07.15.png]]
##### Primeiro SWITCH Camada Três
![[Captura de Tela 2024-10-13 às 23.08.39.png]]
##### Segundo SWITCH Camada Três
![[Captura de Tela 2024-10-13 às 23.09.13.png]]

### Roteador Filial
Para o roteador da filial temos três rotas estáticas, as duas primeiras são reservadas para as rotas das VLAN's para a troca de pacotes. A terceira rota estática é definida como a rota _default_ para enviar os pacotes em direção a internet
![[Captura de Tela 2024-10-13 às 23.10.04.png]]
### Data Center Filial
Nesse data center temos algo diferente da filial, o servidor DNS não é definido aqui. Nós acessamos o servidor DNS www.acmefilial.com.br via ERP. As máquinas da filial estão com IP público do DNS, mas para fazer a diferenciação se usa o ERP
Por conta disso temos definido apenas ERP e voIP
##### SWITCH Data Center FIlial
![[Captura de Tela 2024-10-13 às 23.16.27.png]]
##### ERP - Data Center Filial
![[Captura de Tela 2024-10-13 às 23.17.26.png]]
#### voIP - Data Center Filial
![[Captura de Tela 2024-10-13 às 23.18.43.png]]
### Conexão com a internet
Para os IP's públicos foi definido a seguinte faixa de IP's:

| Endereço IP Inicial | Endereço IP Final |
| ------------------- | ----------------- |
| 128.14.238.0        | 128.14.238.255    |
- Para poder acessar as redes externas e também alguma máquina acessar outra rede seja, matriz para filial, filial para matriz, os servidores tem IP's dedicados de tradução para a comunicação externa, com NAT/PAT estático
- Os lados internos são definidos para o firewall da matriz e o firewall da filial
![[Captura de Tela 2024-10-13 às 23.19.55.png]]

### Contrato de Plano Empresarial
Para a empresa poder se conectar com a internet temos dois roteadores, um com o plano empresarial da Vivo Fibra - Download 700Mbps e Upload 350Mpbs.
Para o segundo roteador será usado outro plano de internet, caso caia o primeiro ainda haverá conexão. Com um plano empresarial da Oi Fibra - Download 700Mbps e Upload 350Mpbs
![[Captura de Tela 2024-10-13 às 23.31.29.png]]
![[Captura de Tela 2024-10-13 às 23.33.07.png]]
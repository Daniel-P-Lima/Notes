- Apenas um SO por máquina
- Software e hardware altamente acoplados
# Conjunto de Instruções (ISA)
---
User ISA -> Cria uma abstração maior para o usuário
Kernel ISA -> Todo o conjunto de instruções

1. O usuário se comunica com o kernel por chamadas de sistemas, ```syscall```
	- Implementado pelo S.O
	- Facilita o acesso do usuário ao hardware

Sistemas operacionais diferentes se comportam de maneiras diferentes em relação ao ```syscall``` as chamadas de sistemas são diferentes

Em sistemas windows e linux tem implementações totalmente diferentes mesmo sendo da arquitetura x86, causando um **conflito entre aplicações**

Considerando os problemas, a manutenção se torna difícil
# Virtualização
----
"Fingir que tem um sistema operacional rodando em cima de outro sistema operacional"
- Permite **desacoplar a infraestutura** de serviços dos dispositivos/recursos físicos
	- Máquinas virtuais
	- JVM
	- Docker
- Torna a camada de serviços totalmente **abstraída em nível de software**
## Tipos de Hypervisors (Camada de Virtualização)
----
### Tipo 1
Divisão mais justa dos componentes dos sistemas operacionais
- Cada máquina virtual tem seu isolamento, uma não enxerga a memória da outra. Isolada quase a nível de hardware
- O hardware deve suportar a virtualização
	- Ter a capacidade de abstração de memória
	- Tornar o acesso isolado nativamente
### Tipo 2 
A camada de virtualização é dentro do sistema operacional, com as máquinas virtuais
A gestão de recursos é feita pelo sistema operacional
- É executada como uma aplicação de host
- O padrão utilizado
1. Vantagens:
	- Executado independente do hardware
	- Maior compatibilidade 
2. Desvantagens:
	- Performance vira uma desvantagem 
	- Menor compatibilidade de VMs
	- Menor controle sobre hardware
# Máquina Virtual
----
- Independente do hardware
- **A VM convidada executa sobre a abstração do hardware virtualizado**
	- A camada de virtualização traduz o hardware ARM para x86 por exemplo
	- A máquina virtual enxerga de forma abstrata o hardware adjacente 
- **Isolamento**
	- SO da VM é isolado do ambiente do host
	- A VM só enxerga uma parte da memória e qualquer outro recurso
	- Interface de comunicação entre entidades
- **Encapsulamento**
	- VM é encapsulada independentemente do host
# Como é alcançada a virtualização?
- Depende do hypervisor
	- Dentro do hypervisor também haverá um escalonador VMM
- Threads são executadas de acordo com o escalonador de thread
- Processos são executadas de acordo com escalonador do SO
- Cada máquina virtual recebe uma fatia do CPU
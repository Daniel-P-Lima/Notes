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
"Fingir que tem um sistema operacional rodando em cima de outro sistema operacional"
- Permite **desacoplar a infraestutura** de serviços dos dispositivos/recursos físicos
	- Máquinas virtuais
	- JVM
	- Docker
- Torna a camada de serviços totalmente **abstraída em nível de software**

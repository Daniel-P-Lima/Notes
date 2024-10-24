![[Sistemas Ciberfísicos]]
_Internet of Things (IoT)_
# Estrutura de um Processo no Contiki
Um processo tem:
- Um ==bloco de controle de processo== e um ==thread de processo==
- O BCP é armazenado na RAM, Contém
	- Nome do processo
	- Estado do processo
	- Ponteiro para o thread do processo
- O bloco de controle de processo é usado apenas internamente pelo kernel\
- Nunca deve ser acessado diretamente pelo processo
```
#include "contiki.h"
#include <stdio.h>

PROCESS(socps_process, "Hello World!!");
AUTOSTART_PROCESSES(&socps_process);

PROCESSES_THREAD(socps_process, ev, data) {
	PROCESS_BEGIN();
	while (true) {
		printf("SOCPS - Hello World!!!\n");
	}
	PROCESS_END();
}
```

# Escalonador Contiki
Todos os eventos são ==síncronos==
Invocar processos quando for sua hora de execução
## process_start()
- É chamado implicitamente no ```AUTOSTART_PROCESSES```
- Configura a estrutura de controle do processo
- Coloca o processo na lista do kernel de processos 
- É utilizado o algoritmo de fila, First-in First-out
# Protothread - Contiki
- Permite estruturar o código de forma que o sistema execute outras atividades quando o código estiver esperando que algo aconteça 
- São usados em vários sistemas como o linux 
- É uma função regular no ```C```
- Threads podem compartilhar um contexto de memória 
A função começa e termina com duas macros especiais, ```PT_BEGIN() e PT_END()``` 
## O processo implementa sua própria versão de protothreads
```
PROCESS_BEGIN()
PROCESS_END()
PROCESS_EXIT()
PROCESS_WAIT_EVENT()
```
# Eventos
## Assíncronos
Um processo é executado quando recebe um evento 
==Quando eventos assíncronos são postados, o evento é colocado na fila de eventos no kernel e entregue ao processo sequencialmente==  
## Síncronos
São entregues imediatamente quando postados, um atrás do outro
## Identificador de eventos
Eventos são identificados por um identificador de evento
Todos os eventos tem IDS específicos para identificar o tal processo
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
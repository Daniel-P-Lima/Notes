![[Estrutura de dados]]
# Entendendo o que é uma árvore binária
Uma árvore binária é composta por nós que tem filhos à esquerda e à direita. Todo nó tem um filho esquerdo e um filho direito e esses filhos também têm um filho esquerda e um filho direito assim subsequentemente formando uma árvore. Talvez seja a estrutura mais importante de ser estudada
![[bst-completa.png]]

- O primeiro nó é chamado de raiz
- Cada filho da raiz é uma sub-árvore da árvore principal, tendo sua raiz própria e sub-árvores também.
- Uma folha é um nó que não tem filho, tendo seu filho esquerdo nulo e o direito também
- Toda árvore tem uma altura ou profundidade, sendo a maior distância da raiz até um nó folha
- Note que um nó da Árvore da Binária é totalmente diferente do nó de uma Lista Encadeada
Recursividade é muito importante para a árvore binária
## Estratégias de travessia
Para percorrer uma árvore binária existem várias maneiras porém, todas elas passam obrigatoriamente por todos os nós da árvore
Nesse passo é onde a recursividade mais importa, sendo ela o principal agente para percorrer a Árvore

### Pré-ordem
Um algoritmo que tem os seguintes passos:
1. Visitar a raiz da árvore, **imagine que isso é um print()**
2. Percorra a subárvore da esquerda, **aqui é onde começa a recursão**
3. Percorra a subárvore direita
![[Captura de Tela 2024-10-11 às 21.10.46.png]]

### In-ordem
Um algoritmo que tem os seguintes passos:
1. Percorra a subárvore esquerda
2. Visite a raiz da árvore
3. Percorra a subárvore direita
**Esse algoritmo é igual mostrar os números de forma crescente**
![[Captura de Tela 2024-10-11 às 21.20.21.png]]

### Pós-ordem
Um algoritmo que tem os seguintes passos:
1. Percorra a subárvore esquerda
2. Percorra a subárvore direita
3. Visite a raíz da árvore
![[Captura de Tela 2024-10-11 às 21.25.23.png]]

Algoritmos que implementam árvores binárias, geralmente, são divididos em duas etapas. A primeira consiste em construir a árvore e a segunda em percorrer a árvore.
## Estratégia de ordenação
Para se criar uma Árvore Binária de Busca é primordial saber como construir ela corretamente. Construir de forma errada surtirá em erros nos algoritmos de busca
### Inserir nós
1. Se a árvore estiver vazia, crie uma árvore com um único nó contendo o valor de $N$
2. Se o número $N$ for maior ou igual ao valor armazenado no nó raiz, então repita o procedimento sobre a subárvore direita do nó raiz
3. Se o número $N$ for menor que o valor armazenado sobre o nó, então repita o procedimento sobre a subárvore esquerda do nó raiz
#### Note: Valores menores sempre estarão à esquerda do nó raiz, eliminando a direita inteira da árvore. Caso erre na inserção de algum valor é necessário começar do zero a criação da árvore.

Digamos que queremos criar uma Árvore Binária de Busca com tais valores: 
$14, 15, 4, 9, 7, 18, 3, 5, 16, 4, 20, 17, 9, 14, 5$
Para a criação com esses valores, seguindo a lógica proposta, o resultado será o seguinte: 

![[Captura de Tela 2024-10-11 às 21.35.55.png]]

## Remoção de um nó
Nessa parte temos algumas alternativas para remover nós, todos os elementos removidos são substituídos por ```null```
### Removendo um nó externo
Talvez o modo mais fácil de remover um nó
![[Pasted image 20241011214047.png]]
### Removendo um nó interno
O modo mais complicado de remover um nó, pois você deve realocar os filhos do nó removido seguindo a lógica de inserção
![[Pasted image 20241011214458.png]]
Para esse caso temos duas estratégias para deixar menos trabalhoso:
- O maior valor da esquerda do nó removido é colocado no lugar
- O menor valor da direita do nó removido é colocado no lugar
Em alguns casos é mais fácil não remover o nó e simplesmente atualizar sua informação
Para remoção é necessário também usar recursividade 
## Calcular a altura de uma árvore
Para calcular a altura de uma árvore é necessário conhecer o maior caminho de $X$ até um de seus descendentes. A altura de um nó $X$ somente pode ser calculada após a visita a todos os descendentes de $X$. Sendo a altura de um nó folha é $0$
Ir em todos os filhos e depois ir subindo aumentando o valor da altura, calculando de baixo para cima 
Muito parecido com o algoritmo de travessia do pós-ordem
Caso um nó tenha um filho null (não tenha filho), é atribuído o valor -1 
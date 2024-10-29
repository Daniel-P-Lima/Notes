![[Modelagem]]
- Forma **testada** ou **documentada** de alcançar um objetivo qualquer
- Descrição de uma solução genérica que deve ser adaptada de acordo com o contexto em que o problema se manifesta 
- Usar a solução inúmeras vezes sem nunca fazê-la da mesma forma duas vezes
# Por que utilizar?
- Facilita a comunicação, compreensão e documentação
- Soluções testadas e bem documentadas 
- **Aprender a programar bem com orientação a objetos**
- **Desenvolver software de melhor qualidade** 
# Elementos de um Padrão
1. **Nome**
2. **Problema**
	1. Quando aplicar o padrão, em que condições?
3. **Solução**
	1. Descrição abstrata de um problema e como usar os elementos disponíveis (classes e objetos) para solucioná-lo
4. **Consequências** 
	1. Custos e benefícios de se aplicar o padrão
	2. Impacto na flexibilidade, extensibilidade, portabilidade e eficiência do sistema
# Forma de classificação
- Há várias formas de classificar os padrões. Gamma et al [1] os classifica de duas formas
	- Por propósito: (1) criação de classes e objetos, (2) alteração da estrutura de um programa, (3) controle do seu comportamento
	- Por escopo: classe ou objeto
![[Captura de Tela 2024-10-28 às 10.34.40.png]]
## 1. Criação 

### Singleton
- Obriga uma classe gerar apenas uma implementação, apenas um objeto da classe
### Prototype 
- Clonagem de projetos, só é colocado valores diferentes e valores default não são alterados
- Por exemplo o modelo de um carro, onde um carro de 2012 é clonado e alterado apenas os valores específicos para 2013
## 2. Estrutura
### Adaptador
- Ajustar a conexão, um adaptador entre conexões 
- Como utilizar um sistema novo com um sistema legado, adaptando métodos do sistema legado
### Decorador
- Uma pilha de objetos, um objeto montado a partir de outros objetos
### Façade
- Como uma fachada, uma interface onde o usuário só enxerga os métodos "públicos", não sabem como funciona por trás dela
## 3. Comportamento
- O código da implementação
### Método template
- O método que implementa outros métodos, o algoritmo é o mesmo e partes são injetadas automaticamente
### Cadeia de responsabilidade
- Um objeto que chama um método, que chama outro método e assim por diante. Segurança de objetos bem criados
### Comand
- Uma classe que tem vários métodos, sendo possível encapsular cada método em outra classe chamada _comand_, criando um objeto de cada método
- Aplicação segura sem banco de dados, escrevendo objetos em disco 
### Iterador
- Iteradores de java, para ter acesso a itens privados
- Como getters e setters em java
### Mediador
- Meio de campo entre os objetos, para eles se encontrarem
### Memento
- Por exemplo o ctrl-z
### Observer
### State
- Implementar uma máquina de estado, um padrão apenas para ela
### Strategy
- Uma estratégia para lidar com problemas, como uma estratégia de ordenação
- Vários algoritmos, todos dentro da estratégia
### Visitor
- Métodos que tem acessos a todos os dados privados de outra classe, como um amigo que recebe a chave da casa para poder ter acesso de tudo
- Método ```friend() em c++```
---

# Interface 
- Por exemplo de implementação de interface como, o ```Implements``` em java 
- Uma interface sem métodos nada mais é do que uma interface de marcação
```java
writeObject(a1, " ")
a1 = readObject(" ")
```
## Composição
- Representar um objeto composto por outros objetos
- **Aplicar em uma árvore de objetos**, com acesso uniforme
- Como uma pasta raiz onde dentro tem mais pastas e essas pastas tem outras passas dentro que possuem arquivos
![[Captura de Tela 2024-10-28 às 11.30.24.png]]

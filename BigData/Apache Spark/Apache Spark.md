![[BigData]]
- Uma engine multi-linguagem para execução de data engineering, data science e machine learning em uma máquina ou cluster
- Processamento para fluxo de dados, processa cada dado por si só, considerando um novo processamento somente os novos dados sendo utilizados
- Escrito em Scala
- Arquitetura Master-Slave 
- Integração HDFS

## Propriedades do Apache Spark
### Velocidade
Processamento de data pode ser 100 vezes mais rápido em memória, e 10 vezes mais rápido quando em disco
### Suporte Multi-Linguagem
Possibilidade de programar em Java, R, Scala ou Python
### Análises Avançadas
Spark não só suporta _Map_ e _Reduce_ mas também _SQL queries_, fluxo de dados, machine learning e algoritmos orientados a grafos
### Tolerância a falha
 Grafos acíclicos e direcionais feitos para tolerar erros com a replicação de dados, com perda zero
Caso haja um erro em algum nó, os resultados podem ser obtidos executando novamente os passos pelo DAG já existente
O R de RDD é a tolerância a erros, resilient
### Transformação
Geram RDDS, dataset intermediários, exemplo: map
### Ação
Geram resultados de saídas, exemplo: count
### Lazy Evaluation
O Spark não faz nenhuma transformação imediatamente, só vai ser executada quando uma ação for chamada terá a sequência de execução das transformações
### Não armazena arquivos intermediários
Os arquivos intermediários gerados não são armazenados na memória, armazenando em cache para ser utilizado no processamento da próxima interação
### Arquitetura Mestre-Escravo
Executado em apenas um master mas possível ter múltiplos slaves
Slaves servem para executar as transformações
Função _parallelize_ cria um novo RDD
#### Driver Program 
Executa a aplicação, cria o SparkContext, coordena a aplicação
#### Cluster Manager 
Gerenciamento de recursos, ligado a aplicação (main), possibilidade de rodar em um grande conjunto de nós
#### Worker Node
Nó escravo que estará rodando os códigos
Executor: armazena as tarefas e executa as tarefas (toda aplicação deve ter)
Task: unidade de trabalho ligada ao executor
**Paralismo intranode:** dentro do node temos paralelismo com vários blocos do arquivo principal
**Paralelismo internode:** o paralelismo entre diferentes nós

## 1º Criação do arquivo no Colab
Baixar os pacotes no novo notebook do colab
```!pip install findpark pyspark```
### 2º Criar o spark context
```
import findspark
findspark.find()
from pyspark import SparkConf, SparkContext

# Criação do contexto na main
if __name__ == "__main__":
conf = SparkConf().setAppName("WordCount").setMaster("local[*]")
context = SparkContext.getOrCreate(conf=conf)
```
### 3º Criar o RDD inicial
```rdd = context.textFile("bible.txt")```

### 4º Aplicar as transformações
### 5º Executar as operações
```print(rdd.count())``` Mostra quantas linhas tem no arquivo - uma ação

### 6º Mostrar os resultados
### 7º Código completo

```
import findspark
import re
findspark.find()
from pyspark import SparkConf, SparkContext
import os
import shutil
def delete(path:str):
if os.path.exists(path):
shutil.rmtree(path)
path = "Word Count"
delete(path)
if __name__ == "__main__":
conf = SparkConf().setAppName("WordCount").setMaster("local[*]")
context = SparkContext.getOrCreate(conf=conf)
rdd = context.textFile("bible.txt")
rdd_words = rdd.flatMap(lambda line: re.findall("[A-Za-z//-]+", line.upper())) # Uma entrada várias saídas
rdd_map = rdd_words.map(lambda word: (word, 1)) # Uma entrada uma saída
rdd_reduce = rdd_map.reduceByKey(lambda x,y: x+y) # Executa de forma recursiva
rdd_reduce.saveAsTextFile("Word Count")
```
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
## RDD
### Transformação
Geram RDDS, dataset intermediários, exemplo: map
#### Map - Uma entrada e uma saída 
```
# MAP

rdd_map = sc.parallelize(["Antonio", "João", "Ana", "Maria", "José"]) # Cria o dataset

res = rdd_map.map(lambda x: x.upper()) # Converteu tudo para maiúsculo

res.take(6)
```
#### FlatMap - Uma entrada e várias saídas
```
#FLATMAP

rdd_map = sc.parallelize(["Antonio", "João", "Ana", "Maria", "José"]) # Cria o dataset

res = rdd_map.flatMap(lambda x: list(x.upper())) # Separa por letras

res.take(7)
```
#### Filter - Filtragem
```
# FILTER (precisa ter uma condição)

rdd_airports = sc.textFile("airports.csv")

rdd_usa = rdd_airports.filter(lambda line: line.split(",")[3] == "\"United States\"") # Filtra apenas os USA

rdd_usa.take(5)
```
#### Sample - Amostragem
```
# SAMPLE

rdd_numbers = sc.parallelize(range(1, 1001))

rdd_sample = rdd_numbers.sample(withReplacement=False, fraction=0.01)

print(rdd_sample.collect())
```
#### Distinct - Dados distintos 
```

```
#### Union - União
#### Intersect - Intersecção
#### Subtract - Remove as intersecções
#### Cartesian Product - Todas as relações possíveis de dois RDDS

### Ação
Geram resultados de saídas, exemplo: count
#### Count
```
# COUNT

  

rdd_bible = sc.textFile("bible.txt")

rdd_words = rdd_bible.flatMap(lambda line: line.split(" ")) # Separa as palavras

rdd_words.count() # Conta as palavras
```
#### Count By Value
Quantos valores distintos aparece
```
rdd_bible = sc.textFile("bible.txt")

rdd_chars = rdd_bible.flatMap(lambda line: list(line.upper().replace(" ", " "))) # Separa as letras

rdd_chars.countByValue()
```
#### Take
Retorna quantos elementos escolher
#### Reduce
Recebe um input de dois itens de um RDD e retorna um elemento do mesmo tipo
Considera os dois elementos como um só, diferente do reduce by key
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

### 1º Criação do arquivo no Colab
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
## PairRDD
Onde recebe o formato <key><valor>, diferente do RDD que recebe apenas um <valor>
Com a função map no RDD podemos retornar a lista com tuplas
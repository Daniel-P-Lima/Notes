![[BigData]]
1. **Job 1** - Conta a quantidade de meteoros por classificação e calcula o total geral de meteoros.
2. **Job 2** - Utiliza a saída do primeiro job para calcular o percentual de meteoros por classificação, baseado no total calculado no Job 1.
### **Job 1: Contagem de Meteoros por Classificação**

O primeiro Job processa os dados de entrada e conta quantas vezes cada classificação de meteoros aparece. Ele também calcula o total geral de meteoros. A saída desse Job é utilizada como entrada para o segundo Job.

- **Mapper (`RecClassMapper`)**: Lê o arquivo de entrada linha por linha, identifica a classificação do meteoro e emite a classificação com um valor de `1`.
- **Reducer (`RecClassReducer`)**: Soma todas as ocorrências para cada classificação e também calcula o total geral de meteoros. O total é escrito no final do processamento.

### **Job 2: Cálculo do Percentual de Meteoros por Classificação**

O segundo Job lê a saída do Job 1 e calcula o percentual de meteoros de cada classificação, dividindo a quantidade de cada classificação pelo total geral de meteoros.

- **Mapper (`PercentMapper`)**: Lê a saída do Job 1 e emite a classificação e a quantidade associada.
- **Reducer (`PercentReducer`)**: Calcula o percentual para cada classificação com base no total de meteoros.
### **RecClassMapper.java**
Responsável por mapear as classificações dos meteoros no primeiro Job.

**Código Principal:**
```java
public static class RecClassMapper extends Mapper<LongWritable, Text, Text, IntWritable> {
    private static final IntWritable one = new IntWritable(1);

    public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
        String line = value.toString();
        if (line.startsWith("name")) {
            return; // Ignora a linha do cabeçalho
        }
        String[] columns = line.split(",(?=(?:[^\"]*\"[^\"]*\")*[^\"]*$)");
        if (columns.length >= 3 && !columns[3].isEmpty()) {
            String recClass = columns[3].trim();
            context.write(new Text(recClass), one);
        }
    }
}

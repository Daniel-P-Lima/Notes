![[Lógica]]
- Linguagem funcional
- Variável global não existe
- Interatividade não existe, é usado recursividade
``` haskell 
add :: Int -> Int -> Int
add x y = x + y
```

> [!NOTE]
> 
> **Add** = assinatura da função
> **::**  = é do tipo, add é do tipo int 
Recebe um inteiro, recebe um inteiro e devolve inteiro 
Nome da função, argumentos da função, corpo da função
## Não existe laço
**É usado recursão**
```haskell
factorial :: Integer -> Integer
factorial 0 = 1 // Definição de um caso base
factorial n = n * factorial (n - 1)
```

## Mônade
- Interface, tudo que está do lado do IO é abstraído
```haskell 
main :: IO()
main = do
    putStrLn "Hello World"
```
## $ É o símbolo de aplicação 
- O símbolo de *$* funciona como um pipe, ele simboliza a ==aplicação ==
```haskell
print $ add 3 4 
```

## Função fatorial
- Usando a recursividade e caso base 
```haskell
factorial :: Integer -> Integer
factorial 0 = 1
factorial n = n * factorial (n - 1)

main :: IO()
main = do
    print $ factorial(5)
```

## Listas 
- Criação de listas, a função não recebe parâmetros mas define os valores que vai devolver
```haskell
firstFive :: [Int] -- Está função sempre devolve uma lista de inteiros
firstFive = [1..5]
```

## Guard
- Operador para desvio de função, funcionando parecido como um switch
- ==Pipe (|) é interpretado com "OU"==
## Local Bindings
- Criar funções que só existem dentro de outras funções
- Evitando o efeito colateral
	- Definindo uma função circleArea dentro da função cylinderVolume
```haskell
cylinderVolume :: Float -> Float -> Float
cylinderVolume r h = circleArea * h
	where circleArea = pi * r * r 
```
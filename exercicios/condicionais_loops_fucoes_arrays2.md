# Exercícios Preparatórios: Arrays Unidimensionais em C++

## Objetivo
Este conjunto de exercícios visa desenvolver as habilidades de manipulação de arrays unidimensionais, loops, condicionais, e operações lógicas e aritméticas em C++. A implementação deve ser feita através de funções.

## Exercícios

1. **Gerador de Números Aleatórios entre [a, b]** ⭐⭐
   Crie uma função que gere um número aleatório entre dois valores inteiros a e b (incluindo números negativos).
   
   **Conhecimentos necessários:** Funções de biblioteca, manipulação de intervalos de valores.
   
   **Dica de implementação:** Use uma função de biblioteca para gerar o número aleatório e assegure-se de que a função aceita valores negativos.

   **Exemplo:**
   ```
   a = -5, b = 5
   Número Aleatório: -2
   ```

   **Tarefa Adicional:** Utilize essa função para criar um vetor de N elementos aleatórios (onde N é definido pelo usuário) e use-o para testar os exercícios subsequentes.

2. **Rearranjo dos Números Positivos e Negativos** ⭐⭐⭐
   Implemente uma função que reorganize um array de modo que todos os números negativos venham antes dos positivos, mantendo a ordem relativa original.

   **Conhecimentos necessários:** Manipulação de arrays, ordenação condicional.

   **Dica de implementação:** Utilize dois arrays auxiliares: um para números negativos e outro para positivos. Combine-os no array original ao final.

   **Exemplo:**
   ```
   Entrada: [-5, 2, -3, 4, -1]
   Saída:   [-5, -3, -1, 2, 4]
   ```

3. **Verificação de Array Palíndromo** ⭐⭐
   Crie uma função que verifique se os elementos de um array formam um palíndromo.

   **Conhecimentos necessários:** Manipulação de índices de arrays, comparação simétrica de elementos.

   **Dica de implementação:** Compare os elementos do início e do final do array, movendo-se em direção ao centro.

   **Exemplo:**
   ```
   Entrada:  [1, 2, 3, 2, 1]
   Resultado: Verdadeiro
   ```

4. **Sequência Longa de Elementos Crescentes** ⭐⭐⭐
   Implemente uma função que encontre a maior sequência crescente de elementos consecutivos no array.

   **Conhecimentos necessários:** Loops, condicionais, tracking de sequências.

   **Dica de implementação:** Percorra o array comparando cada elemento com o próximo para identificar sequências crescentes. Mantenha o controle do comprimento da maior sequência encontrada.

   **Exemplo:**
   ```
   Entrada: [1, 2, 1, 2, 3, 4, 1]
   Saída:   Maior sequência crescente: 2, 3, 4 (comprimento: 3)
   ```

5. **Contagem de Números Divisíveis por 3** ⭐⭐
   Escreva uma função que conte quantos elementos de um array são divisíveis por 3.

   **Conhecimentos necessários:** Loops, operador módulo (%), condicionais.

   **Dica de implementação:** Use um loop para percorrer o array e o operador `%` para identificar os números divisíveis por 3.

   **Exemplo:**
   ```
   Entrada:  [3, 6, 7, 10, 12]
   Resultado: Números divisíveis por 3: 3, 6, 12 (Total: 3)
   ```

6. **Multiplicação de Arrays** ⭐⭐⭐
   Crie uma função que multiplique os elementos correspondentes de dois arrays e armazene o resultado em um novo array.

   **Conhecimentos necessários:** Manipulação de múltiplos arrays, operações aritméticas.

   **Dica de implementação:** Use um loop para multiplicar os elementos nas mesmas posições dos dois arrays e armazene os resultados em um novo array.

   **Exemplo:**
   ```
   Array 1:  [2, 4, 6]
   Array 2:  [1, 3, 5]
   Resultado: [2, 12, 30]
   ```

7. **Contagem de Elementos Maiores que a Média** ⭐⭐⭐
   Implemente uma função que conte quantos elementos de um array são maiores que a média de seus elementos.

   **Conhecimentos necessários:** Cálculo de média, loops, condicionais.

   **Dica de implementação:** Primeiro, calcule a média dos elementos do array, depois conte quantos elementos são maiores que essa média.

   **Exemplo:**
   ```
   Entrada:  [10, 15, 20, 30]
   Média:    18.75
   Resultado: 2 elementos maiores que a média (20, 30)
   ```

8. **Substituição de Elementos** ⭐⭐⭐
   Escreva uma função que substitua todos os elementos negativos de um array por 0.

   **Conhecimentos necessários:** Loops, condicionais, manipulação de arrays.

   **Dica de implementação:** Use um loop para percorrer o array e uma condicional para verificar se o número é negativo. Se for, substitua-o por 0.

   **Exemplo:**
   ```
   Entrada:  [-1, 2, -3, 4]
   Resultado: [0, 2, 0, 4]
   ```

9. **Diferença de Elementos Adjacentes** ⭐⭐⭐
   Crie uma função que calcule a diferença entre os elementos adjacentes de um array.

   **Conhecimentos necessários:** Manipulação de índices de arrays, operações aritméticas.

   **Dica de implementação:** Subtraia cada elemento do anterior e armazene o resultado em um novo array.

   **Exemplo:**
   ```
   Entrada:  [5, 10, 15, 20]
   Resultado: [5, 5, 5]
   ```

10. **Contagem de Números Primos** ⭐⭐⭐⭐
    Implemente uma função que conte quantos números primos existem em um array.

    **Conhecimentos necessários:** Funções auxiliares, verificação de primalidade, loops.

    **Dica de implementação:** Implemente uma função auxiliar para verificar se um número é primo e use-a para contar os números primos no array.

    **Exemplo:**
    ```
    Entrada:  [2, 3, 4, 5, 6]
    Resultado: 3 números primos (2, 3, 5)
    ```

Lembre-se de pensar sobre casos de borda e a testar suas soluções com diferentes inputs.

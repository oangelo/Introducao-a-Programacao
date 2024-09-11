# Exercícios Preparatórios: Arrays 1D em C++

## Objetivo
Este conjunto de exercícios visa preparar os alunos para a prova, focando em arrays unidimensionais e sua aplicação com condicionais, loops e funções básicas. Os exercícios estão organizados em ordem crescente de dificuldade.

## Exercícios

1. **Soma dos Elementos** ⭐
   Escreva uma função que receba um array de inteiros e seu tamanho, e retorne a soma de todos os elementos.
   
   **Conhecimentos necessários:** Declaração de funções, parâmetros, loops (for ou while), operações aritméticas.
   
   **Dica de implementação:** Use um loop para percorrer o array e uma variável para acumular a soma.

2. **Maior Elemento** ⭐
   Crie uma função que receba um array de inteiros e seu tamanho, e retorne o maior elemento do array.
   
   **Conhecimentos necessários:** Declaração de funções, loops, condicionais (if).
   
   **Dica de implementação:** Inicialize uma variável com o primeiro elemento e compare com os demais em um loop.

3. **Ordenação Simples** ⭐⭐⭐
   Implemente uma função que ordene um array de inteiros usando o seguinte método: para cada posição do array, encontre o menor elemento entre ela e o final do array, e troque-os.

   **Conhecimentos necessários:** Loops aninhados, condicionais, troca de elementos em array.

   **Dica de implementação:** 
   - Use um loop externo para percorrer o array da posição 0 até o penúltimo elemento.
   - Para cada posição i do loop externo, use um loop interno para encontrar o menor elemento entre as posições i+1 e o final do array.
   - Se encontrar um elemento menor, troque-o com o elemento na posição i.

   **Explicação detalhada:**
   Considere o array: [5, 2, 8, 12, 1, 6]
   
   1ª iteração: 
   [5, 2, 8, 12, 1, 6] → [1, 2, 8, 12, 5, 6] (1 é o menor, troca com 5)
   
   2ª iteração:
   [1, 2, 8, 12, 5, 6] → [1, 2, 8, 12, 5, 6] (2 já é o menor)
   
   3ª iteração:
   [1, 2, 8, 12, 5, 6] → [1, 2, 5, 12, 8, 6] (5 é o menor após 8, troca)
   
   E assim por diante até o array estar ordenado.

4. **Contagem de Pares e Ímpares** ⭐⭐
   Implemente uma função que receba um array de inteiros e seu tamanho, e imprima quantos números pares e ímpares existem no array.
   
   **Conhecimentos necessários:** Loops, condicionais, operador módulo (%).
   
   **Dica de implementação:** Use duas variáveis contadoras e incremente-as conforme a condição de par ou ímpar.

5. **Média dos Elementos** ⭐⭐
   Escreva um programa que leia 10 números reais do usuário, armazene-os em um array, e então calcule e imprima a média desses números.
   
   **Conhecimentos necessários:** Arrays, loops, entrada/saída, operações com ponto flutuante.
   
   **Dica de implementação:** Use um loop para ler os valores, outro para somá-los, e divida pelo tamanho do array.

6. **Inversão de Array** ⭐⭐
   Crie uma função que receba um array de inteiros e seu tamanho, e inverta a ordem dos elementos no próprio array.
   
   **Conhecimentos necessários:** Manipulação de arrays, loops, troca de valores.
   
   **Dica de implementação:** Use dois índices (início e fim) e troque os elementos até que os índices se encontrem.

   **Explicação detalhada:**
   Considere o array: [1, 2, 3, 4, 5]
   
   1ª troca: [5, 2, 3, 4, 1]
   2ª troca: [5, 4, 3, 2, 1]
   
   O processo para quando os índices se cruzam no meio do array.

7. **Remoção de Duplicatas** ⭐⭐⭐
   Implemente uma função que receba um array de inteiros e seu tamanho, e remova todos os elementos duplicados, retornando o novo tamanho do array.
   
   **Conhecimentos necessários:** Loops aninhados, condicionais, manipulação de arrays.
   
   **Dica de implementação:** Compare cada elemento com os seguintes, movendo os elementos únicos para o início do array.

8. **Rotação de Array** ⭐⭐⭐
   Escreva uma função que receba um array de inteiros, seu tamanho e um número K, e rotacione o array K posições para a direita.
   
   **Conhecimentos necessários:** Manipulação de arrays, loops, operador módulo.
   
   **Dica de implementação:** Use uma função auxiliar para inverter partes do array e então o array inteiro.

   **Explicação detalhada:**
   Para rotacionar [1, 2, 3, 4, 5] 2 posições à direita:
   1. Inverta todo o array: [5, 4, 3, 2, 1]
   2. Inverta os primeiros K elementos: [4, 5, 3, 2, 1]
   3. Inverta os N-K elementos restantes: [4, 5, 1, 2, 3]

9. **Sequência Crescente** ⭐⭐⭐
   Crie um programa que leia uma sequência de números inteiros do usuário até que seja digitado -1, armazene esses números em um array, e então verifique se a sequência está em ordem crescente.
   
   **Conhecimentos necessários:** Entrada/saída, arrays dinâmicos ou com tamanho máximo predefinido, loops, condicionais.
   
   **Dica de implementação:** Compare cada elemento com o anterior enquanto lê a sequência.

10. **Moda do Array** ⭐⭐⭐
    Implemente uma função que receba um array de inteiros e seu tamanho, e retorne a moda (o elemento que aparece com mais frequência) do array.
   
    **Conhecimentos necessários:** Arrays, loops aninhados, condicionais.
   
    **Dica de implementação:** Use um loop para contar as ocorrências de cada elemento e outro para encontrar o de maior contagem.

11. **Subarray de Soma Máxima** ⭐⭐⭐⭐
    Escreva uma função que encontre o subarray contíguo com a maior soma em um array de inteiros e retorne essa soma.
    
    **Conhecimentos necessários:** Arrays, loops, compreensão de subarrays.
    
    **Explicação detalhada e dica de implementação:** 
    Este problema pode ser resolvido usando o algoritmo de Kadane simplificado. A ideia é manter duas variáveis: 
    - `soma_atual`: a soma do subarray atual
    - `soma_maxima`: a maior soma encontrada até agora

    Percorra o array da esquerda para a direita:
    1. Para cada elemento, decida se é melhor:
       a) Incluí-lo na soma atual
       b) Começar um novo subarray a partir dele
    2. Atualize `soma_maxima` se `soma_atual` for maior.

    Exemplo:
    Array: [-2, 1, -3, 4, -1, 2, 1, -5, 4]

    Passo a passo:
    1. -2: soma_atual = -2, soma_maxima = -2
    2. 1:  soma_atual = 1,  soma_maxima = 1  (começar novo subarray)
    3. -3: soma_atual = -2, soma_maxima = 1
    4. 4:  soma_atual = 4,  soma_maxima = 4  (começar novo subarray)
    5. -1: soma_atual = 3,  soma_maxima = 4
    6. 2:  soma_atual = 5,  soma_maxima = 5
    7. 1:  soma_atual = 6,  soma_maxima = 6
    8. -5: soma_atual = 1,  soma_maxima = 6
    9. 4:  soma_atual = 5,  soma_maxima = 6

    A soma máxima é 6, correspondente ao subarray [4, -1, 2, 1].

12. **Intercalação de Arrays** ⭐⭐⭐
    Crie uma função que receba dois arrays ordenados e seus tamanhos, e retorne um novo array que seja a intercalação ordenada dos dois arrays de entrada.
   
    **Conhecimentos necessários:** Manipulação de múltiplos arrays, loops, condicionais.
   
    **Dica de implementação:** Use três índices (um para cada array de entrada e um para o array resultante) e compare os elementos.

13. **Compressão de Array** ⭐⭐⭐⭐
    Implemente uma função que "comprima" um array de caracteres substituindo sequências de caracteres repetidos por um número seguido do caractere.
    
    **Conhecimentos necessários:** Manipulação de strings como arrays de char, loops, condicionais.
    
    **Dica de implementação:** Percorra o array contando caracteres repetidos e substituindo-os pela contagem e o caractere.

    **Explicação detalhada:**
    Para o array: ['a', 'a', 'b', 'b', 'c', 'c', 'c']
    Resultado: ['2', 'a', '2', 'b', '3', 'c']

14. **Elementos Únicos** ⭐⭐⭐
    Escreva um programa que leia uma sequência de números inteiros do usuário, armazene em um array, e então imprima apenas os números que aparecem uma única vez no array.
    
    **Conhecimentos necessários:** Arrays, loops aninhados, condicionais.
    
    **Dica de implementação:** Use um loop para contar as ocorrências de cada elemento e outro para imprimir os que têm contagem 1.

15. **Histograma** ⭐⭐⭐⭐
    Crie uma função que receba um array de inteiros (representando dados) e imprima um histograma usando asteriscos para representar a frequência de cada número.
    
    **Conhecimentos necessários:** Arrays, loops aninhados, saída formatada.
    
    **Dica de implementação:** Encontre o valor máximo para determinar a escala, então use loops para imprimir os asteriscos.

    **Explicação detalhada:**
    Para o array: [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
    
    Saída:
    ```
    1: *
    2: **
    3: ***
    4: ****
    ```

16. **Mediana** ⭐⭐⭐⭐
    Implemente uma função que calcule a mediana de um array de números reais não ordenados.
    
    **Conhecimentos necessários:** Arrays, ordenação básica (pode usar a ordenação simples do exercício 3), operações com ponto flutuante.
    
    **Dica de implementação:** Ordene o array primeiro, então retorne o elemento do meio (ou a média dos dois do meio se o tamanho for par).

Lembre-se de pensar sobre casos de borda e a testar suas soluções com diferentes inputs.

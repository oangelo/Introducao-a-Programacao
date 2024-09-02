# Exercícios Básicos: Arrays em C++

## Importância dos Exercícios

[O conteúdo desta seção permanece inalterado]

## Lista de Exercícios

### 1. Declaração e Inicialização ⭐
**Objetivo:** Declare um array de inteiros com 5 elementos e inicialize-o com os valores 10, 20, 30, 40 e 50.

**Importância:** Este exercício ajuda a praticar a sintaxe básica de declaração e inicialização de arrays, fundamentais para qualquer trabalho com arrays em C++.

**Dica de implementação:** Use a sintaxe de inicialização de array com chaves {}. Declare o tipo do array (int), seguido do nome e do tamanho entre colchetes. Em seguida, use chaves para listar os valores iniciais.

**Exemplo:**
| Índice | 0  | 1  | 2  | 3  | 4  |
|--------|----|----|----|----|----| 
| Valor  | 10 | 20 | 30 | 40 | 50 |

### 2. Acesso e Impressão ⭐
**Objetivo:** Crie um array de 7 inteiros com os números de 1 a 7. Imprima o primeiro e o último elemento do array.

**Importância:** Praticar o acesso a elementos específicos de um array é crucial para manipular dados armazenados em arrays.

**Dica de implementação:** Lembre-se que os índices de array em C++ começam em 0. Para acessar o primeiro elemento, use o índice 0. Para o último elemento de um array de tamanho n, use o índice n-1.

**Exemplo:**
| Índice | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|--------|---|---|---|---|---|---|---|
| Valor  | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

Primeiro elemento: array[0] = 1
Último elemento: array[6] = 7

### 3. Modificação de Elementos ⭐⭐
**Objetivo:** Crie um array de 5 números inteiros. Peça ao usuário para inserir 5 números e armazene-os no array. Em seguida, multiplique cada elemento por 2 e imprima o array resultante.

**Importância:** Este exercício pratica a entrada de dados do usuário, armazenamento em arrays e manipulação simples de elementos.

**Dica de implementação:** Use um loop para ler os números do usuário e armazená-los no array. Em seguida, use outro loop para multiplicar cada elemento por 2 e imprimi-lo.

### 4. Soma de Elementos ⭐⭐
**Objetivo:** Escreva um programa que some todos os elementos de um array de 10 inteiros e imprima o resultado.

**Importância:** Introduz a iteração sobre arrays e a realização de operações cumulativas, conceitos fundamentais em programação.

**Dica de implementação:** Inicialize uma variável soma com zero. Use um loop para percorrer o array, adicionando cada elemento à soma. Ao final do loop, a variável soma conterá a soma total.

**Exemplo:**
| Índice | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|--------|---|---|---|---|---|---|---|---|---|---|
| Valor  | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

Soma: 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10 = 55

### 5. Contagem de Elementos Pares ⭐⭐
**Objetivo:** Crie um array de 8 números inteiros. Conte quantos números pares existem no array e imprima o resultado.

**Importância:** Este exercício combina iteração com tomada de decisão simples, habilidades essenciais na programação.

**Dica de implementação:** Inicialize um contador de pares com zero. Percorra o array com um loop, verificando cada elemento. Se o elemento for par (divisível por 2 sem resto), incremente o contador.

### 6. Encontrar o Maior e o Menor ⭐⭐⭐
**Objetivo:** Encontre e imprima o maior e o menor elemento em um array de 10 números inteiros.

**Importância:** Ajuda a praticar a lógica de comparação e a manter o controle de valores enquanto itera sobre um array.

**Dica de implementação:** Inicialize as variáveis 'maior' e 'menor' com o primeiro elemento do array. Percorra o array comparando cada elemento com 'maior' e 'menor', atualizando-os quando necessário.

### 7. Inversão de Array ⭐⭐⭐
**Objetivo:** Crie um array de 6 inteiros. Inverta a ordem dos elementos no array e imprima o resultado.

**Importância:** Este exercício desafia você a pensar sobre manipulação de índices e trocas de elementos, uma operação comum em muitos algoritmos.

**Dica de implementação:** Use dois índices, um começando do início e outro do fim do array. Troque os elementos nestes índices e mova os índices em direção ao centro do array. Pare quando os índices se cruzarem.

**Exemplo:**
Antes da inversão:
| Índice | 0 | 1 | 2 | 3 | 4 | 5 |
|--------|---|---|---|---|---|---|
| Valor  | 1 | 2 | 3 | 4 | 5 | 6 |

Depois da inversão:
| Índice | 0 | 1 | 2 | 3 | 4 | 5 |
|--------|---|---|---|---|---|---|
| Valor  | 6 | 5 | 4 | 3 | 2 | 1 |

### 8. Média dos Elementos ⭐⭐
**Objetivo:** Calcule e imprima a média dos elementos em um array de 5 números de ponto flutuante.

**Importância:** Combina iteração, soma e divisão, introduzindo o conceito de operações com ponto flutuante em arrays.

**Dica de implementação:** Some todos os elementos do array e divida pelo número total de elementos (5 neste caso). Lembre-se de usar variáveis de ponto flutuante para a soma e a média.

### 9. Busca Linear ⭐⭐⭐
**Objetivo:** Peça ao usuário para inserir um número e verifique se esse número existe em um array predefinido de 10 elementos. Se existir, imprima a posição; caso contrário, informe que o número não foi encontrado.

**Importância:** Introduz o conceito básico de busca em arrays, uma operação fundamental em ciência da computação.

**Dica de implementação:** Use um loop para percorrer o array, comparando cada elemento com o número buscado. Se encontrar, imprima a posição e encerre a busca. Se o loop terminar sem encontrar o número, informe que não foi encontrado.

### 10. Concatenação de Arrays ⭐⭐⭐
**Objetivo:** Crie dois arrays de 3 elementos cada. Combine-os em um terceiro array que contenha todos os elementos dos dois arrays originais.

**Importância:** Este exercício pratica a manipulação de múltiplos arrays e a criação de um novo array baseado em arrays existentes.

**Dica de implementação:** Crie um novo array com tamanho igual à soma dos tamanhos dos dois arrays originais. Copie os elementos do primeiro array para o início do novo array, e em seguida, copie os elementos do segundo array para as posições restantes.

**Exemplo:**
Array 1: [1, 2, 3]
Array 2: [4, 5, 6]
Array Concatenado: [1, 2, 3, 4, 5, 6]

Lembre-se: A prática é essencial para o aprendizado! Comece pelos exercícios mais simples e vá progredindo. Não hesite em revisar conceitos ou pedir ajuda quando necessário. Boa sorte!

# Exercícios: Arrays Multidimensionais e Matrizes em C++

Antes de mergulhar nas soluções, lembre-se: a melhor maneira de aprender programação é fazendo por conta própria. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Declaração e Inicialização de Array 2D ⭐
**Objetivo:** Declare uma matriz 3x3 de inteiros e inicialize-a com os números de 1 a 9 em ordem crescente.

**Importância:** Este exercício ajuda a praticar a sintaxe básica de declaração e inicialização de arrays bidimensionais em C++.

**Dica de implementação:** Use chaves aninhadas para inicializar a matriz. Lembre-se que a matriz terá 3 linhas e 3 colunas.

**Exemplo:**
```
1 2 3
4 5 6
7 8 9
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int matriz[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Imprimindo a matriz
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```

</details>

### 2. Acesso e Impressão de Array 2D ⭐⭐
**Objetivo:** Crie uma matriz 4x4 de inteiros. Preencha-a com os números de 1 a 16. Imprima os elementos da diagonal principal.

**Importância:** Praticar o acesso a elementos específicos em uma matriz é crucial para manipulação de dados em arrays bidimensionais.

**Dica de implementação:** Use dois loops aninhados para preencher a matriz. Para imprimir a diagonal principal, os índices de linha e coluna serão iguais.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int matriz[4][4];
    int num = 1;

    // Preenchendo a matriz
    for (int i = 0; i < 4; i++) {
        for (int j = 0; j < 4; j++) {
            matriz[i][j] = num++;
        }
    }

    // Imprimindo os elementos da diagonal
    std::cout << "Elementos da diagonal: ";
    for (int i = 0; i < 4; i++) {
        std::cout << matriz[i][i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

</details>

### 3. Declaração e Inicialização de Array 3D ⭐⭐
**Objetivo:** Declare um array tridimensional 2x3x2 de inteiros e inicialize-o com valores de sua escolha.

**Importância:** Este exercício introduz a complexidade adicional de trabalhar com arrays tridimensionais.

**Dica de implementação:** Use chaves aninhadas em três níveis para inicializar o array 3D.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int array3D[2][3][2] = {
        {{1, 2}, {3, 4}, {5, 6}},
        {{7, 8}, {9, 10}, {11, 12}}
    };

    // Imprimindo o array 3D
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            for (int k = 0; k < 2; k++) {
                std::cout << array3D[i][j][k] << " ";
            }
            std::cout << std::endl;
        }
        std::cout << std::endl;
    }

    return 0;
}
```

</details>

### 4. Soma de Matrizes ⭐⭐⭐
**Objetivo:** Crie duas matrizes 3x3 de inteiros. Escreva uma função que some estas matrizes e retorne o resultado em uma terceira matriz.

**Importância:** Introduz operações básicas com matrizes, fundamentais em álgebra linear e muitas aplicações de engenharia.

**Dica de implementação:** Use três loops aninhados: dois para percorrer as linhas e colunas, e um terceiro para realizar a soma dos elementos correspondentes.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void somaMatrizes(int a[3][3], int b[3][3], int resultado[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            resultado[i][j] = a[i][j] + b[i][j];
        }
    }
}

void imprimeMatriz(int matriz[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    int matriz1[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int matriz2[3][3] = {{9, 8, 7}, {6, 5, 4}, {3, 2, 1}};
    int resultado[3][3];

    somaMatrizes(matriz1, matriz2, resultado);

    std::cout << "Resultado da soma das matrizes:" << std::endl;
    imprimeMatriz(resultado);

    return 0;
}
```

</details>

### 5. Multiplicação de Matriz por Escalar ⭐⭐
**Objetivo:** Crie uma matriz 3x4 de inteiros. Escreva uma função que multiplique cada elemento da matriz por um número escalar fornecido pelo usuário.

**Importância:** Este exercício pratica a manipulação de todos os elementos de uma matriz, uma operação comum em processamento de dados.

**Dica de implementação:** Use dois loops aninhados para percorrer a matriz. Multiplique cada elemento pelo escalar fornecido.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void multiplicaPorEscalar(int matriz[3][4], int escalar) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            matriz[i][j] *= escalar;
        }
    }
}

void imprimeMatriz(int matriz[3][4]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    int matriz[3][4] = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };

    int escalar;
    std::cout << "Digite um valor escalar: ";
    std::cin >> escalar;

    std::cout << "Matriz original:" << std::endl;
    imprimeMatriz(matriz);

    multiplicaPorEscalar(matriz, escalar);

    std::cout << "Matriz após multiplicação por escalar:" << std::endl;
    imprimeMatriz(matriz);

    return 0;
}
```

</details>

### 6. Transposta de uma Matriz ⭐⭐⭐
**Objetivo:** Escreva uma função que receba uma matriz como argumento e retorne sua transposta.

**Importância:** A transposição de matrizes é uma operação fundamental em álgebra linear e tem muitas aplicações práticas em engenharia.

**Dica de implementação:** Crie uma nova matriz onde as linhas da matriz original se tornam colunas e vice-versa. Cuidado com as dimensões da nova matriz.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void transpoeMatriz(int original[3][3], int transposta[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transposta[j][i] = original[i][j];
        }
    }
}

void imprimeMatriz(int matriz[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    int original[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int transposta[3][3];

    std::cout << "Matriz original:" << std::endl;
    imprimeMatriz(original);

    transpoeMatriz(original, transposta);

    std::cout << "Matriz transposta:" << std::endl;
    imprimeMatriz(transposta);

    return 0;
}
```

</details>

### 7. Multiplicação de Matrizes ⭐⭐⭐⭐
**Objetivo:** Implemente uma função que realize a multiplicação de duas matrizes compatíveis.

**Importância:** A multiplicação de matrizes é uma operação essencial em muitos campos da engenharia e ciência da computação.

**Dica de implementação:** Use três loops aninhados. Verifique se as dimensões das matrizes são compatíveis antes de realizar a multiplicação.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void multiplicaMatrizes(int a[3][2], int b[2][3], int resultado[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            resultado[i][j] = 0;
            for (int k = 0; k < 2; k++) {
                resultado[i][j] += a[i][k] * b[k][j];
            }
        }
    }
}

void imprimeMatriz(int matriz[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    int matriz1[3][2] = {{1, 2}, {3, 4}, {5, 6}};
    int matriz2[2][3] = {{7, 8, 9}, {10, 11, 12}};
    int resultado[3][3];

    multiplicaMatrizes(matriz1, matriz2, resultado);

    std::cout << "Resultado da multiplicação das matrizes:" << std::endl;
    imprimeMatriz(resultado);

    return 0;
}
```

</details>

### 8. Busca em Matriz ⭐⭐⭐
**Objetivo:** Escreva uma função que busque um valor específico em uma matriz 5x5 e retorne sua posição (linha e coluna) se encontrado.

**Importância:** Pratica a busca em estruturas de dados bidimensionais, uma habilidade importante para manipulação de dados em tabelas.

**Dica de implementação:** Use dois loops aninhados para percorrer a matriz. Quando encontrar o valor, retorne os índices atuais.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void buscaEmMatriz(int matriz[5][5], int alvo) {
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            if (matriz[i][j] == alvo) {
                std::cout << "Encontrado " << alvo << " na posição (" << i << ", " << j << ")" << std::endl;
                return;
            }
        }
    }
    std::cout << alvo << " não encontrado na matriz." << std::endl;
}

int main() {
    int matriz[5][5] = {
        {1, 2, 3, 4, 5},
        {6, 7, 8, 9, 10},
        {11, 12, 13, 14, 15},
        {16, 17, 18, 19, 20},
        {21, 22, 23, 24, 25}
    };

    int alvo;
    std::cout << "Digite um número para buscar: ";
    std::cin >> alvo;

    buscaEmMatriz(matriz, alvo);

    return 0;
}
```

</details>

### 9. Determinante de Matriz 3x3 ⭐⭐⭐⭐
**Objetivo:** Escreva uma função que calcule o determinante de uma matriz 3x3.

**Importância:** O cálculo de determinantes é fundamental em álgebra linear e tem aplicações em sistemas de equações lineares e transformações geométricas.

**Dica de implementação:** Use a regra de Sarrus ou a expansão de Laplace. Para uma matriz 3x3, você pode implementar diretamente a fórmula do determinante.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int determinante3x3(int matriz[3][3]) {
    return matriz[0][0] * (matriz[1][1] * matriz[2][2] - matriz[1][2] * matriz[2][1])
         - matriz[0][1] * (matriz[1][0] * matriz[2][2] - matriz[1][2] * matriz[2][0])
         + matriz[0][2] * (matriz[1][0] * matriz[2][1] - matriz[1][1] * matriz[2][0]);
}

int main() {
    int matriz[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int det = determin
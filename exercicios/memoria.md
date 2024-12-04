# Lista de Exercícios de Alocação Dinâmica de Memória em C++

Antes de começar os exercícios, lembre-se: a melhor maneira de aprender programação é praticando. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Alocação e Desalocação Básica ⭐
**Objetivo:** Aloque dinamicamente um inteiro, atribua um valor a ele, imprima o valor e então desaloque a memória.

**Exemplo:**
Saída esperada:
```
Valor alocado: 42
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int* ptr = new int;
    *ptr = 42;
    
    std::cout << "Valor alocado: " << *ptr << std::endl;
    
    delete ptr;
    ptr = nullptr;

    return 0;
}
```

</details>

### 2. Array Dinâmico ⭐⭐
**Objetivo:** Crie uma função que aloque dinamicamente um array de inteiros, preencha-o com os primeiros n números pares e retorne o ponteiro para o array.

**Exemplo:**
Entrada: 5
Saída esperada:
```
Array de números pares: 2 4 6 8 10
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int* criarArrayPares(int n) {
    int* arr = new int[n];
    for (int i = 0; i < n; i++) {
        arr[i] = (i + 1) * 2;
    }
    return arr;
}

int main() {
    int n;
    std::cout << "Digite o tamanho do array: ";
    std::cin >> n;

    int* pares = criarArrayPares(n);

    std::cout << "Array de números pares: ";
    for (int i = 0; i < n; i++) {
        std::cout << pares[i] << " ";
    }
    std::cout << std::endl;

    delete[] pares;
    pares = nullptr;

    return 0;
}
```

</details>

### 3. Redimensionamento de Array ⭐⭐
**Objetivo:** Implemente uma função que receba um array dinâmico, seu tamanho atual e um novo tamanho. A função deve redimensionar o array para o novo tamanho, preservando os elementos existentes.

**Exemplo:**
Entrada: Array [1, 2, 3], tamanho atual 3, novo tamanho 5
Saída esperada:
```
Array original: 1 2 3
Array redimensionado: 1 2 3 0 0
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int* redimensionarArray(int* arr, int tamanhoAtual, int novoTamanho) {
    int* novoArr = new int[novoTamanho];
    
    // Copia os elementos existentes
    for (int i = 0; i < tamanhoAtual && i < novoTamanho; i++) {
        novoArr[i] = arr[i];
    }
    
    // Inicializa novos elementos com 0
    for (int i = tamanhoAtual; i < novoTamanho; i++) {
        novoArr[i] = 0;
    }
    
    delete[] arr;
    return novoArr;
}

int main() {
    int tamanhoAtual = 3;
    int* arr = new int[tamanhoAtual] {1, 2, 3};
    
    std::cout << "Array original: ";
    for (int i = 0; i < tamanhoAtual; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    
    int novoTamanho = 5;
    arr = redimensionarArray(arr, tamanhoAtual, novoTamanho);
    
    std::cout << "Array redimensionado: ";
    for (int i = 0; i < novoTamanho; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
    
    delete[] arr;
    arr = nullptr;
    
    return 0;
}
```

</details>

### 4. Matriz Dinâmica ⭐⭐⭐
**Objetivo:** Crie uma função que aloque dinamicamente uma matriz 2D de inteiros e outra função que a desaloque.

**Exemplo:**
Entrada: 3 linhas, 4 colunas
Saída esperada:
```
Matriz alocada:
0 0 0 0
0 0 0 0
0 0 0 0
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int** alocarMatriz(int linhas, int colunas) {
    int** matriz = new int*[linhas];
    for (int i = 0; i < linhas; i++) {
        matriz[i] = new int[colunas]();  // Inicializa com zeros
    }
    return matriz;
}

void desalocarMatriz(int** matriz, int linhas) {
    for (int i = 0; i < linhas; i++) {
        delete[] matriz[i];
    }
    delete[] matriz;
}

void imprimirMatriz(int** matriz, int linhas, int colunas) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

int main() {
    int linhas = 3, colunas = 4;
    int** matriz = alocarMatriz(linhas, colunas);

    std::cout << "Matriz alocada:" << std::endl;
    imprimirMatriz(matriz, linhas, colunas);

    desalocarMatriz(matriz, linhas);
    matriz = nullptr;

    return 0;
}
```

</details>

### 5. Alocação Dinâmica de Strings ⭐⭐
**Objetivo:** Crie um programa que aloque dinamicamente um array de strings (array de char*). O programa deve ler N strings do usuário e armazená-las neste array.

**Exemplo:**
Entrada: N = 3, strings: "Hello", "World", "C++"
Saída esperada:
```
Strings armazenadas:
1: Hello
2: World
3: C++
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cstring>

int main() {
    int N;
    std::cout << "Quantas strings você quer armazenar? ";
    std::cin >> N;
    std::cin.ignore(); // Limpa o buffer do teclado

    char** strings = new char*[N];

    for (int i = 0; i < N; i++) {
        const int MAX_LENGTH = 100;
        strings[i] = new char[MAX_LENGTH];
        std::cout << "Digite a string " << i+1 << ": ";
        std::cin.getline(strings[i], MAX_LENGTH);
    }

    std::cout << "\nStrings armazenadas:" << std::endl;
    for (int i = 0; i < N; i++) {
        std::cout << i+1 << ": " << strings[i] << std::endl;
    }

    // Liberando a memória
    for (int i = 0; i < N; i++) {
        delete[] strings[i];
    }
    delete[] strings;

    return 0;
}
```

</details>

### 6. Calculadora de Média ⭐⭐
**Objetivo:** Crie um programa que aloque dinamicamente um array de notas (números de ponto flutuante). O programa deve ler N notas do usuário, calcular a média e imprimir o resultado.

**Exemplo:**
Entrada: N = 4, notas: 7.5, 8.0, 6.5, 9.0
Saída esperada:
```
Média das notas: 7.75
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int N;
    std::cout << "Quantas notas você quer calcular? ";
    std::cin >> N;

    float* notas = new float[N];

    for (int i = 0; i < N; i++) {
        std::cout << "Digite a nota " << i+1 << ": ";
        std::cin >> notas[i];
    }

    float soma = 0;
    for (int i = 0; i < N; i++) {
        soma += notas[i];
    }

    float media = soma / N;

    std::cout << "Média das notas: " << media << std::endl;

    delete[] notas;
    notas = nullptr;

    return 0;
}
```

</details>

Estes exercícios cobrem os conceitos fundamentais de alocação dinâmica de memória em C++, adequados para um curso introdutório. Eles incluem exemplos práticos e evitam tópicos avançados, mantendo-se alinhados com o conteúdo da apresentação fornecida.

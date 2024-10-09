# Exercícios Introdutórios de C++ - Matrizes, Alocação Dinâmica e Ponteiros (com Soluções)

## 1. Soma de Elementos de uma Matriz ⭐
**Objetivo:** Calcule a soma de todos os elementos de uma matriz 3x3.

**Tarefas:**
1. Declare uma matriz 3x3 de inteiros.
2. Preencha a matriz com valores fornecidos pelo usuário.
3. Calcule e imprima a soma de todos os elementos.

**Exemplo:**
```cpp
int matriz[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
// Resultado: 45
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int matriz[3][3];
    int soma = 0;

    // Preenchendo a matriz
    cout << "Digite os 9 elementos da matriz:" << endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            cin >> matriz[i][j];
        }
    }

    // Calculando a soma
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            soma += matriz[i][j];
        }
    }

    cout << "A soma de todos os elementos é: " << soma << endl;

    return 0;
}
```

</details>

## 2. Maior Elemento de uma Matriz ⭐
**Objetivo:** Encontre o maior elemento em uma matriz 4x4.

**Tarefas:**
1. Declare uma matriz 4x4 de inteiros.
2. Preencha a matriz com valores aleatórios entre 1 e 100.
3. Encontre e imprima o maior elemento da matriz.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;

int main() {
    int matriz[4][4];
    int maior = 0;

    // Inicializar o gerador de números aleatórios
    srand(time(0));

    // Preenchendo a matriz com números aleatórios
    for(int i = 0; i < 4; i++) {
        for(int j = 0; j < 4; j++) {
            matriz[i][j] = rand() % 100 + 1;  // Números entre 1 e 100
            cout << matriz[i][j] << "\t";
            if(matriz[i][j] > maior) {
                maior = matriz[i][j];
            }
        }
        cout << endl;
    }

    cout << "O maior elemento da matriz é: " << maior << endl;

    return 0;
}
```

</details>

## 3. Alocação Dinâmica de um Array ⭐⭐
**Objetivo:** Crie um array dinâmico de inteiros.

**Tarefas:**
1. Peça ao usuário para inserir o tamanho do array.
2. Aloque dinamicamente um array com esse tamanho.
3. Preencha o array com números pares começando de 2.
4. Imprima o array e depois libere a memória.

**Exemplo:**
```
Tamanho do array: 5
Array: 2 4 6 8 10
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int tamanho;
    cout << "Digite o tamanho do array: ";
    cin >> tamanho;

    // Alocação dinâmica
    int* array = new int[tamanho];

    // Preenchendo o array
    for(int i = 0; i < tamanho; i++) {
        array[i] = (i + 1) * 2;
    }

    // Imprimindo o array
    cout << "Array: ";
    for(int i = 0; i < tamanho; i++) {
        cout << array[i] << " ";
    }
    cout << endl;

    // Liberando a memória
    delete[] array;

    return 0;
}
```

</details>

## 4. Soma de Dois Arrays com Ponteiros ⭐⭐
**Objetivo:** Some dois arrays usando ponteiros.

**Tarefas:**
1. Crie dois arrays de inteiros com 5 elementos cada.
2. Use ponteiros para somar os elementos correspondentes.
3. Armazene o resultado em um terceiro array.
4. Imprima o array resultante.

**Exemplo:**
```
Array1: 1 2 3 4 5
Array2: 5 4 3 2 1
Resultado: 6 6 6 6 6
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int array1[5] = {1, 2, 3, 4, 5};
    int array2[5] = {5, 4, 3, 2, 1};
    int resultado[5];

    int *ptr1 = array1;
    int *ptr2 = array2;
    int *ptr_res = resultado;

    for(int i = 0; i < 5; i++) {
        *ptr_res = *ptr1 + *ptr2;
        ptr1++;
        ptr2++;
        ptr_res++;
    }

    cout << "Resultado: ";
    for(int i = 0; i < 5; i++) {
        cout << resultado[i] << " ";
    }
    cout << endl;

    return 0;
}
```

</details>

## 5. Matriz Transposta ⭐⭐
**Objetivo:** Crie a transposta de uma matriz 3x3.

**Tarefas:**
1. Declare uma matriz 3x3 e preencha-a com valores.
2. Crie uma função que receba a matriz como argumento.
3. Dentro da função, crie uma nova matriz que seja a transposta da original.
4. Imprima a matriz original e a transposta.

**Exemplo:**
```
Original:     Transposta:
1 2 3         1 4 7
4 5 6         2 5 8
7 8 9         3 6 9
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

void transpor(int matriz[3][3]) {
    int transposta[3][3];

    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            transposta[j][i] = matriz[i][j];
        }
    }

    cout << "Matriz Original:" << endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            cout << matriz[i][j] << " ";
        }
        cout << endl;
    }

    cout << "Matriz Transposta:" << endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            cout << transposta[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    int matriz[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    transpor(matriz);
    return 0;
}
```

</details>

## 6. Alocação Dinâmica de Matriz ⭐⭐⭐
**Objetivo:** Aloque dinamicamente uma matriz 2D.

**Tarefas:**
1. Peça ao usuário para inserir o número de linhas e colunas.
2. Aloque dinamicamente uma matriz com essas dimensões.
3. Preencha a matriz com números sequenciais.
4. Imprima a matriz e depois libere a memória.

**Exemplo:**
```
Linhas: 3, Colunas: 4
1  2  3  4
5  6  7  8
9 10 11 12
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int linhas, colunas;
    cout << "Digite o número de linhas: ";
    cin >> linhas;
    cout << "Digite o número de colunas: ";
    cin >> colunas;

    // Alocação dinâmica da matriz
    int** matriz = new int*[linhas];
    for(int i = 0; i < linhas; i++) {
        matriz[i] = new int[colunas];
    }

    // Preenchendo a matriz
    int valor = 1;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            matriz[i][j] = valor++;
        }
    }

    // Imprimindo a matriz
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            cout << matriz[i][j] << "\t";
        }
        cout << endl;
    }

    // Liberando a memória
    for(int i = 0; i < linhas; i++) {
        delete[] matriz[i];
    }
    delete[] matriz;

    return 0;
}
```

</details>

## 7. Contagem de Pares e Ímpares em Matriz ⭐⭐
**Objetivo:** Conte quantos números pares e ímpares existem em uma matriz 3x4.

**Tarefas:**
1. Declare uma matriz 3x4 de inteiros.
2. Preencha a matriz com valores fornecidos pelo usuário.
3. Conte quantos números são pares e quantos são ímpares.
4. Imprima os resultados.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int matriz[3][4];
    int pares = 0, impares = 0;

    cout << "Digite os 12 elementos da matriz:" << endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 4; j++) {
            cin >> matriz[i][j];
            if(matriz[i][j] % 2 == 0) {
                pares++;
            } else {
                impares++;
            }
        }
    }

    cout << "Quantidade de números pares: " << pares << endl;
    cout << "Quantidade de números ímpares: " << impares << endl;

    return 0;
}
```

</details>

## 8. Troca de Valores com Ponteiros ⭐
**Objetivo:** Troque os valores de duas variáveis usando ponteiros.

**Tarefas:**
1. Declare duas variáveis inteiras e inicialize-as com valores.
2. Crie uma função que receba dois ponteiros para inteiros.
3. Dentro da função, troque os valores apontados pelos ponteiros.
4. Imprima os valores antes e depois da troca.

**Exemplo:**
```
Antes: a = 5, b = 10
Depois: a = 10, b = 5
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

void trocar(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int a = 5, b = 10;

    cout << "Antes: a = " << a << ", b = " << b << endl;

    trocar(&a, &b);

    cout << "Depois: a = " << a << ", b = " << b << endl;

    return 0;
}
```

</details>

Estes exercícios fornecem uma introdução prática aos conceitos de matrizes, alocação dinâmica de memória e ponteiros em C++. As soluções incluídas oferecem um guia para os alunos verificarem seu trabalho ou obterem ajuda quando necessário.


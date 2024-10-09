# Exercícios de C++ - Matrizes, Alocação Dinâmica e Ponteiros

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

void lerMatriz(int (*matriz)[3], int linhas) {
    cout << "Digite os 9 elementos da matriz:" << endl;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 3; j++) {
            cin >> matriz[i][j];
        }
    }
}

int somaMatriz(int (*matriz)[3], int linhas) {
    int soma = 0;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 3; j++) {
            soma += matriz[i][j];
        }
    }
    return soma;
}

int main() {
    int matriz[3][3];
    lerMatriz(matriz, 3);
    int soma = somaMatriz(matriz, 3);
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

void preencherMatriz(int (*matriz)[4], int linhas) {
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 4; j++) {
            matriz[i][j] = rand() % 100 + 1;
        }
    }
}

void imprimirMatriz(int (*matriz)[4], int linhas) {
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 4; j++) {
            cout << matriz[i][j] << "\t";
        }
        cout << endl;
    }
}

int encontrarMaior(int (*matriz)[4], int linhas) {
    int maior = matriz[0][0];
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 4; j++) {
            if(matriz[i][j] > maior) {
                maior = matriz[i][j];
            }
        }
    }
    return maior;
}

int main() {
    int matriz[4][4];
    srand(time(0));
    preencherMatriz(matriz, 4);
    cout << "Matriz:" << endl;
    imprimirMatriz(matriz, 4);
    int maior = encontrarMaior(matriz, 4);
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

int* alocarArray(int tamanho) {
    return new int[tamanho];
}

void preencherArray(int* array, int tamanho) {
    for(int i = 0; i < tamanho; i++) {
        array[i] = (i + 1) * 2;
    }
}

void imprimirArray(int* array, int tamanho) {
    cout << "Array: ";
    for(int i = 0; i < tamanho; i++) {
        cout << array[i] << " ";
    }
    cout << endl;
}

void liberarArray(int* array) {
    delete[] array;
}

int main() {
    int tamanho;
    cout << "Digite o tamanho do array: ";
    cin >> tamanho;

    int* array = alocarArray(tamanho);
    preencherArray(array, tamanho);
    imprimirArray(array, tamanho);
    liberarArray(array);

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

void somarArrays(int* arr1, int* arr2, int* resultado, int tamanho) {
    int *ptr1 = arr1, *ptr2 = arr2, *ptrRes = resultado;
    for(int i = 0; i < tamanho; i++, ptr1++, ptr2++, ptrRes++) {
        *ptrRes = *ptr1 + *ptr2;
    }
}

void imprimirArray(int* arr, int tamanho, const char* nome) {
    cout << nome << ": ";
    for(int i = 0; i < tamanho; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int array1[] = {1, 2, 3, 4, 5};
    int array2[] = {5, 4, 3, 2, 1};
    int resultado[5];

    somarArrays(array1, array2, resultado, 5);

    imprimirArray(array1, 5, "Array1");
    imprimirArray(array2, 5, "Array2");
    imprimirArray(resultado, 5, "Resultado");

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

void preencherMatriz(int (*matriz)[3]) {
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            matriz[i][j] = i * 3 + j + 1;
        }
    }
}

void imprimirMatriz(int (*matriz)[3], const char* nome) {
    cout << nome << ":" << endl;
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            cout << matriz[i][j] << " ";
        }
        cout << endl;
    }
}

void transpor(int (*matriz)[3], int (*transposta)[3]) {
    for(int i = 0; i < 3; i++) {
        for(int j = 0; j < 3; j++) {
            transposta[j][i] = matriz[i][j];
        }
    }
}

int main() {
    int matriz[3][3];
    int transposta[3][3];

    preencherMatriz(matriz);
    imprimirMatriz(matriz, "Matriz Original");

    transpor(matriz, transposta);
    imprimirMatriz(transposta, "Matriz Transposta");

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

int** alocarMatriz(int linhas, int colunas) {
    int** matriz = new int*[linhas];
    for(int i = 0; i < linhas; i++) {
        matriz[i] = new int[colunas];
    }
    return matriz;
}

void preencherMatriz(int** matriz, int linhas, int colunas) {
    int valor = 1;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            matriz[i][j] = valor++;
        }
    }
}

void imprimirMatriz(int** matriz, int linhas, int colunas) {
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            cout << matriz[i][j] << "\t";
        }
        cout << endl;
    }
}

void liberarMatriz(int** matriz, int linhas) {
    for(int i = 0; i < linhas; i++) {
        delete[] matriz[i];
    }
    delete[] matriz;
}

int main() {
    int linhas, colunas;
    cout << "Digite o número de linhas: ";
    cin >> linhas;
    cout << "Digite o número de colunas: ";
    cin >> colunas;

    int** matriz = alocarMatriz(linhas, colunas);
    preencherMatriz(matriz, linhas, colunas);
    imprimirMatriz(matriz, linhas, colunas);
    liberarMatriz(matriz, linhas);

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

void lerMatriz(int (*matriz)[4], int linhas) {
    cout << "Digite os 12 elementos da matriz:" << endl;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 4; j++) {
            cin >> matriz[i][j];
        }
    }
}

void contarParesImpares(int (*matriz)[4], int linhas, int* pares, int* impares) {
    *pares = 0;
    *impares = 0;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < 4; j++) {
            if(matriz[i][j] % 2 == 0) {
                (*pares)++;
            } else {
                (*impares)++;
            }
        }
    }
}

int main() {
    int matriz[3][4];
    int pares, impares;

    lerMatriz(matriz, 3);
    contarParesImpares(matriz, 3, &pares, &impares);

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


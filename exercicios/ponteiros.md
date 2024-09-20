# Lista de Exercícios de Ponteiros em C++

Antes de mergulhar nas soluções, lembre-se: a melhor maneira de aprender programação é fazendo por conta própria. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Declaração e Uso Básico de Ponteiros ⭐
**Objetivo:** Declare uma variável inteira, um ponteiro para essa variável, e imprima o valor da variável usando o ponteiro.

**Exemplo:**
Saída esperada:
```
Valor da variável: 42
Valor através do ponteiro: 42
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int num = 42;
    int* ptr = &num;

    std::cout << "Valor da variável: " << num << std::endl;
    std::cout << "Valor através do ponteiro: " << *ptr << std::endl;

    return 0;
}
```

</details>

### 2. Modificação de Valor via Ponteiro ⭐
**Objetivo:** Crie uma função que receba um ponteiro para um inteiro e dobre o valor da variável apontada.

**Exemplo:**
Entrada: 5
Saída esperada:
```
Valor original: 5
Valor após dobrar: 10
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void dobrarValor(int* ptr) {
    *ptr *= 2;
}

int main() {
    int num;
    std::cout << "Digite um número: ";
    std::cin >> num;

    std::cout << "Valor original: " << num << std::endl;
    dobrarValor(&num);
    std::cout << "Valor após dobrar: " << num << std::endl;

    return 0;
}
```

</details>

### 3. Troca de Valores Usando Ponteiros ⭐⭐
**Objetivo:** Escreva uma função que troque os valores de duas variáveis inteiras usando ponteiros.

**Exemplo:**
Entrada: 5, 10
Saída esperada:
```
Antes da troca: x = 5, y = 10
Depois da troca: x = 10, y = 5
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void trocar(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x, y;
    std::cout << "Digite dois números: ";
    std::cin >> x >> y;

    std::cout << "Antes da troca: x = " << x << ", y = " << y << std::endl;
    trocar(&x, &y);
    std::cout << "Depois da troca: x = " << x << ", y = " << y << std::endl;

    return 0;
}
```

</details>

### 4. Aritmética de Ponteiros com Arrays ⭐⭐
**Objetivo:** Use um ponteiro para percorrer e imprimir os elementos de um array.

**Exemplo:**
Saída esperada:
```
Elementos do array:
10 20 30 40 50
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int* ptr = arr;

    std::cout << "Elementos do array:" << std::endl;
    for (int i = 0; i < 5; i++) {
        std::cout << *ptr << " ";
        ptr++;
    }
    std::cout << std::endl;

    return 0;
}
```

</details>

### 5. Ponteiros e Funções ⭐⭐
**Objetivo:** Crie uma função que receba um array e seu tamanho como parâmetros, e calcule a soma dos elementos usando ponteiros.

**Exemplo:**
Entrada: Array com elementos 1, 2, 3, 4, 5
Saída esperada:
```
A soma dos elementos é: 15
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int somaArray(int* arr, int tamanho) {
    int soma = 0;
    for (int i = 0; i < tamanho; i++) {
        soma += *arr;
        arr++;
    }
    return soma;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int tamanho = sizeof(arr) / sizeof(arr[0]);

    std::cout << "A soma dos elementos é: " << somaArray(arr, tamanho) << std::endl;

    return 0;
}
```

</details>

### 6. Ponteiros para Ponteiros ⭐⭐⭐
**Objetivo:** Declare um ponteiro para ponteiro (ponteiro duplo) e use-o para modificar o valor de uma variável.

**Exemplo:**
Saída esperada:
```
Valor original: 42
Valor após modificação: 100
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int valor = 42;
    int* ptr = &valor;
    int** pptr = &ptr;

    std::cout << "Valor original: " << valor << std::endl;
    
    **pptr = 100;
    std::cout << "Valor após modificação: " << valor << std::endl;

    return 0;
}
```

</details>

### 7. Comparação de Ponteiros ⭐⭐
**Objetivo:** Crie um programa que compare os endereços de duas variáveis usando ponteiros.

**Exemplo:**
Saída esperada (os endereços serão diferentes em cada execução):
```
Endereço de x: 0x7ffd5ca30a5c
Endereço de y: 0x7ffd5ca30a60
y está em um endereço de memória maior que x
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int main() {
    int x = 5, y = 10;
    int* ptrX = &x;
    int* ptrY = &y;

    std::cout << "Endereço de x: " << ptrX << std::endl;
    std::cout << "Endereço de y: " << ptrY << std::endl;

    if (ptrX < ptrY) {
        std::cout << "y está em um endereço de memória maior que x" << std::endl;
    } else if (ptrX > ptrY) {
        std::cout << "x está em um endereço de memória maior que y" << std::endl;
    } else {
        std::cout << "x e y têm o mesmo endereço de memória" << std::endl;
    }

    return 0;
}
```

</details>

### 8. Ponteiros e Arrays Multidimensionais ⭐⭐⭐
**Objetivo:** Use ponteiros duplos para acessar e modificar elementos de uma matriz 2D estática.

**Exemplo:**
Saída esperada:
```
Matriz original:
1 2 3
4 5 6

Matriz após modificação:
2 4 6
8 10 12
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

const int LINHAS = 2;
const int COLUNAS = 3;

void imprimirMatriz(int** matriz, int linhas, int colunas) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

void modificarMatriz(int** matriz, int linhas, int colunas) {
    for (int i = 0; i < linhas; i++) {
        for (int j = 0; j < colunas; j++) {
            matriz[i][j] *= 2;
        }
    }
}

int main() {
    int matriz[LINHAS][COLUNAS] = {{1, 2, 3}, {4, 5, 6}};
    
    // Criando um array de ponteiros para as linhas da matriz
    int* ptrMatriz[LINHAS];
    for (int i = 0; i < LINHAS; i++) {
        ptrMatriz[i] = matriz[i];
    }

    // Ponteiro para o array de ponteiros
    int** ptr = ptrMatriz;

    std::cout << "Matriz original:" << std::endl;
    imprimirMatriz(ptr, LINHAS, COLUNAS);

    modificarMatriz(ptr, LINHAS, COLUNAS);

    std::cout << "\nMatriz após modificação:" << std::endl;
    imprimirMatriz(ptr, LINHAS, COLUNAS);

    return 0;
}
```

</details>


### 9. Ponteiros e Retorno de Função ⭐⭐
**Objetivo:** Crie uma função que retorne um ponteiro para o maior valor entre dois inteiros.

**Exemplo:**
Entrada: 5, 10
Saída esperada:
```
O maior valor é: 10
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int* maiorValor(int* a, int* b) {
    return (*a > *b) ? a : b;
}

int main() {
    int x, y;
    std::cout << "Digite dois números: ";
    std::cin >> x >> y;

    int* maior = maiorValor(&x, &y);
    std::cout << "O maior valor é: " << *maior << std::endl;

    return 0;
}
```

</details>

Estes exercícios cobrem os conceitos fundamentais de ponteiros em C++, adequados para um curso introdutório. Eles incluem exemplos práticos e evitam tópicos avançados como alocação dinâmica de memória, manipulação complexa de strings e estruturas de dados complexas.

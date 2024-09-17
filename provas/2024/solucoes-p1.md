# Soluções da Prova de Introdução à Programação - 2024.2 - UERJ

## Questão 1

```cpp
bool buscarElemento(int arr[], int tamanho, int elemento, int& posicao) {
    for (int i = 0; i < tamanho; i++) {
        if (arr[i] == elemento) {
            posicao = i;
            return true;
        }
    }
    return false;
}

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int pos = -1;
    bool encontrado = buscarElemento(arr, 5, 30, pos);
    cout << "Elemento " << (encontrado ? "encontrado" : "não encontrado");
    if (encontrado) cout << " na posição " << pos;
    cout << endl;
    return 0;
}
```

## Questão 2

```cpp
void ordenarArray(int arr[], int tamanho, bool crescente) {
    for (int i = 0; i < tamanho - 1; i++) {
        for (int j = i + 1; j < tamanho; j++) {
            if ((crescente && arr[i] > arr[j]) || (!crescente && arr[i] < arr[j])) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}

int main() {
    int arr[] = {5, 2, 8, 1, 9};
    ordenarArray(arr, 5, true);
    for (int i = 0; i < 5; i++) cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

## Questão 3

```cpp
void gerarSequencia(int arr[], int tamanho) {
    if (tamanho <= 0) return;
    
    arr[0] = 1;
    if (tamanho > 1) {
        arr[1] = 1;
    }
    
    for (int i = 2; i < tamanho; i++) {
        arr[i] = arr[i-1] + arr[i-2];
    }
}

int main() {
    int arr[6];
    gerarSequencia(arr, 6);
    for (int i = 0; i < 6; i++) cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

## Questão 4

```cpp
void trocarArraysInverso(int arr1[], int arr2[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {
        int temp = arr1[i];
        arr1[i] = arr2[tamanho - 1 - i];
        arr2[tamanho - 1 - i] = temp;
    }
}

int main() {
    int arr1[] = {1, 2, 3, 4, 5};
    int arr2[] = {10, 20, 30, 40, 50};
    trocarArraysInverso(arr1, arr2, 5);
    for (int i = 0; i < 5; i++) cout << arr1[i] << " ";
    cout << " | ";
    for (int i = 0; i < 5; i++) cout << arr2[i] << " ";
    cout << endl;
    return 0;
}
```

## Questão 5

```cpp
#include <string>

string avaliarMudancaMarcha(int rpm, int velocidade, int marcha) {
    int rpmMin[] = {1000, 1500, 2000, 2500, 3000};
    int rpmMax[] = {2500, 3000, 3500, 4000, 4500};
    int velMin[] = {0, 15, 30, 50, 70};
    int velMax[] = {20, 40, 60, 80, 999}; // 999 para representar 70+

    int index = marcha - 1;
    if (index < 0 || index > 4) return "Marcha inválida";

    if (rpm < rpmMin[index] || velocidade < velMin[index]) {
        return (marcha > 1) ? "Descer Marcha" : "Manter Marcha";
    } else if (rpm > rpmMax[index] || velocidade > velMax[index]) {
        return (marcha < 5) ? "Subir Marcha" : "Manter Marcha";
    } else {
        return "Manter Marcha";
    }
}

int main() {
    cout << avaliarMudancaMarcha(3200, 45, 2) << endl;
    return 0;
}
```

Cada solução inclui a implementação da função solicitada e um exemplo simples de uso na função `main()`. As soluções estão separadas e em formato Markdown, facilitando a leitura e a possível inclusão em documentos ou sistemas de gerenciamento de conteúdo.

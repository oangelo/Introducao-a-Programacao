# Soluções da Prova de Introdução à Programação - 2024.2 - UERJ

## Questão 1 (2 pontos)

```cpp
bool buscarElemento(int arr[], int tamanho, int elemento, int& posicao) {
    for (int i = 0; i < tamanho; i++) {  // Percorre o array (0.5 ponto)
        if (arr[i] == elemento) {  // Verifica se o elemento foi encontrado (0.5 ponto)
            posicao = i;  // Atualiza a posição do elemento encontrado (0.5 ponto)
            return true;  // Retorna true se o elemento foi encontrado (0.25 ponto)
        }
    }
    return false;  // Retorna false se o elemento não foi encontrado (0.25 ponto)
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

## Questão 2 (2 pontos)

```cpp
void ordenarArray(int arr[], int tamanho, bool crescente) {
    for (int i = 0; i < tamanho - 1; i++) {  // Loop externo (0.5 ponto)
        for (int j = i + 1; j < tamanho; j++) {  // Loop interno (0.5 ponto)
            // Comparação baseada na flag 'crescente' (0.5 ponto)
            if ((crescente && arr[i] > arr[j]) || (!crescente && arr[i] < arr[j])) {
                // Troca de elementos (0.5 ponto)
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

## Questão 3 (2 pontos)

```cpp
void gerarSequencia(int arr[], int tamanho) {
    if (tamanho <= 0) return;  // Tratamento de caso especial (0.25 ponto)
    
    arr[0] = 1;  // Inicialização do primeiro elemento (0.25 ponto)
    if (tamanho > 1) {
        arr[1] = 1;  // Inicialização do segundo elemento (0.25 ponto)
    }
    
    // Geração da sequência (1 ponto)
    for (int i = 2; i < tamanho; i++) {
        arr[i] = arr[i-1] + arr[i-2];  // Soma dos dois elementos anteriores
    }
    
    // Tratamento correto para diferentes tamanhos de array (0.25 ponto)
}

int main() {
    int arr[6];
    gerarSequencia(arr, 6);
    for (int i = 0; i < 6; i++) cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

## Questão 4 (2 pontos)

```cpp
void trocarArraysInverso(int arr1[], int arr2[], int tamanho) {
    for (int i = 0; i < tamanho; i++) {  // Loop para percorrer os arrays (0.5 ponto)
        // Troca de elementos na ordem inversa (1 ponto)
        int temp = arr1[i];
        arr1[i] = arr2[tamanho - 1 - i];
        arr2[tamanho - 1 - i] = temp;
    }
    // Lógica correta para inversão sem array adicional (0.5 ponto)
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

## Questão 5 (2 pontos)

```cpp
#include <string>

string avaliarMudancaMarcha(int rpm, int velocidade, int marcha) {
    // Definição dos arrays com os limites de RPM e velocidade (0.5 ponto)
    int rpmMin[] = {1000, 1500, 2000, 2500, 3000};
    int rpmMax[] = {2500, 3000, 3500, 4000, 4500};
    int velMin[] = {0, 15, 30, 50, 70};
    int velMax[] = {20, 40, 60, 80, 999}; // 999 para representar 70+

    // Verificação da marcha atual e ajuste do índice (0.25 ponto)
    int index = marcha - 1;
    if (index < 0 || index > 4) return "Marcha inválida";

    // Lógica de avaliação da mudança de marcha (1 ponto)
    if (rpm < rpmMin[index] || velocidade < velMin[index]) {
        return (marcha > 1) ? "Descer Marcha" : "Manter Marcha";
    } else if (rpm > rpmMax[index] || velocidade > velMax[index]) {
        return (marcha < 5) ? "Subir Marcha" : "Manter Marcha";
    } else {
        return "Manter Marcha";
    }

    // Tratamento de casos especiais (primeira e última marcha) (0.25 ponto)
}

int main() {
    cout << avaliarMudancaMarcha(3200, 45, 2) << endl;
    return 0;
}
```

Cada solução inclui comentários indicando a distribuição dos pontos para os aspectos mais importantes da implementação. A pontuação total para cada questão é de 2 pontos, divididos entre os elementos críticos de cada função.

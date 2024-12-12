# Lista de Exercícios de Ponteiros para Funções em C++

Antes de mergulhar nas soluções, lembre-se: a melhor maneira de aprender programação é fazendo por conta própria. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Declaração Básica de Ponteiro para Função ⭐
**Objetivo:** Declare um ponteiro para função que receba dois inteiros e retorne um inteiro, e use-o para apontar para uma função de soma.

**Exemplo:**
Saída esperada:
```
Resultado da soma: 15
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int soma(int a, int b) {
    return a + b;
}

int main() {
    int (*ptrFuncao)(int, int);  // Declaração do ponteiro para função
    ptrFuncao = soma;            // Atribuição da função ao ponteiro
    
    int resultado = ptrFuncao(7, 8);
    std::cout << "Resultado da soma: " << resultado << std::endl;
    
    return 0;
}
```

</details>

### 2. Array de Operações Matemáticas ⭐⭐
**Objetivo:** Implemente uma calculadora simples usando um array de ponteiros para funções que realize as quatro operações básicas.

**Exemplo:**
Entrada: 10, 5, operação (0-3)
Saída esperada:
```
Escolha a operação (0-Soma, 1-Subtração, 2-Multiplicação, 3-Divisão): 2
Resultado: 50
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int soma(int a, int b) { return a + b; }
int subtracao(int a, int b) { return a - b; }
int multiplicacao(int a, int b) { return a * b; }
int divisao(int a, int b) { return b != 0 ? a / b : 0; }

int main() {
    typedef int (*OperacaoMatematica)(int, int);
    OperacaoMatematica operacoes[] = {soma, subtracao, multiplicacao, divisao};
    
    int a, b, op;
    std::cout << "Digite dois números: ";
    std::cin >> a >> b;
    std::cout << "Escolha a operação (0-Soma, 1-Subtração, 2-Multiplicação, 3-Divisão): ";
    std::cin >> op;
    
    if (op >= 0 && op < 4) {
        std::cout << "Resultado: " << operacoes[op](a, b) << std::endl;
    } else {
        std::cout << "Operação inválida!" << std::endl;
    }
    
    return 0;
}
```

</details>

### 3. Processamento de Array com Callback ⭐⭐
**Objetivo:** Crie uma função que processe cada elemento de um array usando uma função callback passada como parâmetro.

**Exemplo:**
Entrada: Array [1, -2, 3, -4, 5]
Saída esperada:
```
Array original: 1 -2 3 -4 5
Array após processamento (valor absoluto): 1 2 3 4 5
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void processarArray(int arr[], int tamanho, int (*processador)(int)) {
    for(int i = 0; i < tamanho; i++) {
        arr[i] = processador(arr[i]);
    }
}

int valorAbsoluto(int x) {
    return x < 0 ? -x : x;
}

void imprimirArray(int arr[], int tamanho) {
    for(int i = 0; i < tamanho; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {1, -2, 3, -4, 5};
    int tamanho = sizeof(arr) / sizeof(arr[0]);
    
    std::cout << "Array original: ";
    imprimirArray(arr, tamanho);
    
    processarArray(arr, tamanho, valorAbsoluto);
    
    std::cout << "Array após processamento (valor absoluto): ";
    imprimirArray(arr, tamanho);
    
    return 0;
}
```

</details>

### 4. Sistema de Filtros em Cadeia ⭐⭐⭐
**Objetivo:** Implemente um sistema de filtros em cadeia que processe um valor através de múltiplos filtros usando um array de ponteiros para funções.

**Exemplo:**
Entrada: 150
Saída esperada:
```
Valor original: 150
Após filtro de máximo (100): 100
Após filtro de mínimo (0): 100
Após filtro de paridade (par): 100
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

typedef int (*Filtro)(int);

struct CadeiaFiltros {
    Filtro filtros[10];  // Array fixo de 10 filtros
    int quantidade;
};

void inicializarCadeia(CadeiaFiltros* cadeia) {
    cadeia->quantidade = 0;
}

void adicionarFiltro(CadeiaFiltros* cadeia, Filtro f) {
    if(cadeia->quantidade < 10) {
        cadeia->filtros[cadeia->quantidade] = f;
        cadeia->quantidade++;
    }
}

int processar(CadeiaFiltros* cadeia, int valor) {
    for(int i = 0; i < cadeia->quantidade; i++) {
        valor = cadeia->filtros[i](valor);
    }
    return valor;
}

int filtroMaximo(int x) { return x > 100 ? 100 : x; }
int filtroMinimo(int x) { return x < 0 ? 0 : x; }
int filtroParidade(int x) { return x - (x % 2); }

int main() {
    CadeiaFiltros cadeia;
    inicializarCadeia(&cadeia);
    
    adicionarFiltro(&cadeia, filtroMaximo);
    adicionarFiltro(&cadeia, filtroMinimo);
    adicionarFiltro(&cadeia, filtroParidade);
    
    int valor = 150;
    std::cout << "Valor original: " << valor << std::endl;
    valor = processar(&cadeia, valor);
    std::cout << "Valor após todos os filtros: " << valor << std::endl;
    
    return 0;
}
```

</details>



### 5. Menu de Comandos ⭐⭐
**Objetivo:** Crie um sistema de menu usando uma tabela de ponteiros para funções.

**Exemplo:**
Saída esperada:
```
Menu:
1. Novo
2. Abrir
3. Salvar
4. Sair
Escolha uma opção: 1
Criando novo arquivo...
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <string>

struct Comando {
    std::string nome;
    void (*executar)();
};

void novo() { std::cout << "Criando novo arquivo..." << std::endl; }
void abrir() { std::cout << "Abrindo arquivo..." << std::endl; }
void salvar() { std::cout << "Salvando arquivo..." << std::endl; }
void sair() { std::cout << "Saindo..." << std::endl; }

int main() {
    Comando comandos[] = {
        {"Novo", novo},
        {"Abrir", abrir},
        {"Salvar", salvar},
        {"Sair", sair}
    };
    
    std::cout << "Menu:" << std::endl;
    for(int i = 0; i < 4; i++) {
        std::cout << i + 1 << ". " << comandos[i].nome << std::endl;
    }
    
    int opcao;
    std::cout << "Escolha uma opção: ";
    std::cin >> opcao;
    
    if(opcao >= 1 && opcao <= 4) {
        comandos[opcao-1].executar();
    }
    
    return 0;
}
```

</details>

### 6. Ordenação Customizada ⭐⭐⭐
**Objetivo:** Implemente uma função de ordenação que aceite um ponteiro para função como critério de comparação.

**Exemplo:**
Saída esperada:
```
Array original: 5 2 8 1 9
Ordenado crescente: 1 2 5 8 9
Ordenado decrescente: 9 8 5 2 1
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

bool crescente(int a, int b) { return a < b; }
bool decrescente(int a, int b) { return a > b; }

void ordenar(int arr[], int tamanho, bool (*comparador)(int, int)) {
    for(int i = 0; i < tamanho-1; i++) {
        for(int j = 0; j < tamanho-i-1; j++) {
            if(comparador(arr[j+1], arr[j])) {
                std::swap(arr[j], arr[j+1]);
            }
        }
    }
}

void imprimirArray(int arr[], int tamanho) {
    for(int i = 0; i < tamanho; i++) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;
}

int main() {
    int arr[] = {5, 2, 8, 1, 9};
    int tamanho = sizeof(arr) / sizeof(arr[0]);
    
    std::cout << "Array original: ";
    imprimirArray(arr, tamanho);
    
    ordenar(arr, tamanho, crescente);
    std::cout << "Ordenado crescente: ";
    imprimirArray(arr, tamanho);
    
    ordenar(arr, tamanho, decrescente);
    std::cout << "Ordenado decrescente: ";
    imprimirArray(arr, tamanho);
    
    return 0;
}
```

</details>

### 7. Transformação em Cadeia ⭐⭐⭐
**Objetivo:** Implemente um sistema que permita aplicar múltiplas transformações em uma string usando um array de ponteiros para funções.

**Exemplo:**
Entrada: "Hello World"
Saída esperada:
```
Original: Hello World
Após transformações: HELLO_WORLD!
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cstring>

typedef char* (*Transformacao)(char*);

struct ProcessadorTexto {
    Transformacao transformacoes[10];  // Array fixo de 10 transformações
    int quantidade;
};

void inicializarProcessador(ProcessadorTexto* proc) {
    proc->quantidade = 0;
}

void adicionarTransformacao(ProcessadorTexto* proc, Transformacao t) {
    if(proc->quantidade < 10) {
        proc->transformacoes[proc->quantidade] = t;
        proc->quantidade++;
    }
}

void processarTexto(ProcessadorTexto* proc, char* texto) {
    for(int i = 0; i < proc->quantidade; i++) {
        proc->transformacoes[i](texto);
    }
}

char* paraMaiusculo(char* str) {
    for(int i = 0; str[i]; i++) {
        str[i] = toupper(str[i]);
    }
    return str;
}

char* substituirEspacos(char* str) {
    for(int i = 0; str[i]; i++) {
        if(str[i] == ' ') {
            str[i] = '_';
        }
    }
    return str;
}

char* adicionarExclamacao(char* str) {
    int len = strlen(str);
    str[len] = '!';
    str[len + 1] = '\0';
    return str;
}

int main() {
    char texto[100] = "Hello World";  // Buffer com tamanho fixo
    
    ProcessadorTexto processador;
    inicializarProcessador(&processador);
    
    adicionarTransformacao(&processador, paraMaiusculo);
    adicionarTransformacao(&processador, substituirEspacos);
    adicionarTransformacao(&processador, adicionarExclamacao);
    
    std::cout << "Original: " << texto << std::endl;
    processarTexto(&processador, texto);
    std::cout << "Após transformações: " << texto << std::endl;
    
    return 0;
}
```

</details>


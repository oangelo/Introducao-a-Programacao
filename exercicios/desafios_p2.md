# Exercícios Avançados para P2 

## 1. Rotação de Matriz 90 Graus no Sentido Horário

### Objetivo
Implementar uma função que rotacione uma matriz quadrada 90 graus no sentido horário.

### Conceitos Necessários
- Alocação dinâmica de memória
- Manipulação de matrizes usando ponteiros
- Lógica de rotação de matriz

### Explicação Detalhada
A rotação de uma matriz 90 graus no sentido horário significa que cada elemento da matriz muda de posição de forma que:
- A primeira linha se torna a última coluna
- A última linha se torna a primeira coluna
- As linhas intermediárias seguem o mesmo padrão

### Exemplo
Matriz original 3x3:
```
1 2 3
4 5 6
7 8 9
```

Matriz após rotação 90 graus no sentido horário:
```
7 4 1
8 5 2
9 6 3
```

### Tarefas
1. Crie uma função para alocar dinamicamente uma matriz quadrada de tamanho n x n.
2. Implemente uma função para preencher a matriz com valores.
3. Desenvolva uma função para imprimir a matriz.
4. Crie a função principal de rotação, que deve modificar a matriz original sem usar uma matriz auxiliar.
5. Implemente uma função para desalocar a memória da matriz.

### Dicas
- Para rotacionar sem usar uma matriz auxiliar, considere trocar os elementos em grupos de 4.
- Comece pelos elementos das bordas e vá se movendo para o centro da matriz.
- Lembre-se de que em C++, as matrizes são armazenadas em ordem de linha (row-major order).

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

// Função para alocar dinamicamente uma matriz quadrada de tamanho n x n
int** alocarMatriz(int n) {
    int** matriz = new int*[n];
    for(int i = 0; i < n; ++i) {
        matriz[i] = new int[n];
    }
    return matriz;
}

// Função para preencher a matriz com valores
void preencherMatriz(int** matriz, int n) {
    std::cout << "Digite os elementos da matriz (" << n*n << " elementos):\n";
    for(int i = 0; i < n; ++i) {
        for(int j = 0; j < n; ++j) {
            std::cin >> matriz[i][j];
        }
    }
}

// Função para imprimir a matriz
void imprimirMatriz(int** matriz, int n) {
    std::cout << "Matriz atual:\n";
    for(int i = 0; i < n; ++i) {
        for(int j = 0; j < n; ++j) {
            std::cout << matriz[i][j] << " ";
        }
        std::cout << "\n";
    }
    std::cout << std::endl;
}

void rotacionarMatriz(int** matriz, int n) {
    // 1. Transpor a matriz (trocar elementos [i][j] com [j][i] para i < j)
    for(int i = 0; i < n; ++i) {
        for(int j = i + 1; j < n; ++j) {
            // Troca manualmente 
            int temp = matriz[i][j];
            matriz[i][j] = matriz[j][i];
            matriz[j][i] = temp;
        }
    }

    // 2. Reverter cada linha da matriz
    for(int i = 0; i < n; ++i) {
        for(int j = 0; j < n / 2; ++j) {
            // Troca manualmente 
            int temp = matriz[i][j];
            matriz[i][j] = matriz[i][n - 1 - j];
            matriz[i][n - 1 - j] = temp;
        }
    }
}

// Função para desalocar a memória da matriz
void desalocarMatriz(int** matriz, int n) {
    for(int i = 0; i < n; ++i) {
        delete[] matriz[i];
    }
    delete[] matriz;
}

int main() {
    int n;
    std::cout << "Digite o tamanho da matriz quadrada (n): ";
    std::cin >> n;
    
    // Aloca a matriz
    int** matriz = alocarMatriz(n);
    
    // Preenche a matriz
    preencherMatriz(matriz, n);
    
    // Imprime a matriz original
    std::cout << "\nMatriz Original:\n";
    imprimirMatriz(matriz, n);
    
    // Rotaciona a matriz 90 graus no sentido horário
    rotacionarMatriz(matriz, n);
    
    // Imprime a matriz rotacionada
    std::cout << "Matriz após rotação 90 graus no sentido horário:\n";
    imprimirMatriz(matriz, n);
    
    // Desaloca a matriz
    desalocarMatriz(matriz, n);
    
    return 0;
}
```

</details>

## 2. Espiral de Matriz

### Objetivo
Criar uma função que preencha uma matriz em espiral.

### Conceitos Necessários
- Alocação dinâmica de matriz 2D
- Manipulação de matrizes usando ponteiros
- Lógica de preenchimento em espiral

### Explicação Detalhada
O preenchimento em espiral de uma matriz envolve preencher os elementos da borda externa da matriz em sentido horário, e então mover-se para dentro, continuando o padrão até que toda a matriz esteja preenchida.

### Exemplo
Para uma matriz 4x4, o preenchimento em espiral resultaria em:
```
 1   2   3   4
12  13  14   5
11  16  15   6
10   9   8   7
```

### Tarefas
1. Implemente uma função para alocar dinamicamente uma matriz quadrada.
2. Desenvolva uma função que preencha a matriz em espiral (do exterior para o centro).
3. Crie uma função para imprimir a matriz resultante.
4. Implemente uma função para desalocar a memória da matriz.

### Dicas
- Comece preenchendo a borda superior, depois a direita, inferior e esquerda.
- Use variáveis para controlar os limites atuais da espiral (linha/coluna inicial e final).
- A cada volta completa da espiral, atualize esses limites.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <iomanip>

// Função para alocar uma matriz quadrada de tamanho n x n
int** alocarMatriz(int n) {
    int** matriz = new int*[n];
    if (matriz == nullptr) {
        std::cerr << "Erro ao alocar memória." << std::endl;
        std::exit(1);
    }
    for(int i = 0; i < n; ++i) {
        matriz[i] = new int[n];
        if(matriz[i] == nullptr) {
            std::cerr << "Erro ao alocar memória." << std::endl;
            std::exit(1);
        }
    }
    return matriz;
}

// Função para preencher a matriz em espiral
void preencherEspiral(int** matriz, int n) {
    int inicioLinha = 0, fimLinha = n - 1;
    int inicioColuna = 0, fimColuna = n - 1;
    int contador = 1;

    while(inicioLinha <= fimLinha && inicioColuna <= fimColuna) {
        // Preenche a borda superior
        for(int i = inicioColuna; i <= fimColuna; ++i) {
            matriz[inicioLinha][i] = contador++;
        }
        inicioLinha++;

        // Preenche a borda direita
        for(int i = inicioLinha; i <= fimLinha; ++i) {
            matriz[i][fimColuna] = contador++;
        }
        fimColuna--;

        // Preenche a borda inferior
        if(inicioLinha <= fimLinha) {
            for(int i = fimColuna; i >= inicioColuna; --i) {
                matriz[fimLinha][i] = contador++;
            }
            fimLinha--;
        }

        // Preenche a borda esquerda
        if(inicioColuna <= fimColuna) {
            for(int i = fimLinha; i >= inicioLinha; --i) {
                matriz[i][inicioColuna] = contador++;
            }
            inicioColuna++;
        }
    }
}

// Função para imprimir a matriz
void imprimirMatriz(int** matriz, int n) {
    for(int i = 0; i < n; ++i) {
        for(int j = 0; j < n; ++j) {
            std::cout << std::setw(4) << matriz[i][j] << " ";
        }
        std::cout << std::endl;
    }
}

// Função para desalocar a memória da matriz
void desalocarMatriz(int** matriz, int n) {
    for(int i = 0; i < n; ++i) {
        delete[] matriz[i];
    }
    delete[] matriz;
}

int main() {
    int n;

    std::cout << "Digite o tamanho da matriz (n x n): ";
    std::cin >> n;

    if(n <= 0) {
        std::cerr << "Tamanho da matriz deve ser positivo." << std::endl;
        return 1;
    }

    // Aloca a matriz
    int** matriz = alocarMatriz(n);

    // Preenche a matriz em espiral
    preencherEspiral(matriz, n);

    // Imprime a matriz
    std::cout << "Matriz preenchida em espiral:\n";
    imprimirMatriz(matriz, n);

    // Desaloca a memória
    desalocarMatriz(matriz, n);

    return 0;
}

```
</details>


## 3. Detector de Ilhas

### Objetivo
Contar o número de "ilhas" em uma matriz binária.

### Conceitos Necessários
- Alocação dinâmica de matriz 2D
- Manipulação de matrizes usando ponteiros
- Algoritmo de busca iterativo

### Explicação Detalhada
Neste problema, uma matriz binária representa um mapa onde 0 representa água e 1 representa terra. Uma "ilha" é definida como um grupo conectado de 1s (terra). Dois pedaços de terra são considerados conectados se forem adjacentes horizontalmente ou verticalmente (não diagonalmente).

### Exemplo
Para a seguinte matriz 5x5:
```
1 0 1 0 0
1 1 0 0 1
0 1 0 0 0
0 0 0 1 1
1 0 1 0 1
```
Esta matriz contém 6 ilhas.

### Tarefas
1. Implemente uma função para alocar dinamicamente uma matriz binária.
2. Crie uma função para preencher a matriz com 0s e 1s (pode ser aleatório ou predefinido).
3. Desenvolva uma função iterativa que "marque" uma ilha inteira.
4. Implemente a função principal que percorre a matriz e conta o número de ilhas.
5. Crie uma função para imprimir a matriz e o número de ilhas encontradas.
6. Implemente uma função para desalocar a memória da matriz.

### Dicas
- Use um loop aninhado para percorrer a matriz.
- Ao encontrar um 1, marque-o como visitado (por exemplo, mudando para 2) e explore seus vizinhos usando um loop.
- Lembre-se de verificar os limites da matriz ao explorar os vizinhos.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
using namespace std;

// Função para alocar dinamicamente uma matriz 2D
int** alocarMatriz(int linhas, int colunas) {
    int** matriz = new int*[linhas];
    for(int i = 0; i < linhas; i++) {
        matriz[i] = new int[colunas];
    }
    return matriz;
}

// Função para preencher a matriz com valores predefinidos
void preencherMatriz(int** matriz, int linhas, int colunas) {
    // Exemplo predefinido conforme o enunciado
    int valores[5][5] = {
        {1, 0, 1, 0, 0},
        {1, 1, 0, 0, 1},
        {0, 1, 0, 0, 0},
        {0, 0, 0, 1, 1},
        {1, 0, 1, 0, 1}
    };
    
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            matriz[i][j] = valores[i][j];
        }
    }
}

// Função para imprimir a matriz
void imprimirMatriz(int** matriz, int linhas, int colunas) {
    cout << "Matriz:" << endl;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            cout << matriz[i][j] << " ";
        }
        cout << endl;
    }
}

// Função para marcar uma ilha inteira usando busca em profundidade iterativa
void marcarIlha(int** matriz, int linhas, int colunas, int x, int y) {
    // Pilha simples usando arrays
    int stackX[linhas * colunas];
    int stackY[linhas * colunas];
    int topo = -1;

    // Adiciona a posição inicial à pilha
    topo++;
    stackX[topo] = x;
    stackY[topo] = y;

    while(topo >= 0) {
        // Remove o elemento do topo da pilha
        int currentX = stackX[topo];
        int currentY = stackY[topo];
        topo--;

        // Marca como visitado (por exemplo, mudando para 2)
        if(matriz[currentX][currentY] == 1) {
            matriz[currentX][currentY] = 2;

            // Verifica os vizinhos (cima, baixo, esquerda, direita)
            // Cima
            if(currentX > 0 && matriz[currentX - 1][currentY] == 1) {
                topo++;
                stackX[topo] = currentX - 1;
                stackY[topo] = currentY;
            }
            // Baixo
            if(currentX < linhas - 1 && matriz[currentX + 1][currentY] == 1) {
                topo++;
                stackX[topo] = currentX + 1;
                stackY[topo] = currentY;
            }
            // Esquerda
            if(currentY > 0 && matriz[currentX][currentY - 1] == 1) {
                topo++;
                stackX[topo] = currentX;
                stackY[topo] = currentY - 1;
            }
            // Direita
            if(currentY < colunas - 1 && matriz[currentX][currentY + 1] == 1) {
                topo++;
                stackX[topo] = currentX;
                stackY[topo] = currentY + 1;
            }
        }
    }
}

// Função para contar o número de ilhas na matriz
int contarIlhas(int** matriz, int linhas, int colunas) {
    int contagem = 0;
    for(int i = 0; i < linhas; i++) {
        for(int j = 0; j < colunas; j++) {
            if(matriz[i][j] == 1) { // Encontrou uma nova ilha
                contagem++;
                marcarIlha(matriz, linhas, colunas, i, j);
            }
        }
    }
    return contagem;
}

// Função para desalocar a memória da matriz
void desalocarMatriz(int** matriz, int linhas) {
    for(int i = 0; i < linhas; i++) {
        delete[] matriz[i];
    }
    delete[] matriz;
}

int main() {
    int linhas = 5;
    int colunas = 5;

    // Aloca a matriz
    int** matriz = alocarMatriz(linhas, colunas);

    // Preenche a matriz com valores predefinidos
    preencherMatriz(matriz, linhas, colunas);

    // Imprime a matriz original
    imprimirMatriz(matriz, linhas, colunas);

    // Conta o número de ilhas
    int numeroDeIlhas = contarIlhas(matriz, linhas, colunas);

    // Imprime o número de ilhas encontradas
    cout << "Número de ilhas encontradas: " << numeroDeIlhas << endl;

    // Opcional: Imprime a matriz após a marcação das ilhas
    // Isso mostra como as ilhas foram marcadas como '2'
    cout << "\nMatriz após a marcação das ilhas:" << endl;
    imprimirMatriz(matriz, linhas, colunas);

    // Desaloca a memória da matriz
    desalocarMatriz(matriz, linhas);

    return 0;
}
```

</details>


## 4. Jogo da Vida de Conway

### Objetivo
Implementar uma simulação do Jogo da Vida de Conway usando matrizes e ponteiros.

### Conceitos Necessários
- Alocação dinâmica de memória para matrizes 2D
- Manipulação de matrizes usando ponteiros
- Lógica condicional para aplicar as regras do jogo

### Explicação Detalhada
O Jogo da Vida é um autômato celular desenvolvido por John Conway. Ele é jogado em uma grade bidimensional de células, onde cada célula pode estar viva ou morta. A evolução é determinada pelo estado inicial e não requer mais entradas. A cada geração, o estado de cada célula é determinado pelos seus oito vizinhos adjacentes, seguindo estas regras:

1. Qualquer célula viva com menos de dois vizinhos vivos morre (solidão).
2. Qualquer célula viva com dois ou três vizinhos vivos continua viva.
3. Qualquer célula viva com mais de três vizinhos vivos morre (superpopulação).
4. Qualquer célula morta com exatamente três vizinhos vivos se torna uma célula viva (reprodução).

### Exemplo Simplificado
Usando * para células vivas e . para células mortas:

Geração 1:
```
.*.
.*.
.*.
```

Geração 2:
```
...
***
...
```

### Tarefas
1. Crie funções para alocar e desalocar dinamicamente duas matrizes (uma para o estado atual e outra para o próximo estado).
2. Implemente uma função para inicializar o estado inicial da matriz (pode ser aleatório ou predefinido).
3. Desenvolva uma função iterativa que aplique as regras do jogo a cada célula.
4. Crie uma função para exibir o estado atual da matriz.
5. Implemente a lógica principal que alterna entre os dois estados usando ponteiros, sem copiar dados.

### Dicas
- Use dois ponteiros para matrizes e troque-os a cada geração, em vez de copiar dados.
- Considere as células nas bordas da matriz como tendo vizinhos "mortos" além da borda.
- Para melhor visualização, use caracteres diferentes para representar células vivas e mortas ao imprimir.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cstdlib> // Para rand() e srand()
#include <ctime>   // Para time()
using namespace std;

// Função para alocar dinamicamente uma matriz 2D
int** alocarMatriz(int linhas, int colunas) {
    int** matriz = new int*[linhas];
    for(int i = 0; i < linhas; ++i) {
        matriz[i] = new int[colunas];
    }
    return matriz;
}

// Função para desalocar uma matriz 2D
void desalocarMatriz(int** matriz, int linhas) {
    for(int i = 0; i < linhas; ++i) {
        delete[] matriz[i];
    }
    delete[] matriz;
}

// Função para inicializar a matriz com um padrão predefinido ou aleatório
void inicializarMatriz(int** matriz, int linhas, int colunas, int tipo) {
    if(tipo == 2) { // Aleatório
        // Inicializa a matriz de forma aleatória
        for(int i = 0; i < linhas; ++i) {
            for(int j = 0; j < colunas; ++j) {
                // 50% de chance de a célula estar viva
                matriz[i][j] = rand() % 2;
            }
        }
    }
    else { // Padrão Predefinido
        // Inicializa todas as células como mortas
        for(int i = 0; i < linhas; ++i) {
            for(int j = 0; j < colunas; ++j) {
                matriz[i][j] = 0;
            }
        }

        // Define um padrão inicial (exemplo: "Blinker")
        // Geração 1:
        // .*.
        // .*.
        // .*.
        if(linhas >= 3 && colunas >= 3) {
            matriz[0][1] = 1;
            matriz[1][1] = 1;
            matriz[2][1] = 1;
        }
    }
}

// Função para exibir a matriz no console
void exibirMatriz(int** matriz, int linhas, int colunas) {
    for(int i = 0; i < linhas; ++i) {
        for(int j = 0; j < colunas; ++j) {
            if(matriz[i][j] == 1)
                cout << "*";
            else
                cout << ".";
        }
        cout << endl;
    }
    cout << endl;
}

// Função para contar os vizinhos vivos de uma célula
int contarVizinhos(int** matriz, int linhas, int colunas, int x, int y) {
    int contagem = 0;
    // Percorre todas as células vizinhas
    for(int i = x-1; i <= x+1; ++i) {
        for(int j = y-1; j <= y+1; ++j) {
            // Verifica se está dentro dos limites da matriz
            if(i >= 0 && i < linhas && j >= 0 && j < colunas) {
                if(i == x && j == y)
                    continue; // Ignora a célula atual
                if(matriz[i][j] == 1)
                    contagem++;
            }
        }
    }
    return contagem;
}

// Função para calcular a próxima geração
void proximaGeracao(int** atual, int** proximo, int linhas, int colunas) {
    for(int i = 0; i < linhas; ++i) {
        for(int j = 0; j < colunas; ++j) {
            int vizinhos = contarVizinhos(atual, linhas, colunas, i, j);
            
            // Aplicar as regras do Jogo da Vida
            if(atual[i][j] == 1) {
                if(vizinhos < 2 || vizinhos > 3)
                    proximo[i][j] = 0; // Morte por solidão ou superpopulação
                else
                    proximo[i][j] = 1; // Continua viva
            }
            else {
                if(vizinhos == 3)
                    proximo[i][j] = 1; // Reprodução
                else
                    proximo[i][j] = 0; // Continua morta
            }
        }
    }
}

int main() {
    int linhas, colunas, geracoes;
    int escolha;

    // Inicializa o gerador de números aleatórios
    srand(time(0));

    // Solicita ao usuário as dimensões da matriz e o número de gerações
    cout << "Digite o número de linhas: ";
    cin >> linhas;
    cout << "Digite o número de colunas: ";
    cin >> colunas;
    cout << "Digite o número de gerações: ";
    cin >> geracoes;
    cout << endl;

    // Solicita ao usuário o tipo de inicialização
    cout << "Escolha o tipo de condição inicial:" << endl;
    cout << "1 - Padrão Predefinido (Blinker)" << endl;
    cout << "2 - Aleatório" << endl;
    cout << "Digite sua escolha (1 ou 2): ";
    cin >> escolha;
    cout << endl;

    // Valida a escolha do usuário
    if(escolha != 1 && escolha != 2) {
        cout << "Escolha inválida! Usando Padrão Predefinido (Blinker)." << endl;
        escolha = 1;
    }

    // Aloca duas matrizes: atual e próxima
    int** atual = alocarMatriz(linhas, colunas);
    int** proximo = alocarMatriz(linhas, colunas);

    // Inicializa a matriz atual com o estado inicial
    inicializarMatriz(atual, linhas, colunas, escolha);

    // Mostra o estado inicial
    cout << "Geração 0:" << endl;
    exibirMatriz(atual, linhas, colunas);

    // Loop para cada geração
    for(int g = 1; g <= geracoes; ++g) {
        // Calcula a próxima geração
        proximaGeracao(atual, proximo, linhas, colunas);

        // Exibe a próxima geração
        cout << "Geração " << g << ":" << endl;
        exibirMatriz(proximo, linhas, colunas);

        // Troca os ponteiros das matrizes
        int** temp = atual;
        atual = proximo;
        proximo = temp;
    }

    // Desaloca as matrizes
    desalocarMatriz(atual, linhas);
    desalocarMatriz(proximo, linhas);

    return 0;
}
```

</details>

## 5. Jogo da Velha Dinâmico

### Objetivo
Implementar o jogo da velha com um tabuleiro de tamanho variável.

### Conceitos Necessários
- Alocação dinâmica de memória para matriz 2D
- Manipulação de matrizes usando ponteiros
- Lógica de verificação de vitória em um jogo da velha

### Explicação Detalhada
O jogo da velha tradicional é jogado em um tabuleiro 3x3. Nesta versão dinâmica, o tabuleiro pode ter qualquer tamanho n x n, onde n é definido pelo usuário. As regras permanecem as mesmas: os jogadores alternam colocando seus símbolos (geralmente X e O) no tabuleiro, e o primeiro a formar uma linha, coluna ou diagonal completa com seu símbolo vence.

### Exemplo
Para um tabuleiro 4x4:
```
 X | O |   |   
---+---+---+---
 O | X |   |   
---+---+---+---
   |   | X |   
---+---+---+---
   |   | O | X 
```

### Tarefas
1. Crie uma função para alocar dinamicamente um tabuleiro n x n.
2. Implemente uma função para imprimir o estado atual do tabuleiro.
3. Desenvolva funções para fazer jogadas e verificar se são válidas.
4. Crie uma função iterativa para verificar se há um vencedor ou empate.
5. Implemente a lógica principal do jogo, alternando entre os jogadores.
6. Crie uma função para desalocar a memória do tabuleiro.

### Dicas
- Use caracteres para representar os espaços vazios, 'X' e 'O'.
- A verificação de vitória deve ser adaptável ao tamanho do tabuleiro.
- Considere implementar uma opção para o usuário escolher o tamanho do tabuleiro no início do jogo.


## 6. Editor de Texto Simples

### Objetivo
Criar um editor de texto simples que use um array dinâmico de arrays de char.

### Conceitos Necessários
- Alocação dinâmica de memória
- Manipulação de arrays de char
- Realocação de memória
- Ponteiros e arrays

### Explicação Detalhada
Um editor de texto simples deve ser capaz de armazenar várias linhas de texto, permitindo inserção, edição e remoção de linhas. O uso de um array dinâmico de arrays de char permite que o documento cresça conforme necessário.

### Funcionalidades
1. Inserir uma nova linha em qualquer posição do documento
2. Remover uma linha existente
3. Editar o conteúdo de uma linha específica
4. Buscar por uma palavra-chave em todas as linhas
5. Imprimir o documento inteiro

### Exemplo de Uso
```
Inserir: "Primeira linha"
Inserir: "Segunda linha"
Editar linha 1: "Linha dois modificada"
Imprimir documento:
1: Primeira linha
2: Linha dois modificada
Buscar "linha":
Encontrado em: linha 1, linha 2
```

### Tarefas
1. Implemente funções para alocar e desalocar um array dinâmico de ponteiros para char.
2. Crie funções para inserir, remover e editar linhas (arrays de char).
3. Desenvolva uma função de busca que retorne todas as linhas contendo uma palavra-chave.
4. Implemente a realocação dinâmica do array de ponteiros quando necessário.
5. Crie uma função para imprimir o documento inteiro.

### Dicas
- Use `new` e `delete` para alocar e desalocar memória dinamicamente.
- Lembre-se de alocar memória suficiente para o caractere nulo '\0' ao final de cada linha.
- Ao realocar o array de ponteiros, crie um novo array maior e copie os ponteiros existentes.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

using namespace std;

// Variáveis globais para o documento
char** document = nullptr; // Array dinâmico de ponteiros para char
int numLines = 0;          // Número atual de linhas no documento
int capacity = 0;          // Capacidade atual do documento

// Função para calcular o comprimento de uma string em C
int stringLength(const char* str) {
    int length = 0;
    while (str[length] != '\0') {
        length++;
    }
    return length;
}

// Função para copiar uma string em C de src para dest
void copyString(char* dest, const char* src) {
    int i = 0;
    while (src[i] != '\0') {
        dest[i] = src[i];
        i++;
    }
    dest[i] = '\0'; // Adiciona o terminador nulo
}

// Função para comparar duas strings em C
int compareStrings(const char* str1, const char* str2) {
    int i = 0;
    while (str1[i] != '\0' && str2[i] != '\0') {
        if (str1[i] != str2[i]) {
            return str1[i] - str2[i]; // Retorna a diferença dos primeiros caracteres não correspondentes
        }
        i++;
    }
    return str1[i] - str2[i];
}

// Função para encontrar uma substring dentro de uma string
int findSubstring(const char* str, const char* substr) {
    int lenStr = stringLength(str);
    int lenSubstr = stringLength(substr);
    if (lenSubstr == 0)
        return 0; // Substring vazia corresponde na posição 0
    for (int i = 0; i <= lenStr - lenSubstr; i++) {
        int j = 0;
        while (j < lenSubstr && str[i + j] == substr[j]) {
            j++;
        }
        if (j == lenSubstr) {
            return i; // Substring encontrada na posição i
        }
    }
    return -1; // Substring não encontrada
}

// Função para ler uma linha de texto do usuário
char* readLine() {
    int capacity = 10; // Capacidade inicial para a linha
    char* buffer = new char[capacity];
    int length = 0;
    char ch;
    while (true) {
        cin.get(ch); // Lê um caractere
        if (ch == '\n') {
            break; // Para de ler ao encontrar uma nova linha
        }
        if (length + 1 >= capacity) {
            // Realoca o buffer com maior capacidade
            int newCapacity = capacity * 2;
            char* newBuffer = new char[newCapacity];
            for (int i = 0; i < length; i++) {
                newBuffer[i] = buffer[i];
            }
            delete[] buffer;
            buffer = newBuffer;
            capacity = newCapacity;
        }
        buffer[length] = ch;
        length++;
    }
    buffer[length] = '\0'; // Adiciona o terminador nulo
    return buffer;
}

// Função para alocar o documento com uma capacidade inicial
void allocateDocument(int initialCapacity) {
    document = new char*[initialCapacity];
    capacity = initialCapacity;
    numLines = 0;
}

// Função para desalocar o documento e liberar memória
void deallocateDocument() {
    for (int i = 0; i < numLines; i++) {
        delete[] document[i]; // Deleta cada linha
    }
    delete[] document; // Deleta o array de ponteiros
    document = nullptr;
    capacity = 0;
    numLines = 0;
}

// Função para inserir uma nova linha em uma posição específica
void insertLine(int position, const char* newLine) {
    if (position < 0 || position > numLines) {
        cout << "Posição inválida.\n";
        return;
    }
    if (numLines == capacity) {
        // Realoca o documento com maior capacidade
        int newCapacity = capacity * 2;
        char** newDocument = new char*[newCapacity];
        for (int i = 0; i < numLines; i++) {
            newDocument[i] = document[i];
        }
        delete[] document;
        document = newDocument;
        capacity = newCapacity;
    }
    // Desloca as linhas após a posição para baixo
    for (int i = numLines; i > position; i--) {
        document[i] = document[i - 1];
    }
    // Aloca memória para a nova linha
    int lineLength = stringLength(newLine);
    document[position] = new char[lineLength + 1];
    copyString(document[position], newLine); // Copia a nova linha para o documento
    numLines++;
}

// Função para remover uma linha em uma posição específica
void removeLine(int position) {
    if (position < 0 || position >= numLines) {
        cout << "Posição inválida.\n";
        return;
    }
    // Deleta a linha na posição
    delete[] document[position];
    // Desloca as linhas após a posição para cima
    for (int i = position; i < numLines - 1; i++) {
        document[i] = document[i + 1];
    }
    numLines--;
}

// Função para editar uma linha em uma posição específica
void editLine(int position, const char* newLine) {
    if (position < 0 || position >= numLines) {
        cout << "Posição inválida.\n";
        return;
    }
    // Deleta a linha antiga
    delete[] document[position];
    // Aloca memória para a nova linha
    int lineLength = stringLength(newLine);
    document[position] = new char[lineLength + 1];
    copyString(document[position], newLine); // Copia a nova linha para o documento
}

// Função para buscar uma palavra-chave em todas as linhas
void searchKeyword(const char* keyword) {
    bool found = false;
    for (int i = 0; i < numLines; i++) {
        if (findSubstring(document[i], keyword) != -1) {
            cout << "Encontrado na linha " << i + 1 << ": " << document[i] << "\n";
            found = true;
        }
    }
    if (!found) {
        cout << "Palavra-chave não encontrada.\n";
    }
}

// Função para imprimir o documento inteiro
void printDocument() {
    for (int i = 0; i < numLines; i++) {
        cout << i + 1 << ": " << document[i] << "\n";
    }
}

int main() {
    allocateDocument(10); // Inicializa o documento com capacidade 10
    bool running = true;
    while (running) {
        // Exibe o menu
        cout << "\nEditor de Texto Simples\n";
        cout << "1. Inserir linha\n";
        cout << "2. Remover linha\n";
        cout << "3. Editar linha\n";
        cout << "4. Buscar palavra-chave\n";
        cout << "5. Imprimir documento\n";
        cout << "6. Sair\n";
        cout << "Escolha uma opção: ";
        int choice;
        cin >> choice;
        cin.ignore(); // Limpa o caractere de nova linha do buffer de entrada

        int pos;         // Posição para operações de linha
        char* newLine;   // Ponteiro para a nova linha
        char* keyword;   // Ponteiro para a palavra-chave

        switch (choice) {
            case 1:
                // Insere uma nova linha
                cout << "Posição para inserir (1 a " << numLines + 1 << "): ";
                cin >> pos;
                cin.ignore();
                cout << "Digite o texto da nova linha:\n";
                newLine = readLine();
                insertLine(pos - 1, newLine); // Ajusta a posição para índice baseado em 0
                delete[] newLine; // Libera a memória alocada por readLine
                break;
            case 2:
                // Remove uma linha
                cout << "Posição da linha para remover (1 a " << numLines << "): ";
                cin >> pos;
                cin.ignore();
                removeLine(pos - 1); // Ajusta a posição para índice baseado em 0
                break;
            case 3:
                // Edita uma linha
                cout << "Posição da linha para editar (1 a " << numLines << "): ";
                cin >> pos;
                cin.ignore();
                cout << "Digite o novo texto da linha:\n";
                newLine = readLine();
                editLine(pos - 1, newLine); // Ajusta a posição para índice baseado em 0
                delete[] newLine; // Libera a memória alocada por readLine
                break;
            case 4:
                // Busca por uma palavra-chave
                cout << "Digite a palavra-chave para buscar: ";
                keyword = readLine();
                searchKeyword(keyword);
                delete[] keyword; // Libera a memória alocada por readLine
                break;
            case 5:
                // Imprime o documento
                printDocument();
                break;
            case 6:
                // Sai do programa
                running = false;
                break;
            default:
                cout << "Opção inválida.\n";
                break;
        }
    }
    deallocateDocument(); // Libera toda a memória alocada antes de encerrar
    return 0;
}

```
</details>




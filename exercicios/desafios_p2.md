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
Esta matriz contém 5 ilhas.

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

## 5. Editor de Texto Simples

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

## 6. Jogo da Velha Dinâmico

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


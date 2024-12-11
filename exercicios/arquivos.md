# Lista de Exercícios de Arquivos em C++

Antes de mergulhar nas soluções, lembre-se: a melhor maneira de aprender programação é fazendo por conta própria. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Escrita Básica em Arquivo ⭐
**Objetivo:** Crie um programa que escreva uma frase simples em um arquivo texto.

**Exemplo:**
Saída esperada no arquivo "mensagem.txt":
```
Olá, este é meu primeiro arquivo em C++!
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream arquivo("mensagem.txt");
    
    if (arquivo.is_open()) {
        arquivo << "Olá, este é meu primeiro arquivo em C++!" << std::endl;
        arquivo.close();
        std::cout << "Arquivo criado com sucesso!" << std::endl;
    } else {
        std::cout << "Erro ao abrir o arquivo." << std::endl;
    }

    return 0;
}
```

</details>

### 2. Leitura Básica de Arquivo ⭐
**Objetivo:** Leia e exiba o conteúdo de um arquivo texto linha por linha.

**Exemplo:**
Para um arquivo contendo:
```
Primeira linha
Segunda linha
Terceira linha
```

Saída esperada:
```
Conteúdo do arquivo:
1: Primeira linha
2: Segunda linha
3: Terceira linha
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ifstream arquivo("texto.txt");
    std::string linha;
    int numeroLinha = 1;

    if (arquivo.is_open()) {
        std::cout << "Conteúdo do arquivo:" << std::endl;
        while (std::getline(arquivo, linha)) {
            std::cout << numeroLinha << ": " << linha << std::endl;
            numeroLinha++;
        }
        arquivo.close();
    } else {
        std::cout << "Erro ao abrir o arquivo." << std::endl;
    }

    return 0;
}
```

</details>

### 3. Registro de Notas ⭐⭐
**Objetivo:** Crie um programa que permita ao usuário registrar nomes e notas de alunos em um arquivo, e depois leia e calcule a média.

**Exemplo:**
Entrada: João 8.5, Maria 9.0, Pedro 7.5
Saída esperada no arquivo "notas.txt":
```
João 8.5
Maria 9.0
Pedro 7.5
```
E no console:
```
Média da turma: 8.33
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>

int main() {
    std::ofstream arquivoSaida("notas.txt");
    std::string nome;
    float nota;
    int contador = 0;
    
    // Escrita no arquivo
    while (true) {
        std::cout << "Digite o nome do aluno (ou 'fim' para terminar): ";
        std::cin >> nome;
        if (nome == "fim") break;
        
        std::cout << "Digite a nota: ";
        std::cin >> nota;
        
        arquivoSaida << nome << " " << nota << std::endl;
        contador++;
    }
    arquivoSaida.close();
    
    // Leitura e cálculo da média
    std::ifstream arquivoEntrada("notas.txt");
    float soma = 0.0;
    contador = 0;
    
    while (arquivoEntrada >> nome >> nota) {
        soma += nota;
        contador++;
    }
    
    if (contador > 0) {
        float media = soma / contador;
        std::cout << std::fixed << std::setprecision(2);
        std::cout << "Média da turma: " << media << std::endl;
    }
    
    arquivoEntrada.close();
    return 0;
}
```

</details>

### 4. Modo Append ⭐⭐
**Objetivo:** Crie um programa que permita ao usuário adicionar novas entradas de texto ao final de um arquivo sem sobrescrever o conteúdo existente.

**Exemplo:**
Saída esperada em "notas.txt" após múltiplas execuções:
```
Primeira execução: Olá, este é um teste
Segunda execução: Adicionando mais uma linha
Terceira execução: Mais um texto no final
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ofstream arquivo("notas.txt", std::ios::app);
    
    if (arquivo.is_open()) {
        std::string texto;
        std::cout << "Digite o texto para adicionar ao arquivo: ";
        std::getline(std::cin, texto);
        
        arquivo << texto << std::endl;
        arquivo.close();
        
        std::cout << "Texto adicionado com sucesso!" << std::endl;
        
        // Mostrar o conteúdo atual do arquivo
        std::ifstream leitura("notas.txt");
        std::string linha;
        
        std::cout << "\nConteúdo atual do arquivo:" << std::endl;
        while (std::getline(leitura, linha)) {
            std::cout << linha << std::endl;
        }
        leitura.close();
    } else {
        std::cout << "Erro ao abrir o arquivo." << std::endl;
    }

    return 0;
}
```

</details>

### 5. Arquivo Binário com Struct ⭐⭐⭐
**Objetivo:** Crie um programa que armazene uma lista de produtos (código, nome, preço) em um arquivo binário e depois permita a leitura desses dados.

**Exemplo:**
Saída esperada após leitura:
```
Produtos cadastrados:
1. Código: 001, Nome: Teclado, Preço: R$ 89.90
2. Código: 002, Nome: Mouse, Preço: R$ 49.90
3. Código: 003, Nome: Monitor, Preço: R$ 899.90
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>

struct Produto {
    char codigo[4];
    char nome[50];
    double preco;
};

void escreverProduto(std::ofstream& arquivo, const Produto& prod) {
    arquivo.write(reinterpret_cast<const char*>(&prod), sizeof(Produto));
}

void lerProdutos(const std::string& nomeArquivo) {
    std::ifstream arquivo(nomeArquivo, std::ios::binary);
    Produto prod;
    int contador = 1;
    
    std::cout << "Produtos cadastrados:" << std::endl;
    while (arquivo.read(reinterpret_cast<char*>(&prod), sizeof(Produto))) {
        std::cout << contador << ". Código: " << prod.codigo
                 << ", Nome: " << prod.nome
                 << ", Preço: R$ " << std::fixed << std::setprecision(2) << prod.preco
                 << std::endl;
        contador++;
    }
    arquivo.close();
}

int main() {
    std::ofstream arquivoSaida("produtos.dat", std::ios::binary);
    
    // Cadastrar alguns produtos
    Produto produtos[] = {
        {"001", "Teclado", 89.90},
        {"002", "Mouse", 49.90},
        {"003", "Monitor", 899.90}
    };
    
    for (const auto& prod : produtos) {
        escreverProduto(arquivoSaida, prod);
    }
    arquivoSaida.close();
    
    // Ler e mostrar os produtos
    lerProdutos("produtos.dat");
    
    return 0;
}
```

</details>

### 6. Manipulação de Arquivos ⭐⭐
**Objetivo:** Crie um programa que copie o conteúdo de um arquivo para outro, contando o número de linhas e caracteres.

**Exemplo:**
Para um arquivo "origem.txt" contendo:
```
Hello
World
2024
```

Saída esperada:
```
Arquivo copiado com sucesso!
Número de linhas: 3
Número de caracteres: 14
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ifstream origem("origem.txt");
    std::ofstream destino("destino.txt");
    
    if (!origem || !destino) {
        std::cout << "Erro ao abrir os arquivos." << std::endl;
        return 1;
    }
    
    std::string linha;
    int numLinhas = 0;
    int numCaracteres = 0;
    
    while (std::getline(origem, linha)) {
        destino << linha << std::endl;
        numLinhas++;
        numCaracteres += linha.length();
    }
    
    origem.close();
    destino.close();
    
    std::cout << "Arquivo copiado com sucesso!" << std::endl;
    std::cout << "Número de linhas: " << numLinhas << std::endl;
    std::cout << "Número de caracteres: " << numCaracteres << std::endl;
    
    return 0;
}
```

</details>

### 7. Busca em Arquivo ⭐⭐
**Objetivo:** Implemente um programa que procure por uma palavra em um arquivo texto e mostre as linhas onde ela aparece.

**Exemplo:**
Para buscar a palavra "teste" no arquivo, saída esperada:
```
Encontrado "teste" nas seguintes linhas:
2: Este é um teste de busca
5: Outro teste aqui
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

void buscarPalavra(const std::string& nomeArquivo, const std::string& palavra) {
    std::ifstream arquivo(nomeArquivo);
    std::string linha;
    int numeroLinha = 1;
    bool encontrou = false;
    
    std::cout << "Encontrado \"" << palavra << "\" nas seguintes linhas:" << std::endl;
    
    while (std::getline(arquivo, linha)) {
        if (linha.find(palavra) != std::string::npos) {
            std::cout << numeroLinha << ": " << linha << std::endl;
            encontrou = true;
        }
        numeroLinha++;
    }
    
    if (!encontrou) {
        std::cout << "Palavra não encontrada no arquivo." << std::endl;
    }
    
    arquivo.close();
}

int main() {
    std::string palavra;
    std::cout << "Digite a palavra a ser buscada: ";
    std::cin >> palavra;
    
    buscarPalavra("texto.txt", palavra);
    
    return 0;
}
```

</details>

### 8. Mesclagem de Arquivos ⭐⭐⭐
**Objetivo:** Crie um programa que mescle dois arquivos ordenados em um terceiro arquivo, mantendo a ordenação.

**Exemplo:**
Arquivo1.txt:
```
1
3
5
```
Arquivo2.txt:
```
2
4
6
```
Saída esperada em "mesclado.txt":
```
1
2
3
4
5
6
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

void mesclarArquivos(const std::string& arquivo1, const std::string& arquivo2, 
                     const std::string& arquivoSaida) {
    std::ifstream f1(arquivo1);
    std::ifstream f2(arquivo2);
    std::ofstream saida(arquivoSaida);
    
    if (!f1 || !f2 || !saida) {
        std::cout << "Erro ao abrir os arquivos." << std::endl;
        return;
    }
    
    int num1, num2;
    bool tem1 = (f1 >> num1);
    bool tem2 = (f2 >> num2);
    
    while (tem1 && tem2) {
        if (num1 <= num2) {
            saida << num1 << std::endl;
            tem1 = (f1 >> num1);
        } else {
            saida << num2 << std::endl;
            tem2 = (f2 >> num2);
        }
    }
    
    // Copiar números restantes do arquivo 1
    while (tem1) {
        saida << num1 << std::endl;
        tem1 = (f1 >> num1);
    }
    
    // Copiar números restantes do arquivo 2
    while (tem2) {
        saida << num2 << std::endl;
        tem2 = (f2 >> num2);
    }
    
    f1.close();
    f2.close();
    saida.close();
    
    std::cout << "Arquivos mesclados com sucesso!" << std::endl;
}

int main() {
    mesclarArquivos("arquivo1.txt", "arquivo2.txt", "mesclado.txt");
    return 0;
}
```

</details>

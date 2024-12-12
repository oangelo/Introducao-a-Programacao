# Lista de Exercícios de Revisão em C++

Antes de começar, lembre-se: tente resolver os exercícios por conta própria primeiro. É normal encontrar dificuldades - elas são parte importante do aprendizado. Só consulte as soluções depois de tentar resolver sozinho ou quando quiser comparar sua solução.

### 1. Sistema de Notas Básico ⭐
**Objetivo:** Crie um programa que permita registrar notas de alunos em um arquivo texto. Cada linha do arquivo deve conter o nome do aluno e sua nota.

**Exemplo:**
Entrada: "João 8.5", "Maria 9.0"
Arquivo "notas.txt":
```
João 8.5
Maria 9.0
```
**Conceitos revisados:** Arquivos (escrita básica), strings

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ofstream arquivo("notas.txt");
    std::string nome;
    float nota;
    char continuar;
    
    if (!arquivo.is_open()) {
        std::cout << "Erro ao abrir o arquivo!" << std::endl;
        return 1;
    }
    
    do {
        std::cout << "Nome do aluno: ";
        std::cin >> nome;
        std::cout << "Nota: ";
        std::cin >> nota;
        
        arquivo << nome << " " << nota << std::endl;
        
        std::cout << "Deseja continuar? (s/n): ";
        std::cin >> continuar;
    } while (continuar == 's' || continuar == 'S');
    
    arquivo.close();
    return 0;
}
```
</details>

### 2. Calculadora com Menu ⭐⭐
**Objetivo:** Implemente uma calculadora que use ponteiros para funções para realizar operações básicas (soma, subtração, multiplicação, divisão). O programa deve mostrar um menu e salvar o histórico das operações em um arquivo.

**Exemplo:**
Saída esperada:
```
1. Soma
2. Subtração
3. Multiplicação
4. Divisão
Escolha: 1
Digite dois números: 5 3
Resultado: 8
```
Arquivo "historico.txt":
```
Operação: Soma
5 + 3 = 8
```
**Conceitos revisados:** Ponteiros para funções, arquivos (escrita), estruturas de controle

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>

float soma(float a, float b) { return a + b; }
float subtracao(float a, float b) { return a - b; }
float multiplicacao(float a, float b) { return a * b; }
float divisao(float a, float b) { return b != 0 ? a / b : 0; }

void salvarHistorico(const char* operacao, float a, float b, float resultado) {
    std::ofstream arquivo("historico.txt", std::ios::app);
    arquivo << "Operação: " << operacao << std::endl;
    arquivo << a << " " << operacao << " " << b << " = " << resultado << std::endl;
    arquivo.close();
}

int main() {
    float (*operacoes[])(float, float) = {soma, subtracao, multiplicacao, divisao};
    const char* nomes[] = {"+", "-", "*", "/"};
    
    float a, b;
    int escolha;
    
    do {
        std::cout << "1. Soma\n2. Subtração\n3. Multiplicação\n4. Divisão\n0. Sair\n";
        std::cout << "Escolha: ";
        std::cin >> escolha;
        
        if (escolha >= 1 && escolha <= 4) {
            std::cout << "Digite dois números: ";
            std::cin >> a >> b;
            
            float resultado = operacoes[escolha-1](a, b);
            std::cout << "Resultado: " << resultado << std::endl;
            
            salvarHistorico(nomes[escolha-1], a, b, resultado);
        }
    } while (escolha != 0);
    
    return 0;
}
```
</details>

### 3. Sistema de Cadastro de Produtos ⭐⭐
**Objetivo:** Crie um sistema que permita cadastrar produtos (código, nome, preço) em um arquivo. O programa deve permitir adicionar novos produtos e listar todos os produtos cadastrados.

**Exemplo:**
Entrada: Produto(001, "Teclado", 89.90)
Arquivo "produtos.txt":
```
001 Teclado 89.90
```
**Conceitos revisados:** Estruturas, arquivos (escrita/leitura), formatação

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <iomanip>

struct Produto {
    char codigo[4];
    char nome[50];
    float preco;
};

void cadastrarProduto() {
    Produto prod;
    std::ofstream arquivo("produtos.txt", std::ios::app);
    
    std::cout << "Código (3 dígitos): ";
    std::cin >> prod.codigo;
    std::cout << "Nome: ";
    std::cin.ignore();
    std::cin.getline(prod.nome, 50);
    std::cout << "Preço: ";
    std::cin >> prod.preco;
    
    arquivo << prod.codigo << " "
            << prod.nome << " "
            << std::fixed << std::setprecision(2) << prod.preco << std::endl;
            
    arquivo.close();
}

void listarProdutos() {
    std::ifstream arquivo("produtos.txt");
    Produto prod;
    std::string linha;
    
    std::cout << "\nProdutos cadastrados:\n";
    while (std::getline(arquivo, linha)) {
        std::cout << linha << std::endl;
    }
    arquivo.close();
}

int main() {
    int opcao;
    do {
        std::cout << "\n1. Cadastrar Produto\n2. Listar Produtos\n0. Sair\n";
        std::cout << "Escolha: ";
        std::cin >> opcao;
        
        switch(opcao) {
            case 1: cadastrarProduto(); break;
            case 2: listarProdutos(); break;
        }
    } while (opcao != 0);
    
    return 0;
}
```
</details>

### 4. Sistema de Filtragem de Dados ⭐⭐⭐
**Objetivo:** Crie um programa que leia dados de alunos de um arquivo e aplique diferentes filtros (usando ponteiros para funções) para gerar relatórios específicos.

**Exemplo:**
Arquivo de entrada "alunos.txt":
```
João 8.5 75
Maria 9.0 95
Pedro 7.0 85
```
Saída com filtro de aprovados (nota >= 7.0 e frequência >= 75):
```
Alunos aprovados:
João (8.5, 75%)
Maria (9.0, 95%)
Pedro (7.0, 85%)
```
**Conceitos revisados:** Estruturas, arquivos (leitura), ponteiros para funções, processamento de dados

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

struct Aluno {
    char nome[50];
    float nota;
    int frequencia;
};

typedef bool (*Filtro)(const Aluno&);

bool filtroAprovados(const Aluno& aluno) {
    return aluno.nota >= 7.0 && aluno.frequencia >= 75;
}

bool filtroRecuperacao(const Aluno& aluno) {
    return aluno.nota >= 5.0 && aluno.nota < 7.0 && aluno.frequencia >= 75;
}

void processarAlunos(const char* nomeArquivo, Filtro filtro, const char* descricao) {
    std::ifstream arquivo(nomeArquivo);
    Aluno aluno;
    
    std::cout << descricao << ":\n";
    while (arquivo >> aluno.nome >> aluno.nota >> aluno.frequencia) {
        if (filtro(aluno)) {
            std::cout << aluno.nome << " ("
                     << aluno.nota << ", "
                     << aluno.frequencia << "%)\n";
        }
    }
    arquivo.close();
}

int main() {
    int opcao;
    do {
        std::cout << "\n1. Listar Aprovados\n"
                  << "2. Listar Recuperação\n"
                  << "0. Sair\n"
                  << "Escolha: ";
        std::cin >> opcao;
        
        switch(opcao) {
            case 1:
                processarAlunos("alunos.txt", filtroAprovados, "Alunos aprovados");
                break;
            case 2:
                processarAlunos("alunos.txt", filtroRecuperacao, "Alunos em recuperação");
                break;
        }
    } while (opcao != 0);
    
    return 0;
}
```
</details>

### 5. Agenda de Contatos ⭐⭐⭐
**Objetivo:** Desenvolva uma agenda que permita adicionar, buscar e listar contatos. Os contatos devem ser salvos em arquivo e o programa deve oferecer diferentes opções de ordenação.

**Exemplo:**
Menu:
```
1. Adicionar Contato
2. Buscar Contato
3. Listar Contatos (A-Z)
4. Listar Contatos (Z-A)
0. Sair
```
**Conceitos revisados:** Estruturas, arquivos (leitura/escrita), ponteiros para funções (ordenação), busca

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <fstream>
#include <string>

struct Contato {
    char nome[50];
    char telefone[15];
    char email[50];
};

void adicionarContato() {
    Contato c;
    std::ofstream arquivo("contatos.txt", std::ios::app);
    
    std::cout << "Nome: ";
    std::cin.ignore();
    std::cin.getline(c.nome, 50);
    std::cout << "Telefone: ";
    std::cin.getline(c.telefone, 15);
    std::cout << "Email: ";
    std::cin.getline(c.email, 50);
    
    arquivo << c.nome << ";" << c.telefone << ";" << c.email << std::endl;
    arquivo.close();
}

void buscarContato() {
    std::string busca;
    std::cout << "Digite o nome a buscar: ";
    std::cin.ignore();
    std::getline(std::cin, busca);
    
    std::ifstream arquivo("contatos.txt");
    std::string linha;
    bool encontrou = false;
    
    while (std::getline(arquivo, linha)) {
        if (linha.find(busca) != std::string::npos) {
            std::cout << linha << std::endl;
            encontrou = true;
        }
    }
    
    if (!encontrou) {
        std::cout << "Contato não encontrado.\n";
    }
    arquivo.close();
}

void listarContatos(bool crescente) {
    std::ifstream arquivo("contatos.txt");
    std::string linhas[100];  // Limitado a 100 contatos para simplificar
    int numLinhas = 0;
    
    while (std::getline(arquivo, linhas[numLinhas]) && numLinhas < 100) {
        numLinhas++;
    }
    arquivo.close();
    
    // Ordenação simples (bubble sort)
    for (int i = 0; i < numLinhas-1; i++) {
        for (int j = 0; j < numLinhas-i-1; j++) {
            if (crescente ? linhas[j] > linhas[j+1] : linhas[j] < linhas[j+1]) {
                std::string temp = linhas[j];
                linhas[j] = linhas[j+1];
                linhas[j+1] = temp;
            }
        }
    }
    
    for (int i = 0; i < numLinhas; i++) {
        std::cout << linhas[i] << std::endl;
    }
}

int main() {
    int opcao;
    do {
        std::cout << "\n1. Adicionar Contato\n"
                  << "2. Buscar Contato\n"
                  << "3. Listar Contatos (A-Z)\n"
                  << "4. Listar Contatos (Z-A)\n"
                  << "0. Sair\n"
                  << "Escolha: ";
        std::cin >> opcao;
        
        switch(opcao) {
            case 1: adicionarContato(); break;
            case 2: buscarContato(); break;
            case 3: listarContatos(true); break;
            case 4: listarContatos(false); break;
        }
    } while (opcao != 0);
    
    return 0;
}
```
</details>

### Sugestões para Prática Adicional

1. Modifique o Sistema de Notas para calcular e salvar estatísticas (média, maior nota, menor nota)
2. Adicione validação de dados em todos os programas
3. Implemente funções de edição e remoção no Sistema de Cadastro de Produtos
4. Adicione mais filtros no Sistema de Filtragem de Dados
5. Expanda a Agenda de Contatos para incluir mais campos e opções de busca

### Dicas Gerais

1. Sempre verifique se os arquivos foram abertos corretamente
2. Feche os arquivos após usar
3. Valide as entradas do usuário
4. Trate casos especiais (divisão por zero, arquivo vazio, etc.)
5. Use funções para organizar melhor o código

# Lista de Exercícios de Estruturas em C++

Antes de mergulhar nas soluções, lembre-se: a melhor maneira de aprender programação é fazendo por conta própria. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Criação e Uso Básico de Estruturas ⭐
**Objetivo:** Crie uma estrutura para representar um ponto no plano cartesiano (x, y) e calcule a distância deste ponto até a origem.

**Exemplo:**
Entrada: x = 3, y = 4
Saída esperada:
```
Coordenadas do ponto: (3, 4)
Distância até a origem: 5
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cmath>

struct Ponto {
    double x;
    double y;
};

double distanciaOrigem(Ponto p) {
    return sqrt(p.x * p.x + p.y * p.y);
}

int main() {
    Ponto p;
    std::cout << "Digite as coordenadas (x y): ";
    std::cin >> p.x >> p.y;

    std::cout << "Coordenadas do ponto: (" << p.x << ", " << p.y << ")" << std::endl;
    std::cout << "Distância até a origem: " << distanciaOrigem(p) << std::endl;

    return 0;
}
```

</details>

### 2. Array de Estruturas ⭐⭐
**Objetivo:** Crie uma estrutura Aluno com nome e nota, e implemente um programa que calcule a média das notas de uma turma.

**Exemplo:**
Entrada: 3 alunos - ("Ana", 9.5), ("Pedro", 8.0), ("Maria", 9.0)
Saída esperada:
```
Lista de Alunos:
Ana: 9.5
Pedro: 8.0
Maria: 9.0
Média da turma: 8.83
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <string>
#include <iomanip>

struct Aluno {
    std::string nome;
    double nota;
};

int main() {
    int n;
    std::cout << "Digite o número de alunos: ";
    std::cin >> n;
    
    Aluno* turma = new Aluno[n];
    
    for(int i = 0; i < n; i++) {
        std::cout << "Nome do aluno " << i+1 << ": ";
        std::cin >> turma[i].nome;
        std::cout << "Nota: ";
        std::cin >> turma[i].nota;
    }
    
    double soma = 0;
    std::cout << "\nLista de Alunos:" << std::endl;
    for(int i = 0; i < n; i++) {
        std::cout << turma[i].nome << ": " << turma[i].nota << std::endl;
        soma += turma[i].nota;
    }
    
    double media = soma / n;
    std::cout << "Média da turma: " << std::fixed << std::setprecision(2) << media << std::endl;
    
    delete[] turma;
    return 0;
}
```

</details>

### 3. Estruturas Aninhadas ⭐⭐
**Objetivo:** Crie uma estrutura Endereço e uma estrutura Pessoa que contenha um Endereço, e implemente uma função para imprimir os dados completos.

**Exemplo:**
Saída esperada:
```
Dados da Pessoa:
Nome: João Silva
Idade: 30
Endereço:
  Rua das Flores, 123
  São Paulo - SP
  CEP: 01234-567
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <string>

struct Endereco {
    std::string rua;
    int numero;
    std::string cidade;
    std::string estado;
    std::string cep;
};

struct Pessoa {
    std::string nome;
    int idade;
    Endereco endereco;
};

void imprimirPessoa(const Pessoa& p) {
    std::cout << "Dados da Pessoa:" << std::endl;
    std::cout << "Nome: " << p.nome << std::endl;
    std::cout << "Idade: " << p.idade << std::endl;
    std::cout << "Endereço:" << std::endl;
    std::cout << "  " << p.endereco.rua << ", " << p.endereco.numero << std::endl;
    std::cout << "  " << p.endereco.cidade << " - " << p.endereco.estado << std::endl;
    std::cout << "  CEP: " << p.endereco.cep << std::endl;
}

int main() {
    Pessoa pessoa;
    pessoa.nome = "João Silva";
    pessoa.idade = 30;
    pessoa.endereco.rua = "Rua das Flores";
    pessoa.endereco.numero = 123;
    pessoa.endereco.cidade = "São Paulo";
    pessoa.endereco.estado = "SP";
    pessoa.endereco.cep = "01234-567";
    
    imprimirPessoa(pessoa);
    
    return 0;
}
```

</details>

### 4. Funções com Estruturas ⭐⭐
**Objetivo:** Crie uma estrutura Retângulo com largura e altura, e implemente funções para calcular área e perímetro.

**Exemplo:**
Entrada: largura = 5, altura = 3
Saída esperada:
```
Dimensões do retângulo: 5 x 3
Área: 15
Perímetro: 16
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

struct Retangulo {
    double largura;
    double altura;
};

double calcularArea(const Retangulo& r) {
    return r.largura * r.altura;
}

double calcularPerimetro(const Retangulo& r) {
    return 2 * (r.largura + r.altura);
}

int main() {
    Retangulo ret;
    std::cout << "Digite a largura do retângulo: ";
    std::cin >> ret.largura;
    std::cout << "Digite a altura do retângulo: ";
    std::cin >> ret.altura;
    
    std::cout << "Dimensões do retângulo: " << ret.largura << " x " << ret.altura << std::endl;
    std::cout << "Área: " << calcularArea(ret) << std::endl;
    std::cout << "Perímetro: " << calcularPerimetro(ret) << std::endl;
    
    return 0;
}
```

</details>

### 5. Comparação de Estruturas ⭐⭐⭐
**Objetivo:** Crie uma estrutura Data com dia, mês e ano, e implemente uma função que compare duas datas.

**Exemplo:**
Entrada: Data1 (1/5/2023), Data2 (15/3/2023)
Saída esperada:
```
Data 1: 01/05/2023
Data 2: 15/03/2023
Data 2 é anterior à Data 1
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <iomanip>

struct Data {
    int dia;
    int mes;
    int ano;
};

// Retorna -1 se d1 é anterior, 0 se igual, 1 se d1 é posterior
int compararDatas(const Data& d1, const Data& d2) {
    if (d1.ano < d2.ano) return -1;
    if (d1.ano > d2.ano) return 1;
    
    if (d1.mes < d2.mes) return -1;
    if (d1.mes > d2.mes) return 1;
    
    if (d1.dia < d2.dia) return -1;
    if (d1.dia > d2.dia) return 1;
    
    return 0;
}

void imprimirData(const Data& d) {
    std::cout << std::setfill('0') << std::setw(2) << d.dia << "/"
              << std::setfill('0') << std::setw(2) << d.mes << "/"
              << d.ano;
}

int main() {
    Data data1, data2;
    
    std::cout << "Digite a primeira data (dia mes ano): ";
    std::cin >> data1.dia >> data1.mes >> data1.ano;
    
    std::cout << "Digite a segunda data (dia mes ano): ";
    std::cin >> data2.dia >> data2.mes >> data2.ano;
    
    std::cout << "Data 1: ";
    imprimirData(data1);
    std::cout << "\nData 2: ";
    imprimirData(data2);
    std::cout << std::endl;
    
    int resultado = compararDatas(data1, data2);
    if (resultado < 0) {
        std::cout << "Data 1 é anterior à Data 2" << std::endl;
    } else if (resultado > 0) {
        std::cout << "Data 1 é posterior à Data 2" << std::endl;
    } else {
        std::cout << "As datas são iguais" << std::endl;
    }
    
    return 0;
}
```

</details>

### 6. Estruturas com Alocação Dinâmica ⭐⭐⭐
**Objetivo:** Crie uma estrutura Livro e implemente um sistema simples de biblioteca que permita adicionar e listar livros.

**Exemplo:**
Saída esperada:
```
Biblioteca:
1. "Dom Casmurro" - Machado de Assis (1899)
2. "Grande Sertão: Veredas" - Guimarães Rosa (1956)
Total de livros: 2
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <string>

struct Livro {
    std::string titulo;
    std::string autor;
    int ano;
};

struct Biblioteca {
    Livro* livros;
    int quantidade;
    int capacidade;
};

void inicializarBiblioteca(Biblioteca& bib, int capacidadeInicial = 10) {
    bib.livros = new Livro[capacidadeInicial];
    bib.quantidade = 0;
    bib.capacidade = capacidadeInicial;
}

void adicionarLivro(Biblioteca& bib, const Livro& livro) {
    if (bib.quantidade >= bib.capacidade) {
        // Aumentar capacidade
        int novaCapacidade = bib.capacidade * 2;
        Livro* novosLivros = new Livro[novaCapacidade];
        
        for (int i = 0; i < bib.quantidade; i++) {
            novosLivros[i] = bib.livros[i];
        }
        
        delete[] bib.livros;
        bib.livros = novosLivros;
        bib.capacidade = novaCapacidade;
    }
    
    bib.livros[bib.quantidade++] = livro;
}

void listarLivros(const Biblioteca& bib) {
    std::cout << "Biblioteca:" << std::endl;
    for (int i = 0; i < bib.quantidade; i++) {
        std::cout << i+1 << ". \"" << bib.livros[i].titulo << "\" - "
                 << bib.livros[i].autor << " (" << bib.livros[i].ano << ")" << std::endl;
    }
    std::cout << "Total de livros: " << bib.quantidade << std::endl;
}

int main() {
    Biblioteca bib;
    inicializarBiblioteca(bib);
    
    Livro livro1 = {"Dom Casmurro", "Machado de Assis", 1899};
    Livro livro2 = {"Grande Sertão: Veredas", "Guimarães Rosa", 1956};
    
    adicionarLivro(bib, livro1);
    adicionarLivro(bib, livro2);
    
    listarLivros(bib);
    
    delete[] bib.livros;
    return 0;
}
```

</details>

### 7. Estruturas com Vetores ⭐⭐
**Objetivo:** Crie uma estrutura Aluno que armazene notas em um vetor e calcule a média ponderada.

**Exemplo:**
Entrada: 3 notas (7.5, 8.0, 9.0) com pesos (2, 3, 5)
Saída esperada:
```
Notas do aluno João:
Prova 1: 7.5 (peso 2)
Prova 2: 8.0 (peso 3)
Prova 3: 9.0 (peso 5)
Média ponderada: 8.45
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <iomanip>

struct Aluno {
    std::string nome;
    std::vector<double> notas;
    std::vector<int> pesos;
};

double calcularMediaPonderada(const Aluno& aluno) {
    double somaNotas = 0;
    int somaPesos = 0;
    
    for(size_t i = 0; i < aluno.notas.size(); i++) {
        somaNotas += aluno.notas[i] * aluno.pesos[i];
        somaPesos += aluno.pesos[i];
    }
    
    return somaNotas / somaPesos;
}

int main() {
    Aluno aluno;
    aluno.nome = "João";
    
    int numNotas;
    std::cout << "Digite o número de notas: ";
    std::cin >> numNotas;
    
    for(int i = 0; i < numNotas; i++) {
        double nota;
        int peso;
        std::cout << "Digite a nota " << i+1 << ": ";
        std::cin >> nota;
        std::cout << "Digite o peso da nota " << i+1 << ": ";
        std::cin >> peso;
        
        aluno.notas.push_back(nota);
        aluno.pesos.push_back(peso);
    }
    
    std::cout << "\nNotas do aluno " << aluno.nome << ":" << std::endl;
    for(size_t
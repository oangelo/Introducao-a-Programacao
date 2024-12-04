# Lista de Exercícios de Revisão - Estruturas e Ponteiros para Funções

Antes de começar, lembre-se: a melhor maneira de aprender programação é praticando. Tente resolver os exercícios sozinho antes de consultar as soluções. Comece pelos exercícios mais simples (⭐) e vá progredindo para os mais complexos.

### 1. Calculadora de Tempo ⭐
**Objetivo:** Crie uma estrutura Tempo com horas, minutos e segundos. Implemente funções para:
- Converter o tempo total para segundos
- Somar dois tempos
- Imprimir no formato HH:MM:SS

**Exemplo:**
```
Tempo 1: 02:30:45
Tempo 2: 01:15:30
Soma: 03:46:15
Total em segundos: 13575
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <iomanip>

struct Tempo {
    int horas;
    int minutos;
    int segundos;
};

int paraSegundos(const Tempo& t) {
    return t.horas * 3600 + t.minutos * 60 + t.segundos;
}

Tempo deSegundos(int total) {
    Tempo t;
    t.horas = total / 3600;
    total %= 3600;
    t.minutos = total / 60;
    t.segundos = total % 60;
    return t;
}

Tempo somarTempos(const Tempo& t1, const Tempo& t2) {
    int totalSegundos = paraSegundos(t1) + paraSegundos(t2);
    return deSegundos(totalSegundos);
}

void imprimirTempo(const Tempo& t) {
    std::cout << std::setfill('0') << std::setw(2) << t.horas << ":"
              << std::setfill('0') << std::setw(2) << t.minutos << ":"
              << std::setfill('0') << std::setw(2) << t.segundos;
}

int main() {
    Tempo t1 = {2, 30, 45};
    Tempo t2 = {1, 15, 30};
    
    std::cout << "Tempo 1: ";
    imprimirTempo(t1);
    std::cout << "\nTempo 2: ";
    imprimirTempo(t2);
    
    Tempo soma = somarTempos(t1, t2);
    std::cout << "\nSoma: ";
    imprimirTempo(soma);
    
    std::cout << "\nTotal em segundos: " << paraSegundos(soma) << std::endl;
    
    return 0;
}
```

</details>

### 2. Sistema de Notas ⭐
**Objetivo:** Desenvolva um programa que use uma estrutura Aluno (nome e 3 notas) e um array de ponteiros para funções para calcular diferentes médias:
- Média aritmética
- Média ponderada (pesos: 2, 3, 5)
- Maior nota

**Exemplo:**
```
Aluno: João
Notas: 7.5, 8.0, 9.0
Média aritmética: 8.17
Média ponderada: 8.45
Maior nota: 9.0
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <iomanip>
#include <cstring>

struct Aluno {
    char nome[50];
    float notas[3];
};

float calcularMediaAritmetica(const float notas[]) {
    return (notas[0] + notas[1] + notas[2]) / 3.0f;
}

float calcularMediaPonderada(const float notas[]) {
    return (notas[0] * 2 + notas[1] * 3 + notas[2] * 5) / 10.0f;
}

float encontrarMaiorNota(const float notas[]) {
    float maior = notas[0];
    for(int i = 1; i < 3; i++) {
        if(notas[i] > maior) maior = notas[i];
    }
    return maior;
}

int main() {
    typedef float (*Calculadora)(const float[]);
    Calculadora calculadoras[] = {
        calcularMediaAritmetica,
        calcularMediaPonderada,
        encontrarMaiorNota
    };
    
    Aluno aluno;
    std::cout << "Nome do aluno: ";
    std::cin >> aluno.nome;
    
    for(int i = 0; i < 3; i++) {
        std::cout << "Nota " << i+1 << ": ";
        std::cin >> aluno.notas[i];
    }
    
    std::cout << "\nAluno: " << aluno.nome << std::endl;
    std::cout << "Notas: " << aluno.notas[0] << ", " 
              << aluno.notas[1] << ", " << aluno.notas[2] << std::endl;
    
    std::cout << std::fixed << std::setprecision(2);
    std::cout << "Média aritmética: " << calculadoras[0](aluno.notas) << std::endl;
    std::cout << "Média ponderada: " << calculadoras[1](aluno.notas) << std::endl;
    std::cout << "Maior nota: " << calculadoras[2](aluno.notas) << std::endl;
    
    return 0;
}
```

</details>

### 3. Agenda Simplificada ⭐⭐
**Objetivo:** Crie uma estrutura Contato (nome, telefone, tipo) e implemente um sistema de agenda com as operações:
- Adicionar contato
- Buscar por nome
- Listar todos
- Listar por tipo (pessoal/trabalho)

**Exemplo:**
```
1. Adicionar Contato
2. Buscar Contato
3. Listar Todos
4. Listar por Tipo
5. Sair
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cstring>

const int MAX_CONTATOS = 100;

struct Contato {
    char nome[50];
    char telefone[15];
    int tipo; // 1-Pessoal, 2-Trabalho
};

struct Agenda {
    Contato contatos[MAX_CONTATOS];
    int quantidade;
};

void inicializarAgenda(Agenda& ag) {
    ag.quantidade = 0;
}

bool adicionarContato(Agenda& ag) {
    if(ag.quantidade >= MAX_CONTATOS) {
        std::cout << "Agenda cheia!" << std::endl;
        return false;
    }
    
    Contato novo;
    std::cout << "Nome: ";
    std::cin.ignore();
    std::cin.getline(novo.nome, 50);
    
    std::cout << "Telefone: ";
    std::cin.getline(novo.telefone, 15);
    
    std::cout << "Tipo (1-Pessoal, 2-Trabalho): ";
    std::cin >> novo.tipo;
    
    ag.contatos[ag.quantidade++] = novo;
    return true;
}

void buscarContato(const Agenda& ag) {
    char busca[50];
    std::cout << "Digite o nome para buscar: ";
    std::cin.ignore();
    std::cin.getline(busca, 50);
    
    bool encontrou = false;
    for(int i = 0; i < ag.quantidade; i++) {
        if(strstr(ag.contatos[i].nome, busca)) {
            std::cout << "\nNome: " << ag.contatos[i].nome 
                     << "\nTelefone: " << ag.contatos[i].telefone 
                     << "\nTipo: " << (ag.contatos[i].tipo == 1 ? "Pessoal" : "Trabalho")
                     << "\n" << std::endl;
            encontrou = true;
        }
    }
    
    if(!encontrou) {
        std::cout << "Nenhum contato encontrado." << std::endl;
    }
}

void listarTodos(const Agenda& ag) {
    if(ag.quantidade == 0) {
        std::cout << "Agenda vazia!" << std::endl;
        return;
    }
    
    for(int i = 0; i < ag.quantidade; i++) {
        std::cout << "\nContato " << i+1 << ":" 
                 << "\nNome: " << ag.contatos[i].nome
                 << "\nTelefone: " << ag.contatos[i].telefone
                 << "\nTipo: " << (ag.contatos[i].tipo == 1 ? "Pessoal" : "Trabalho")
                 << "\n";
    }
}

void listarPorTipo(const Agenda& ag) {
    int tipo;
    std::cout << "Tipo (1-Pessoal, 2-Trabalho): ";
    std::cin >> tipo;
    
    bool encontrou = false;
    for(int i = 0; i < ag.quantidade; i++) {
        if(ag.contatos[i].tipo == tipo) {
            std::cout << "\nNome: " << ag.contatos[i].nome 
                     << "\nTelefone: " << ag.contatos[i].telefone << "\n";
            encontrou = true;
        }
    }
    
    if(!encontrou) {
        std::cout << "Nenhum contato deste tipo." << std::endl;
    }
}

int main() {
    Agenda agenda;
    inicializarAgenda(agenda);
    
    int opcao;
    do {
        std::cout << "\n1. Adicionar Contato"
                 << "\n2. Buscar Contato"
                 << "\n3. Listar Todos"
                 << "\n4. Listar por Tipo"
                 << "\n5. Sair"
                 << "\nDigite sua opção: ";
        std::cin >> opcao;
        
        switch(opcao) {
            case 1: adicionarContato(agenda); break;
            case 2: buscarContato(agenda); break;
            case 3: listarTodos(agenda); break;
            case 4: listarPorTipo(agenda); break;
            case 5: std::cout << "Saindo..." << std::endl; break;
            default: std::cout << "Opção inválida!" << std::endl;
        }
    } while(opcao != 5);
    
    return 0;
}
```

</details>

### 4. Processador de Texto ⭐⭐
**Objetivo:** Implemente um sistema que processe texto usando um array de ponteiros para funções. Cada função deve realizar uma transformação simples:
- Converter para maiúsculas
- Remover espaços extras
- Contar palavras
- Inverter texto

**Exemplo:**
```
Texto original: "  Olá   mundo  !"
Após maiúsculas: "  OLÁ   MUNDO  !"
Após remover espaços: "OLÁ MUNDO!"
Número de palavras: 2
Texto invertido: "!ODNUM ÁLO"
```

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cstring>
#include <cctype>

const int MAX_TEXTO = 100;

char* converterMaiusculas(char* texto) {
    for(int i = 0; texto[i]; i++) {
        texto[i] = toupper(texto[i]);
    }
    return texto;
}

char* removerEspacosExtras(char* texto) {
    int leitura = 0, escrita = 0;
    bool espacoAnterior = true;  // Considera início como espaço
    
    while(texto[leitura]) {
        if(!isspace(texto[leitura])) {
            texto[escrita++] = texto[leitura];
            espacoAnterior = false;
        }
        else if(!espacoAnterior) {
            texto[escrita++] = ' ';
            espacoAnterior = true;
        }
        leitura++;
    }
    
    // Remove espaço no final se existir
    if(escrita > 0 && texto[escrita-1] == ' ') {
        escrita--;
    }
    
    texto[escrita] = '\0';
    return texto;
}

int contarPalavras(const char* texto) {
    int palavras = 0;
    bool emPalavra = false;
    
    for(int i = 0; texto[i]; i++) {
        if(!isspace(texto[i])) {
            if(!emPalavra) {
                palavras++;
                emPalavra = true;
            }
        } else {
            emPalavra = false;
        }
    }
    
    return palavras;
}

char* inverterTexto(char* texto) {
    int len = strlen(texto);
    for(int i = 0; i < len/2; i++) {
        char temp = texto[i];
        texto[i] = texto[len-1-i];
        texto[len-1-i] = temp;
    }
    return texto;
}

int main() {
    char texto[MAX_TEXTO];
    char textoProcessado[MAX_TEXTO];
    
    std::cout << "Digite um texto: ";
    std::cin.getline(texto, MAX_TEXTO);
    
    // Array de ponteiros para funções
    typedef char* (*ProcessadorTexto)(char*);
    ProcessadorTexto processadores[] = {
        converterMaiusculas,
        removerEspacosExtras,
        inverterTexto
    };
    
    std::cout << "Texto original: \"" << texto << "\"" << std::endl;
    
    // Processar texto com cada função
    strcpy(textoProcessado, texto);
    std::cout << "Após maiúsculas: \"" << processadores[0](textoProcessado) << "\"" << std::endl;
    
    strcpy(textoProcessado, texto);
    std::cout << "Após remover espaços: \"" << processadores[1](textoProcessado) << "\"" << std::endl;
    
    std::cout << "Número de palavras: " << contarPalavras(texto) << std::endl;
    
    strcpy(textoProcessado, texto);
    std::cout << "Texto invertido: \"" << processadores[2](textoProcessado) << "\"" << std::endl;
    
    return 0;
}
```

</details>


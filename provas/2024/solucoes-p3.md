// Questão 1 - Leitura e Escrita de Arquivos
#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>

struct Aluno {
    std::string nome;
    float nota;
};

void processarAlunos() {
    std::ifstream arquivoEntrada("alunos.txt");
    if (!arquivoEntrada) {
        std::cout << "Erro ao abrir arquivo de entrada\n";
        return;
    }

    Aluno alunos[100];
    int quantidade = 0;
    float soma = 0;

    while (arquivoEntrada >> alunos[quantidade].nome >> alunos[quantidade].nota) {
        soma += alunos[quantidade].nota;
        quantidade++;
        if (quantidade >= 100) break;
    }
    arquivoEntrada.close();

    if (quantidade == 0) return;
    float media = soma / quantidade;

    std::ofstream arquivoSaida("aprovados.txt");
    if (!arquivoSaida) {
        std::cout << "Erro ao abrir arquivo de saída\n";
        return;
    }

    arquivoSaida << std::fixed << std::setprecision(1);
    for (int i = 0; i < quantidade; i++) {
        if (alunos[i].nota > media) {
            arquivoSaida << alunos[i].nome << " " << alunos[i].nota << std::endl;
        }
    }
}

int main() {
    processarAlunos();
    return 0;
}

// Questão 2 - Estrutura Data
#include <iostream>

struct Data {
    int dia, mes, ano;
};

bool validarData(const Data& d) {
    if (d.mes < 1 || d.mes > 12) return false;
    if (d.dia < 1) return false;

    int dias_por_mes[] = {31,28,31,30,31,30,31,31,30,31,30,31};
    if (d.ano % 4 == 0 && (d.ano % 100 != 0 || d.ano % 400 == 0))
        dias_por_mes[1] = 29;

    return d.dia <= dias_por_mes[d.mes-1];
}

int compararDatas(const Data& d1, const Data& d2) {
    if (!validarData(d1) || !validarData(d2)) {
        std::cout << "Data inválida!\n";
        return -2;
    }

    if (d1.ano != d2.ano) return (d1.ano > d2.ano) ? 1 : -1;
    if (d1.mes != d2.mes) return (d1.mes > d2.mes) ? 1 : -1;
    if (d1.dia != d2.dia) return (d1.dia > d2.dia) ? 1 : -1;
    return 0;
}

int main() {
    Data d1 = {15, 3, 2024};
    Data d2 = {20, 2, 2024};
    int resultado = compararDatas(d1, d2);
    std::cout << "Resultado da comparação: " << resultado << std::endl;
    return 0;
}

// Questão 3 - Calculadora com Ponteiros para Funções
#include <iostream>
#include <iomanip>

double soma(double a, double b) { return a + b; }
double subtracao(double a, double b) { return a - b; }
double multiplicacao(double a, double b) { return a * b; }
double divisao(double a, double b) {
    if (b == 0) {
        std::cout << "Erro: divisão por zero!\n";
        return 0;
    }
    return a / b;
}

typedef double (*OperacaoMatematica)(double, double);

int main() {
    OperacaoMatematica operacoes[4] = {soma, subtracao, multiplicacao, divisao};
    char simbolos[4] = {'+', '-', '*', '/'};

    double a = 5.2, b = 3.8;
    char operador = '+';

    for (int i = 0; i < 4; i++) {
        if (simbolos[i] == operador) {
            double resultado = operacoes[i](a, b);
            std::cout << std::fixed << std::setprecision(1);
            std::cout << a << " " << operador << " " << b << " = " << resultado << std::endl;
            break;
        }
    }
    return 0;
}

// Questão 4 - Sistema de Filtros
#include <iostream>
#include <iomanip>

typedef double (*Filtro)(double);

double filtroMaximo(double valor) {
    return (valor > 100) ? 100 : valor;
}

double filtroMinimo(double valor) {
    return (valor < 0) ? 0 : valor;
}

double filtroParidade(double valor) {
    return 2 * (int)(valor / 2);
}

int main() {
    Filtro filtros[3] = {filtroMaximo, filtroMinimo, filtroParidade};
    double valor = 123;

    std::cout << std::fixed << std::setprecision(2);
    std::cout << "Valor original: " << valor << std::endl;

    for (int i = 0; i < 3; i++) {
        valor = filtros[i](valor);
        std::cout << "Após filtro " << i+1 << ": " << valor << std::endl;
    }
    return 0;
}

// Questão 5 - Agenda de Contatos
#include <iostream>
#include <string>

const int MAX_CONTATOS = 100;

struct Contato {
    std::string nome;
    std::string telefone;
};

struct Agenda {
    Contato contatos[MAX_CONTATOS];
    int quantidade;
};

void inicializarAgenda(Agenda& agenda) {
    agenda.quantidade = 0;
}

bool adicionarContato(Agenda& agenda, const std::string& nome, const std::string& telefone) {
    if (agenda.quantidade >= MAX_CONTATOS) {
        std::cout << "Agenda cheia!\n";
        return false;
    }
    agenda.contatos[agenda.quantidade].nome = nome;
    agenda.contatos[agenda.quantidade].telefone = telefone;
    agenda.quantidade++;
    return true;
}

void listarContatos(const Agenda& agenda) {
    for (int i = 0; i < agenda.quantidade; i++) {
        std::cout << "Nome: " << agenda.contatos[i].nome
                 << ", Tel: " << agenda.contatos[i].telefone << std::endl;
    }
}

bool buscarContato(const Agenda& agenda, const std::string& nome) {
    for (int i = 0; i < agenda.quantidade; i++) {
        if (agenda.contatos[i].nome == nome) {
            std::cout << "Nome: " << agenda.contatos[i].nome
                     << ", Tel: " << agenda.contatos[i].telefone << std::endl;
            return true;
        }
    }
    std::cout << "Contato não encontrado!\n";
    return false;
}

int main() {
    Agenda agenda;
    inicializarAgenda(agenda);

    adicionarContato(agenda, "João", "21999887766");
    adicionarContato(agenda, "Maria", "21988776655");

    std::cout << "Listando todos os contatos:\n";
    listarContatos(agenda);

    std::cout << "\nBuscando contato João:\n";
    buscarContato(agenda, "João");

    std::cout << "\nBuscando contato inexistente:\n";
    buscarContato(agenda, "Pedro");

    return 0;
}

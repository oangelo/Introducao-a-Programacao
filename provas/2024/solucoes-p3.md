#include <iostream>
#include <fstream>
#include <cstring>

// Questão 1 - Leitura e Escrita de Arquivos
struct Aluno {
    char nome[50];
    float nota;
};

void processarAlunos() {
    FILE* entrada = fopen("alunos.txt", "r");
    if (entrada == NULL) {
        printf("Erro ao abrir arquivo de entrada\n");
        return;
    }
    
    Aluno alunos[100];
    int quantidade = 0;
    float soma = 0;
    
    // Lendo os alunos
    while (!feof(entrada) && quantidade < 100) {
        fscanf(entrada, "%s %f", alunos[quantidade].nome, &alunos[quantidade].nota);
        soma += alunos[quantidade].nota;
        quantidade++;
    }
    fclose(entrada);
    
    // Calculando a média
    float media = soma / quantidade;
    
    // Gravando aprovados
    FILE* saida = fopen("aprovados.txt", "w");
    if (saida == NULL) {
        printf("Erro ao abrir arquivo de saída\n");
        return;
    }
    
    for (int i = 0; i < quantidade; i++) {
        if (alunos[i].nota > media) {
            fprintf(saida, "%s %.1f\n", alunos[i].nome, alunos[i].nota);
        }
    }
    fclose(saida);
}

// Questão 2 - Estrutura Data
struct Data {
    int dia, mes, ano;
};

bool validarData(const Data* d) {
    if (d->mes < 1 || d->mes > 12) return false;
    if (d->dia < 1) return false;
    
    int dias_por_mes[] = {31,28,31,30,31,30,31,31,30,31,30,31};
    if (d->ano % 4 == 0 && (d->ano % 100 != 0 || d->ano % 400 == 0))
        dias_por_mes[1] = 29;
        
    return d->dia <= dias_por_mes[d->mes-1];
}

int compararDatas(const Data* d1, const Data* d2) {
    if (!validarData(d1) || !validarData(d2))
        return -2; // Código de erro para data inválida
        
    if (d1->ano != d2->ano) return (d1->ano > d2->ano) ? 1 : -1;
    if (d1->mes != d2->mes) return (d1->mes > d2->mes) ? 1 : -1;
    if (d1->dia != d2->dia) return (d1->dia > d2->dia) ? 1 : -1;
    return 0;
}

// Questão 3 - Calculadora com Ponteiros para Funções
double soma(double a, double b) { return a + b; }
double subtracao(double a, double b) { return a - b; }
double multiplicacao(double a, double b) { return a * b; }
double divisao(double a, double b) {
    if (b == 0) return 0; // Indica erro
    return a / b;
}

typedef double (*OperacaoMatematica)(double, double);

struct Calculadora {
    OperacaoMatematica operacoes[4];
    char simbolos[4];
    
    void inicializar() {
        operacoes[0] = soma;
        operacoes[1] = subtracao;
        operacoes[2] = multiplicacao;
        operacoes[3] = divisao;
        simbolos[0] = '+';
        simbolos[1] = '-';
        simbolos[2] = '*';
        simbolos[3] = '/';
    }
    
    double executar(char operador, double a, double b) {
        for (int i = 0; i < 4; i++) {
            if (simbolos[i] == operador)
                return operacoes[i](a, b);
        }
        return 0; // Operação inválida
    }
};

// Questão 4 - Sistema de Filtros
double filtroMaximo(double valor) {
    return (valor > 100) ? 100 : valor;
}

double filtroMinimo(double valor) {
    return (valor < 0) ? 0 : valor;
}

double filtroParidade(double valor) {
    return 2 * (int)(valor / 2);  // Arredonda para o par mais próximo para baixo
}

struct SistemaFiltros {
    typedef double (*Filtro)(double);
    Filtro filtros[3];
    int numFiltros;
    
    void inicializar() {
        filtros[0] = filtroMaximo;
        filtros[1] = filtroMinimo;
        filtros[2] = filtroParidade;
        numFiltros = 3;
    }
    
    double aplicarFiltros(double valor) {
        double resultado = valor;
        for (int i = 0; i < numFiltros; i++) {
            resultado = filtros[i](resultado);
            printf("Após filtro %d: %.2f\n", i+1, resultado);
        }
        return resultado;
    }
};

// Questão 5 - Agenda de Contatos
const int MAX_CONTATOS = 100;

struct Contato {
    char nome[50];
    char telefone[15];
};

struct Agenda {
    Contato contatos[MAX_CONTATOS];
    int quantidade;
    
    void inicializar() {
        quantidade = 0;
    }
    
    int adicionar(const char* nome, const char* telefone) {
        if (quantidade >= MAX_CONTATOS) {
            return 0; // falha
        }
        strcpy(contatos[quantidade].nome, nome);
        strcpy(contatos[quantidade].telefone, telefone);
        quantidade++;
        return 1; // sucesso
    }
    
    void listar() {
        for (int i = 0; i < quantidade; i++) {
            printf("Nome: %s, Tel: %s\n", 
                   contatos[i].nome, 
                   contatos[i].telefone);
        }
    }
    
    Contato* buscar(const char* nome) {
        for (int i = 0; i < quantidade; i++) {
            if (strcmp(contatos[i].nome, nome) == 0) {
                return &contatos[i];
            }
        }
        return NULL;
    }
};

// Programa Principal para Testar
int main() {
    // Teste da Questão 1
    printf("Testando processamento de alunos...\n");
    processarAlunos();
    
    // Teste da Questão 2
    printf("\nTestando comparação de datas...\n");
    Data d1 = {15, 3, 2024};
    Data d2 = {20, 2, 2024};
    int resultado = compararDatas(&d1, &d2);
    printf("Resultado da comparação: %d\n", resultado);
    
    // Teste da Questão 3
    printf("\nTestando calculadora...\n");
    Calculadora calc;
    calc.inicializar();
    double res = calc.executar('+', 5.2, 3.8);
    printf("5.2 + 3.8 = %.1f\n", res);
    
    // Teste da Questão 4
    printf("\nTestando sistema de filtros...\n");
    SistemaFiltros filtros;
    filtros.inicializar();
    double valor_final = filtros.aplicarFiltros(123);
    printf("Valor final: %.2f\n", valor_final);
    
    // Teste da Questão 5
    printf("\nTestando agenda de contatos...\n");
    Agenda agenda;
    agenda.inicializar();
    agenda.adicionar("João", "21999887766");
    Contato* c = agenda.buscar("João");
    if (c != NULL) {
        printf("Encontrado - Nome: %s, Tel: %s\n", c->nome, c->telefone);
    }
    
    return 0;
}

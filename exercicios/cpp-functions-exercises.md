# Exercícios: Funções em C++

Antes de mergulhar nas soluções, lembre-se: a melhor maneira de aprender programação é fazendo por conta própria. Tente resolver cada problema sozinho primeiro. Escrever código, mesmo que não seja perfeito, é crucial para desenvolver suas habilidades de resolução de problemas e compreensão de C++. Só olhe as soluções quando estiver realmente travado ou quiser comparar sua abordagem.

### 1. Olá, Função! ★
**Objetivo:** Crie uma função chamada `saudacao` que não recebe parâmetros e imprime "Olá, mundo!" na tela.

**Importância:** Este exercício introduz o conceito básico de definição e chamada de funções, estabelecendo uma base para exercícios mais complexos.

**Dica de implementação:** Use `void` como tipo de retorno, já que a função não retorna nenhum valor.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void saudacao() {
    std::cout << "Olá, mundo!" << std::endl;
}

int main() {
    saudacao();
    return 0;
}
```

</details>

### 2. Soma Simples ★
**Objetivo:** Escreva uma função chamada `soma` que recebe dois inteiros como parâmetros e retorna a soma deles.

**Importância:** Pratica a passagem de parâmetros e o retorno de valores, conceitos fundamentais no uso de funções.

**Dica de implementação:** Use `int` como tipo de retorno e dois parâmetros `int`.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int soma(int a, int b) {
    return a + b;
}

int main() {
    int resultado = soma(5, 3);
    std::cout << "A soma é: " << resultado << std::endl;
    return 0;
}
```

</details>

### 3. Calculadora Básica ★★
**Objetivo:** Crie quatro funções: `adicao`, `subtracao`, `multiplicacao` e `divisao`. Cada função deve receber dois números como parâmetros e retornar o resultado da operação correspondente.

**Importância:** Expande o conceito de funções para múltiplas operações, incentivando a modularização do código.

**Dica de implementação:** Use `float` como tipo de retorno para lidar com divisões não inteiras.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

float adicao(float a, float b) {
    return a + b;
}

float subtracao(float a, float b) {
    return a - b;
}

float multiplicacao(float a, float b) {
    return a * b;
}

float divisao(float a, float b) {
    if (b != 0) {
        return a / b;
    } else {
        std::cout << "Erro: Divisão por zero!" << std::endl;
        return 0;
    }
}

int main() {
    float a = 10, b = 5;
    std::cout << "Adição: " << adicao(a, b) << std::endl;
    std::cout << "Subtração: " << subtracao(a, b) << std::endl;
    std::cout << "Multiplicação: " << multiplicacao(a, b) << std::endl;
    std::cout << "Divisão: " << divisao(a, b) << std::endl;
    return 0;
}
```

</details>

### 4. Número Par ou Ímpar ★★
**Objetivo:** Implemente uma função chamada `ehPar` que recebe um número inteiro e retorna `true` se o número for par e `false` se for ímpar.

**Importância:** Introduz o uso de funções booleanas e a lógica condicional dentro de funções.

**Dica de implementação:** Use o operador módulo (%) para verificar se o número é divisível por 2.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

bool ehPar(int numero) {
    return numero % 2 == 0;
}

int main() {
    int num = 7;
    if (ehPar(num)) {
        std::cout << num << " é par." << std::endl;
    } else {
        std::cout << num << " é ímpar." << std::endl;
    }
    return 0;
}
```

</details>

### 5. Fatorial ★★★
**Objetivo:** Escreva uma função recursiva chamada `fatorial` que calcula o fatorial de um número inteiro não negativo.

**Importância:** Este exercício introduz o conceito de recursão, uma técnica poderosa na programação funcional.

**Dica de implementação:** Use uma condição base para 0 ou 1, e chame a função recursivamente para n * fatorial(n-1).

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

unsigned long long fatorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    }
    return n * fatorial(n - 1);
}

int main() {
    int num = 5;
    std::cout << "Fatorial de " << num << " é " << fatorial(num) << std::endl;
    return 0;
}
```

</details>

### 6. Fibonacci ★★★
**Objetivo:** Crie uma função chamada `fibonacci` que recebe um número n como parâmetro e retorna o n-ésimo número da sequência de Fibonacci.

**Importância:** Pratica o uso de lógica mais complexa dentro de funções e pode ser resolvido de forma iterativa ou recursiva.

**Dica de implementação:** Use uma abordagem iterativa com um loop para calcular os números de Fibonacci até o n-ésimo termo.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }
    int a = 0, b = 1, c;
    for (int i = 2; i <= n; i++) {
        c = a + b;
        a = b;
        b = c;
    }
    return b;
}

int main() {
    int n = 10;
    std::cout << "O " << n << "º número de Fibonacci é " << fibonacci(n) << std::endl;
    return 0;
}
```

</details>

### 7. Troca de Valores ★★
**Objetivo:** Implemente duas funções:
a) `trocaPorValor` que recebe dois inteiros e tenta trocá-los.
b) `trocaPorReferencia` que recebe dois inteiros por referência e os troca.
Compare o resultado das duas funções.

**Importância:** Este exercício demonstra claramente a diferença entre passagem por valor e por referência, mostrando como a passagem por referência permite modificar as variáveis originais.

**Dica de implementação:** Use `&` para declarar parâmetros por referência.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void trocaPorValor(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

void trocaPorReferencia(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 5, y = 10;
    
    std::cout << "Antes da troca por valor: x = " << x << ", y = " << y << std::endl;
    trocaPorValor(x, y);
    std::cout << "Depois da troca por valor: x = " << x << ", y = " << y << std::endl;
    
    std::cout << "Antes da troca por referência: x = " << x << ", y = " << y << std::endl;
    trocaPorReferencia(x, y);
    std::cout << "Depois da troca por referência: x = " << x << ", y = " << y << std::endl;
    
    return 0;
}
```

</details>

### 8. Incremento e Retorno ★★
**Objetivo:** Crie duas funções:
a) `incrementaERetornaPorValor` que recebe um inteiro, incrementa-o e retorna o novo valor.
b) `incrementaPorReferencia` que recebe um inteiro por referência e o incrementa sem retornar nada.
Use ambas as funções e compare seus efeitos.

**Importância:** Este exercício mostra como a passagem por referência pode ser usada para modificar variáveis sem necessidade de retorno, enquanto a passagem por valor requer retorno para refletir mudanças.

**Dica de implementação:** Use `void` como tipo de retorno para a função que recebe por referência.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

int incrementaERetornaPorValor(int n) {
    return n + 1;
}

void incrementaPorReferencia(int& n) {
    n++;
}

int main() {
    int a = 5, b = 5;
    
    std::cout << "Valor original de a: " << a << std::endl;
    a = incrementaERetornaPorValor(a);
    std::cout << "Após incremento por valor: " << a << std::endl;
    
    std::cout << "Valor original de b: " << b << std::endl;
    incrementaPorReferencia(b);
    std::cout << "Após incremento por referência: " << b << std::endl;
    
    return 0;
}
```

</details>

### 9. Calculadora de Desconto ★★★
**Objetivo:** Implemente uma função chamada `aplicarDesconto` que recebe o preço de um produto por referência e a porcentagem de desconto por valor. A função deve modificar o preço aplicando o desconto.

**Importância:** Pratica o uso de passagem por referência para modificar um valor e passagem por valor para um parâmetro que não precisa ser alterado.

**Dica de implementação:** Use a fórmula: preço final = preço original * (1 - desconto/100).

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void aplicarDesconto(float& preco, float desconto) {
    preco = preco * (1 - desconto / 100);
}

int main() {
    float preco = 100.0;
    float desconto = 20.0;
    
    std::cout << "Preço original: R$" << preco << std::endl;
    aplicarDesconto(preco, desconto);
    std::cout << "Preço com desconto de " << desconto << "%: R$" << preco << std::endl;
    
    return 0;
}
```

</details>

### 10. Divisão com Resto ★★★
**Objetivo:** Crie uma função chamada `dividirComResto` que recebe dois inteiros (dividendo e divisor) por valor, e dois inteiros por referência para armazenar o quociente e o resto da divisão.

**Importância:** Este exercício demonstra como usar a passagem por referência para retornar múltiplos valores de uma função.

**Dica de implementação:** Use o operador de divisão (/) para o quociente e o operador módulo (%) para o resto.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void dividirComResto(int dividendo, int divisor, int& quociente, int& resto) {
    quociente = dividendo / divisor;
    resto = dividendo % divisor;
}

int main() {
    int a = 17, b = 5, q, r;
    
    dividirComResto(a, b, q, r);
    
    std::cout << a << " dividido por " << b << " é igual a " << q << " com resto " << r << std::endl;
    
    return 0;
}
```

</details>

### 11. Estatísticas Simples ★★★
**Objetivo:** Escreva uma função chamada `calcularEstatisticas` que recebe um número por valor e três variáveis por referência. A função deve calcular e atribuir às variáveis por referência: o quadrado do número, a raiz quadrada do número e o valor absoluto do número.

**Importância:** Pratica o uso de passagem por referência para retornar múltiplos resultados calculados e passagem por valor para o dado de entrada.

**Dica de implementação:** Use a biblioteca `<cmath>` para as operações matemáticas.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <cmath>

void calcularEstatisticas(double numero, double& quadrado, double& raiz, double& absoluto) {
    quadrado = numero * numero;
    raiz = sqrt(abs(numero));  // Usamos abs para evitar erro com números negativos
    absoluto = abs(numero);
}

int main() {
    double num = -16.0, quad, raiz, abs;
    
    calcularEstatisticas(num, quad, raiz, abs);
    
    std::cout << "Número: " << num << std::endl;
    std::cout << "Quadrado: " << quad << std::endl;
    std::cout << "Raiz quadrada: " << raiz << std::endl;
    std::cout << "Valor absoluto: " << abs << std::endl;
    
    return 0;
}
```

</details>

### 12. Manipulação de Strings ★★★★
**Objetivo:** Implemente uma função chamada `processarString` que recebe uma string por referência. A função deve converter a primeira letra para maiúscula, remover espaços em branco no início e no fim, e substituir múltiplos espaços por um único espaço.

**Importância:** Este exercício mostra como a passagem por referência pode ser usada para modificar strings de forma eficiente, sem necessidade de retornar uma nova string.

**Dica de implementação:** Use funções da biblioteca `<string>` como `erase()`, `find()`, e `toupper()`.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>
#include <string>
#include <algorithm>

void processarString(std::string& str) {
    // Remover espaços no início e no fim
    str.erase(0, str.find_first_not_of(" \t\n\r\f\v"));
    str.erase(str.find_last_not_of(" \t\n\r\f\v") + 1);
    
    // Converter primeira letra para maiúscula
    if (!str.empty()) {
        str[0] = toupper(str[0]);
    }
    
    // Substituir múltiplos espaços por um único espaço
    auto new_end = std::unique(str.begin(), str.end(),
                               [](char a, char b) { return a == ' ' && b == ' '; });
    str.erase(new_end, str.end());
}

int main() {
    std::string texto = "   hello   world  ";
    std::cout << "Original: '" << texto << "'" << std::endl;
    
    processarString(texto);
    std::cout << "Processada: '" << texto << "'" << std::endl;
    
    return 0;
}
```

</details>

### 14. Swap de Inteiros ★★
**Objetivo:** Implemente uma função chamada `trocar` que pode trocar os valores de dois inteiros. Use referências para realizar a troca.

**Importância:** Este exercício demonstra como usar referências para modificar valores de variáveis fora da função, uma técnica comum e útil em C++.

**Dica de implementação:** Use uma variável temporária para realizar a troca.

<details>
<summary>Solução</summary>

```cpp
#include <iostream>

void trocar(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 5, y = 10;
    std::cout << "Antes da troca: x = " << x << ", y = " << y << std::endl;
    trocar(x, y);
    std::cout << "Depois da troca: x = " << x << ", y = " << y << std::endl;

    return 0;
}
```

</details>

**Explicação da solução:**
1. A função `trocar` recebe dois parâmetros por referência (`int& a` e `int& b`). Isso significa que ela trabalha diretamente com as variáveis originais, não com cópias.
2. Dentro da função, usamos uma variável temporária `temp` para armazenar o valor de `a`.
3. Atribuímos o valor de `b` para `a`.
4. Finalmente, atribuímos o valor original de `a` (armazenado em `temp`) para `b`.
5. No `main()`, chamamos `trocar(x, y)`, que troca os valores de `x` e `y`.
6. Imprimimos os valores antes e depois da troca para demonstrar que a função realmente modificou as variáveis originais.

Esta versão do exercício mantém o foco na passagem por referência e na manipulação de variáveis através de funções, sem introduzir o conceito de templates.

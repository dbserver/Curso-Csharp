## Lambda Expressions em C#

As expressões lambda são uma maneira concisa e poderosa de escrever funções anônimas em C#. Elas permitem que você crie métodos inline, ou seja, você pode escrever funções de maneira mais compacta e legível. As expressões lambda são frequentemente usadas em combinação com coleções e LINQ (Language Integrated Query) para manipulação de dados.

### 1. O que são Expressões Lambda?

Uma expressão lambda é uma função anônima que pode conter parâmetros e um corpo. Elas são definidas usando a sintaxe `=>`, que é lida como "vira". Uma expressão lambda pode ser usada para criar delegates ou para expressões que serão avaliadas em tempo de execução.

#### Exemplo Básico

```csharp
// Definindo uma expressão lambda
Func<int, int> quadrado = x => x * x;

// Usando a expressão lambda
int resultado = quadrado(5);
Console.WriteLine($"O quadrado de 5 é: {resultado}"); // Saída: 25
```

### 2. Sintaxe das Expressões Lambda

A sintaxe básica de uma expressão lambda é a seguinte:

```csharp
(parameters) => expression
```

- **parameters**: Os parâmetros da função. Podem ser zero, um ou mais parâmetros. Se houver apenas um parâmetro, os parênteses podem ser omitidos.
- **expression**: O corpo da expressão que pode ser uma expressão única ou um bloco de código.

#### Exemplos de Sintaxe

1. **Sem parâmetros**:

```csharp
Action saudacao = () => Console.WriteLine("Olá, mundo!");
saudacao(); // Saída: Olá, mundo!
```

2. **Um parâmetro**:

```csharp
Func<int, int> dobro = x => x * 2;
Console.WriteLine(dobro(4)); // Saída: 8
```

3. **Múltiplos parâmetros**:

```csharp
Func<int, int, int> soma = (x, y) => x + y;
Console.WriteLine(soma(3, 5)); // Saída: 8
```

4. **Bloco de código**:

```csharp
Func<int, int> fatorial = null;
fatorial = n =>
{
    if (n == 0) return 1;
    return n * fatorial(n - 1);
};

Console.WriteLine(fatorial(5)); // Saída: 120
```

### 3. Usando Expressões Lambda com Coleções

As expressões lambda são frequentemente usadas com métodos de extensão, especialmente em LINQ, para filtrar, ordenar e manipular coleções.

#### Exemplo com LINQ

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

public class Program
{
    public static void Main()
    {
        List<int> numeros = new List<int> { 1, 2, 3, 4, 5, 6 };

        // Filtra números pares usando uma expressão lambda
        var numerosPares = numeros.Where(x => x % 2 == 0);

        Console.WriteLine("Números pares:");
        foreach (var numero in numerosPares)
        {
            Console.WriteLine(numero); // Saída: 2, 4, 6
        }
    }
}
```

### 4. Vantagens das Expressões Lambda

1. **Concisão**: Reduz a quantidade de código necessário para definir métodos anônimos.
2. **Legibilidade**: O código pode se tornar mais legível e fácil de entender.
3. **Integração com LINQ**: Facilita a manipulação de coleções e a consulta de dados.

### 5. Considerações

- As expressões lambda podem capturar variáveis do escopo onde são definidas, o que significa que podem acessar variáveis locais mesmo após o escopo em que foram definidas ter terminado. Essa característica é chamada de **captura de variáveis**.
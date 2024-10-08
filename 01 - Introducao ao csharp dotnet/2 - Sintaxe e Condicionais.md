### Sintaxe Básica de C#: Tipos de Dados, Variáveis, Operadores

A sintaxe básica do C# é intuitiva e poderosa, permitindo o desenvolvimento de uma ampla gama de aplicações. Vamos começar abordando os **tipos de dados**, **variáveis** e **operadores**, seguidos das **estruturas de controle** que permitem decisões e repetições no código.

---

### 1. Tipos de Dados em C#

Os tipos de dados em C# determinam o tipo de valores que podem ser armazenados em uma variável. Eles são classificados em **tipos de valor** e **tipos de referência**.

#### 1.1 Tipos de Valor
Os **tipos de valor** armazenam dados diretamente na memória stack e incluem tipos primitivos, como números, caracteres e estruturas.

- **Inteiros**:
  - `int`: Armazena números inteiros (4 bytes).
  - `long`: Armazena inteiros de maior precisão (8 bytes).
  - `short`: Armazena inteiros menores (2 bytes).
  - `byte`: Armazena inteiros de 1 byte (0 a 255).

  Exemplo:
  ```csharp
  int numero = 42;
  ```

- **Flutuantes**:
  - `float`: Armazena números de ponto flutuante (4 bytes).
  - `double`: Números de ponto flutuante de maior precisão (8 bytes).
  - `decimal`: Alta precisão para cálculos financeiros (16 bytes).

  Exemplo:
  ```csharp
  double preco = 19.99;
  ```

- **Booleano**:
  - `bool`: Armazena valores `true` ou `false` (1 byte).

  Exemplo:
  ```csharp
  bool ativo = true;
  ```

- **Caractere**:
  - `char`: Armazena um único caractere (2 bytes, Unicode).

  Exemplo:
  ```csharp
  char letra = 'A';
  ```

#### 1.2 Tipos de Referência
Os **tipos de referência** armazenam uma referência a um objeto na heap, e não o dado em si. Incluem classes, arrays e strings.

- **String**:
  - `string`: Uma sequência de caracteres.

  Exemplo:
  ```csharp
  string mensagem = "Olá, Mundo!";
  ```

- **Arrays**:
  - Um conjunto de elementos de um tipo específico.

  Exemplo:
  ```csharp
  int[] numeros = { 1, 2, 3, 4, 5 };
  ```

---

### 2. Variáveis

As **variáveis** são usadas para armazenar dados na memória. Em C#, é necessário declarar a variável antes de utilizá-la, especificando o tipo.

**Sintaxe:**
```csharp
tipo nomeVariavel = valorInicial;
```

Exemplo:
```csharp
int idade = 30;
string nome = "Maria";
```

#### 2.1 Modificadores de Acesso e Palavra-chave `var`

O C# permite usar a palavra-chave `var` para a inferência de tipos, onde o compilador automaticamente deduz o tipo da variável com base no valor atribuído.

Exemplo:
```csharp
var preco = 19.99; // Tipo double inferido
```

---

### 3. Operadores em C#

Os **operadores** são usados para realizar operações em variáveis e valores. Eles são classificados em várias categorias.

#### 3.1 Operadores Aritméticos
- **Soma**: `+`
- **Subtração**: `-`
- **Multiplicação**: `*`
- **Divisão**: `/`
- **Módulo** (resto da divisão): `%`

Exemplo:
```csharp
int resultado = 10 + 5;
```

#### 3.2 Operadores Relacionais
Comparam dois valores e retornam `true` ou `false`.

- **Igual a**: `==`
- **Diferente de**: `!=`
- **Maior que**: `>`
- **Menor que**: `<`
- **Maior ou igual a**: `>=`
- **Menor ou igual a**: `<=`

Exemplo:
```csharp
bool comparacao = (10 > 5); // true
```

#### 3.3 Operadores Lógicos
Usados para combinar expressões booleanas.

- **E Lógico**: `&&`
- **Ou Lógico**: `||`
- **Não Lógico**: `!`

Exemplo:
```csharp
bool resultado = (10 > 5) && (5 < 3); // false
```

#### 3.4 Operador de Atribuição
- **Atribuição**: `=`

Além do operador básico de atribuição, existem operadores combinados como `+=`, `-=`, `*=`, etc.

Exemplo:
```csharp
int soma = 5;
soma += 10; // soma agora é 15
```

---

### Estruturas de Controle: Condicionais e Loops

As **estruturas de controle** em C# permitem controlar o fluxo de execução do programa com base em condições e repetições.

---

### 4. Condicionais

#### 4.1 Estrutura `if`

A estrutura `if` é usada para executar um bloco de código se uma condição for verdadeira.

**Sintaxe:**
```csharp
if (condicao)
{
    // Bloco de código executado se a condição for verdadeira
}
```

Exemplo:
```csharp
int idade = 18;

if (idade >= 18)
{
    Console.WriteLine("Maior de idade.");
}
```

#### 4.2 Estrutura `if-else`

A estrutura `if-else` é usada para especificar um bloco de código alternativo, caso a condição seja falsa.

**Sintaxe:**
```csharp
if (condicao)
{
    // Bloco de código executado se a condição for verdadeira
}
else
{
    // Bloco de código executado se a condição for falsa
}
```

Exemplo:
```csharp
int idade = 16;

if (idade >= 18)
{
    Console.WriteLine("Maior de idade.");
}
else
{
    Console.WriteLine("Menor de idade.");
}
```

#### 4.3 Estrutura `switch`

A estrutura `switch` é usada quando temos várias condições para verificar, substituindo múltiplos `if-else`.

**Sintaxe:**
```csharp
switch (variavel)
{
    case valor1:
        // Código executado se variavel == valor1
        break;
    case valor2:
        // Código executado se variavel == valor2
        break;
    default:
        // Código executado se nenhuma das condições anteriores for atendida
        break;
}
```

Exemplo:
```csharp
int dia = 3;

switch (dia)
{
    case 1:
        Console.WriteLine("Domingo");
        break;
    case 2:
        Console.WriteLine("Segunda-feira");
        break;
    case 3:
        Console.WriteLine("Terça-feira");
        break;
    default:
        Console.WriteLine("Outro dia");
        break;
}
```

---

### 5. Loops (Estruturas de Repetição)

Os loops são usados para repetir blocos de código enquanto uma condição for verdadeira.

#### 5.1 Estrutura `for`

O loop `for` é usado quando o número de iterações é conhecido.

**Sintaxe:**
```csharp
for (inicializacao; condicao; incremento)
{
    // Bloco de código a ser repetido
}
```

Exemplo:
```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine("Valor de i: " + i);
}
```

#### 5.2 Estrutura `while`

O loop `while` executa um bloco de código repetidamente enquanto uma condição for verdadeira.

**Sintaxe:**
```csharp
while (condicao)
{
    // Bloco de código a ser repetido
}
```

Exemplo:
```csharp
int contador = 0;

while (contador < 5)
{
    Console.WriteLine("Contador: " + contador);
    contador++;
}
```

#### 5.3 Estrutura `do-while`

O loop `do-while` é semelhante ao `while`, mas a condição é verificada **após** a execução do bloco de código. Isso garante que o código seja executado pelo menos uma vez.

**Sintaxe:**
```csharp
do
{
    // Bloco de código a ser repetido
} while (condicao);
```

Exemplo:
```csharp
int contador = 0;

do
{
    Console.WriteLine("Contador: " + contador);
    contador++;
} while (contador < 5);
```

---
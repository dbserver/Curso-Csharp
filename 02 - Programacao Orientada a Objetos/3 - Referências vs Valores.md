### Referências vs Valores: Tipos de Valor e Tipos de Referência em C#

Em C#, os **tipos de valor** e **tipos de referência** são conceitos fundamentais para entender como a linguagem manipula os dados em memória. A distinção entre esses dois tipos é importante porque eles determinam como os dados são armazenados e manipulados, e isso impacta diretamente o desempenho e o comportamento do código.

#### Tipos de Valor

Os **tipos de valor** armazenam diretamente os dados. Quando você cria uma variável de tipo de valor, um espaço de memória é alocado diretamente para o valor dessa variável. Se você copiar uma variável de tipo de valor para outra, uma **cópia completa** do valor é feita.

- Os tipos de valor são geralmente armazenados na **pilha de memória** (*stack*), uma área de memória que é rápida, mas limitada em espaço.
- Cada variável tem uma cópia própria do dado. Isso significa que mudanças feitas em uma variável **não afetam** outras variáveis.

##### Exemplos de Tipos de Valor:
- Tipos primitivos como `int`, `double`, `float`, `bool`, `char`.
- Estruturas (`struct`), que são semelhantes às classes, mas funcionam como tipos de valor.

##### Exemplo de Tipo de Valor:

```csharp
int a = 10;
int b = a; // Cópia completa do valor de 'a' para 'b'

b = 20;   // Alterar 'b' não afeta 'a'

Console.WriteLine($"a: {a}, b: {b}"); // a: 10, b: 20
```

Aqui, como `int` é um tipo de valor, `a` e `b` são armazenados separadamente na memória. A alteração de `b` para 20 não afeta o valor de `a`, que permanece 10.

##### Definindo uma Estrutura (Tipo de Valor Personalizado):

```csharp
public struct Ponto
{
    public int X;
    public int Y;

    public Ponto(int x, int y)
    {
        X = x;
        Y = y;
    }
}

Ponto p1 = new Ponto(10, 20);
Ponto p2 = p1; // Cópia do valor

p2.X = 30; // Alteração em p2 não afeta p1

Console.WriteLine($"p1: {p1.X}, {p1.Y}"); // p1: 10, 20
Console.WriteLine($"p2: {p2.X}, {p2.Y}"); // p2: 30, 20
```

#### Tipos de Referência

Os **tipos de referência** armazenam uma **referência** (ou endereço) para o valor real. Ou seja, a variável não contém diretamente o dado, mas sim um ponteiro para a localização do dado na memória.

- Os tipos de referência são armazenados no **heap** (uma área de memória maior, mas mais lenta).
- Ao copiar uma variável de tipo de referência, ambas as variáveis apontam para o mesmo local na memória. Isso significa que mudanças feitas em uma variável **afetam** todas as variáveis que apontam para o mesmo objeto.

##### Exemplos de Tipos de Referência:
- **Classes**, como `object`, `string`, arrays, e qualquer tipo de classe personalizada.
- Delegates, interfaces e dynamic types.

##### Exemplo de Tipo de Referência:

```csharp
public class ContaBancaria
{
    public string NomeTitular;
    public decimal Saldo;

    public ContaBancaria(string nomeTitular, decimal saldo)
    {
        NomeTitular = nomeTitular;
        Saldo = saldo;
    }
}

ContaBancaria conta1 = new ContaBancaria("João", 500);
ContaBancaria conta2 = conta1; // Referência para o mesmo objeto

conta2.Saldo = 1000; // Alteração em conta2 afeta conta1

Console.WriteLine($"Saldo de conta1: {conta1.Saldo}"); // 1000
Console.WriteLine($"Saldo de conta2: {conta2.Saldo}"); // 1000
```

Aqui, `conta1` e `conta2` apontam para o mesmo objeto na memória. Alterar o saldo de `conta2` também altera o saldo de `conta1`, porque ambas as variáveis se referem ao mesmo objeto.

#### Diferenças Entre Tipos de Valor e Tipos de Referência

| **Característica**             | **Tipos de Valor**                             | **Tipos de Referência**                         |
|--------------------------------|------------------------------------------------|------------------------------------------------|
| **Armazenamento**              | Na pilha de memória (*stack*).                 | No heap de memória (*heap*).                   |
| **Cópia**                      | Cópia completa dos dados.                      | Cópia do endereço (referência).                |
| **Modificação**                | Não afeta outras variáveis.                    | Afeta todas as referências ao mesmo objeto.    |
| **Tipo**                       | Estruturas, tipos primitivos (int, bool, etc.).| Classes, interfaces, arrays, string.           |
| **Desempenho**                 | Mais rápido, mas limitado em espaço.           | Mais lento, mas mais flexível em alocação.     |

#### Nullabilidade em Tipos de Referência e Valor

Por padrão, **tipos de valor** não podem ser nulos, ou seja, eles devem sempre ter um valor. No entanto, você pode utilizar o modificador `?` para tornar um tipo de valor **nullable** (permitir que ele seja nulo).

##### Exemplo de Tipo de Valor Nullable:

```csharp
int? numero = null; // Um int nullable pode ser nulo
if (numero.HasValue)
{
    Console.WriteLine($"O valor é: {numero.Value}");
}
else
{
    Console.WriteLine("O valor é nulo.");
}
```

**Tipos de referência**, por outro lado, podem ser nulos por padrão. Isso significa que uma variável de tipo de referência pode não apontar para nenhum objeto em memória.

```csharp
ContaBancaria conta = null;
if (conta == null)
{
    Console.WriteLine("A conta bancária não está inicializada.");
}
```

#### Box e Unbox (Encapsulamento e Desencapsulamento)

Em C#, **boxing** e **unboxing** referem-se ao processo de converter tipos de valor em tipos de referência e vice-versa.

- **Boxing:** Converte um tipo de valor para um tipo de referência, encapsulando o valor no heap.
- **Unboxing:** Converte um tipo de referência de volta para um tipo de valor.

##### Exemplo de Boxing e Unboxing:

```csharp
int numero = 123;       // Tipo de valor
object obj = numero;    // Boxing: Converte para tipo de referência

int outroNumero = (int)obj; // Unboxing: Converte de volta para tipo de valor
```

**Boxing** e **unboxing** podem ter um impacto no desempenho, pois envolvem a alocação e cópia de dados na memória.

#### Trabalhando com Tipos de Valor e Referência no Contexto das Classes do Curso

Para ilustrar esses conceitos, vamos trabalhar com as classes que você está utilizando no curso de programação orientada a objetos.

##### Exemplo com Tipo de Valor:

Suponha que você esteja utilizando uma estrutura para representar um ponto de transação, como coordenadas em um mapa de atividades bancárias. Como essas coordenadas não precisam ser compartilhadas e alteradas entre diferentes transações, faz sentido usar um tipo de valor.

```csharp
public struct Coordenada
{
    public int X { get; set; }
    public int Y { get; set; }

    public Coordenada(int x, int y)
    {
        X = x;
        Y = y;
    }
}

Coordenada c1 = new Coordenada(10, 20);
Coordenada c2 = c1; // Cópia de valor
c2.X = 30;

Console.WriteLine($"c1: {c1.X}, {c1.Y}"); // c1: 10, 20
Console.WriteLine($"c2: {c2.X}, {c2.Y}"); // c2: 30, 20
```

##### Exemplo com Tipo de Referência:

Vamos aplicar o conceito de tipo de referência para a classe **Extrato**.

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }

    public Extrato(int id, string numeroConta, string nomeTitular)
    {
        ID = id;
        NumeroConta = numeroConta;
        NomeTitular = nomeTitular;
    }
}

Extrato extrato1 = new Extrato(1, "123456", "João");
Extrato extrato2 = extrato1; // Referência para o mesmo objeto

extrato2.NomeTitular = "Maria"; // Alteração afeta extrato1 também

Console.WriteLine(extrato1.NomeTitular); // Maria
Console.WriteLine(extrato2.NomeTitular); // Maria
```

Aqui, `extrato1` e `extrato2` referenciam o mesmo objeto na memória. Qualquer alteração em um será refletida no outro.
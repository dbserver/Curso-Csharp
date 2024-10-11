### Construtores e Sobrecarga em C#

#### O que é um Construtor?
Um **construtor** é um método especial de uma classe que é chamado automaticamente quando um objeto dessa classe é instanciado. O propósito do construtor é inicializar os atributos da classe, assegurando que o objeto comece em um estado válido.

A sintaxe do construtor em C# é semelhante a um método, mas:
- Ele não tem um tipo de retorno, nem mesmo `void`.
- Seu nome é sempre o mesmo nome da classe.

##### Exemplo de Construtor Básico:

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }

    // Construtor que inicializa os atributos
    public Extrato(int id, string numeroConta, string nomeTitular)
    {
        ID = id;
        NumeroConta = numeroConta;
        NomeTitular = nomeTitular;
    }
}
```

No exemplo acima, ao criar um novo objeto `Extrato`, o construtor será chamado e atribuirá os valores para `ID`, `NumeroConta`, e `NomeTitular`.

##### Instanciando um Objeto:

```csharp
Extrato extrato1 = new Extrato(1, "123456", "João da Silva");
```

Aqui, o objeto `extrato1` será inicializado com o ID `1`, número de conta `123456` e nome do titular `João da Silva`.

#### Construtores Padrão
Se você não definir um construtor explicitamente em sua classe, o C# cria automaticamente um **construtor padrão** que não aceita parâmetros e não faz nada além de inicializar o objeto.

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }
}

// Construtor padrão é criado automaticamente
Extrato extrato2 = new Extrato(); // Isso funciona mesmo sem um construtor explícito
```

No entanto, se você definir um construtor com parâmetros, como no primeiro exemplo, o **construtor padrão** não será mais criado automaticamente. Você terá que defini-lo manualmente se precisar dele:

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }

    // Construtor padrão
    public Extrato() { }

    // Construtor com parâmetros
    public Extrato(int id, string numeroConta, string nomeTitular)
    {
        ID = id;
        NumeroConta = numeroConta;
        NomeTitular = nomeTitular;
    }
}
```

#### Sobrecarga de Construtores (Overloading)

**Sobrecarga de construtores** é a capacidade de definir múltiplos construtores com assinaturas diferentes em uma mesma classe. Cada construtor pode ter diferentes números ou tipos de parâmetros, permitindo flexibilidade na criação de objetos.

##### Exemplo de Sobrecarga:

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }

    // Construtor padrão
    public Extrato() { }

    // Construtor com dois parâmetros
    public Extrato(int id, string numeroConta)
    {
        ID = id;
        NumeroConta = numeroConta;
        NomeTitular = "Desconhecido"; // Valor padrão
    }

    // Construtor com três parâmetros
    public Extrato(int id, string numeroConta, string nomeTitular)
    {
        ID = id;
        NumeroConta = numeroConta;
        NomeTitular = nomeTitular;
    }
}
```

Neste exemplo, temos três construtores:
- Um **construtor padrão** que não aceita parâmetros.
- Um **construtor com dois parâmetros** que define um valor padrão para o nome do titular.
- Um **construtor com três parâmetros** que inicializa todas as propriedades.

##### Instanciando Objetos Usando Sobrecarga:

```csharp
Extrato extrato1 = new Extrato(); // Construtor padrão
Extrato extrato2 = new Extrato(2, "789012"); // Construtor com 2 parâmetros
Extrato extrato3 = new Extrato(3, "345678", "Maria Souza"); // Construtor com 3 parâmetros
```

#### Chamando um Construtor a Partir de Outro (Keyword `this`)
Em C#, você pode reutilizar um construtor chamando outro construtor da mesma classe utilizando a palavra-chave `this`. Isso evita a duplicação de código quando os construtores têm lógica semelhante.

##### Exemplo de Chamada de Construtor:

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }

    // Construtor principal
    public Extrato(int id, string numeroConta, string nomeTitular)
    {
        ID = id;
        NumeroConta = numeroConta;
        NomeTitular = nomeTitular;
    }

    // Construtor com 2 parâmetros reutilizando o construtor principal
    public Extrato(int id, string numeroConta) : this(id, numeroConta, "Desconhecido") { }

    // Construtor padrão reutilizando o construtor com 2 parâmetros
    public Extrato() : this(0, "000000") { }
}
```

Neste exemplo, os construtores de 2 e 0 parâmetros reutilizam o construtor de 3 parâmetros usando `this`.

##### Instanciando Objetos com Construtores Encadeados:

```csharp
Extrato extrato1 = new Extrato(); // ID = 0, NumeroConta = "000000", NomeTitular = "Desconhecido"
Extrato extrato2 = new Extrato(2, "789012"); // NomeTitular = "Desconhecido"
Extrato extrato3 = new Extrato(3, "345678", "Maria Souza"); // Todos os valores definidos
```


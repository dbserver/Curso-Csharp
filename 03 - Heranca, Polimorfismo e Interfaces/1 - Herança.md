### Herança: Conceito e Aplicação

A **herança** é um dos pilares fundamentais da programação orientada a objetos (POO) e permite que uma classe "filha" herde atributos e métodos de uma classe "pai". Isso promove a reutilização de código, facilita a manutenção e permite criar hierarquias de classes mais organizadas. Além disso, a herança possibilita que uma classe filha estenda ou modifique o comportamento da classe pai.

No .NET, várias classes fazem uso da herança, especialmente para tratar erros e exceções, sendo `Exception` uma das mais importantes.

### Conceito de Herança

A herança permite que uma classe derive de outra, estabelecendo uma relação de "é um". Quando uma classe herda de outra, ela herda todos os atributos e métodos públicos e protegidos da classe pai, podendo também sobrescrever esses métodos e adicionar novos comportamentos.

- **Classe Pai**: Também chamada de superclasse ou classe base, é a classe da qual outras classes derivam.
- **Classe Filha**: Também chamada de subclasse ou classe derivada, é a classe que herda de outra classe.

#### Exemplo Simples de Herança

```csharp
public class Animal
{
    public string Nome { get; set; }
    
    public Animal(string nome)
    {
        Nome = nome;
    }

    public void Comer()
    {
        Console.WriteLine($"{Nome} está comendo.");
    }
}

public class Cachorro : Animal
{
    public Cachorro(string nome) : base(nome)
    {
    }

    public void Latir()
    {
        Console.WriteLine($"{Nome} está latindo.");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        Cachorro cachorro = new Cachorro("Rex");
        cachorro.Comer(); // Herdado da classe Animal
        cachorro.Latir(); // Método específico da classe Cachorro
    }
}
```

Neste exemplo, a classe `Cachorro` herda a classe `Animal`, portanto, o cachorro pode "comer" (comportamento herdado) e "latir" (comportamento específico de `Cachorro`).

### Aplicação de Herança com `Exception` e `ArgumentException`

No .NET, a classe `Exception` é a base para todas as exceções, e diversas classes derivam dela, como `ArgumentException`, `InvalidOperationException`, entre outras. A herança é aplicada aqui para criar diferentes tipos de exceções que permitem uma manipulação mais específica de erros.

#### Classe `Exception`

A classe `Exception` é a classe base para todas as exceções no .NET. Ela contém membros comuns a todas as exceções, como a mensagem de erro (`Message`), a pilha de execução (`StackTrace`), e métodos para tratar e manipular exceções.

```csharp
try
{
    throw new Exception("Ocorreu um erro genérico.");
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

#### Classe `ArgumentException`

A classe `ArgumentException` herda de `SystemException` e é utilizada para indicar que um argumento inválido foi passado para um método. Ela também possui propriedades específicas, como `ParamName`, que indica qual parâmetro causou a exceção.

```csharp
public class Calculadora
{
    public int Dividir(int numerador, int denominador)
    {
        if (denominador == 0)
        {
            throw new ArgumentException("O denominador não pode ser zero.", nameof(denominador));
        }

        return numerador / denominador;
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        try
        {
            Calculadora calc = new Calculadora();
            int resultado = calc.Dividir(10, 0); // Isso vai lançar uma exceção ArgumentException
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine($"Erro: {ex.Message}");
            Console.WriteLine($"Parâmetro inválido: {ex.ParamName}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Erro Genérico: {ex.Message}");            
        }

    }
}
```

#### Sobrescrevendo Métodos da Classe Pai

Em herança, é possível sobrescrever métodos da classe pai para alterar ou expandir seu comportamento. No caso das exceções, podemos sobrescrever o método `Message` para fornecer uma mensagem mais específica.

```csharp
public class MinhaExcecaoPersonalizada : Exception
{
    public MinhaExcecaoPersonalizada(string message) : base(message)
    {
    }

    public override string Message
    {
        get
        {
            return $"MinhaExceção: {base.Message}";
        }
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        try
        {
            throw new MinhaExcecaoPersonalizada("Um erro ocorreu.");
        }
        catch (MinhaExcecaoPersonalizada ex)
        {
            Console.WriteLine(ex.Message);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Erro Genérico: {ex.Message}");            
        }
    }
}
```

### Vantagens da Herança

- **Reutilização de Código**: Ao usar herança, não precisamos reescrever código que já existe na classe pai.
- **Organização**: A herança ajuda a organizar o código em uma hierarquia lógica, tornando o design mais intuitivo.
- **Extensibilidade**: Podemos estender o comportamento de uma classe sem alterar seu código diretamente, utilizando subclasses.

### Quando Usar a Herança

- Quando há uma clara relação de "é um" entre a classe pai e a classe filha.
- Quando desejamos reutilizar funcionalidades já existentes em uma classe base.
- Para modelar comportamentos genéricos na classe pai e comportamentos específicos na classe filha.

### Quando Evitar a Herança

- Se as classes não têm uma relação clara entre elas. Nesse caso, pode ser mais adequado usar **composição** ao invés de herança.
- Se a herança causar uma estrutura de classes muito complexa e difícil de entender.

### Exercício: Implementação de Exceções Personalizadas

1. Crie uma classe `ExtratoInvalidoException` que herde de `ArgumentException` e adicione uma mensagem personalizada quando o `NUMEROCONTA` for nulo ou vazio.
2. Crie uma classe `RegistroInvalidoException` que herde de `Exception` e seja lançada quando o valor do `REGISTRO` for menor que zero.

#### Exemplo:

```csharp
public class ExtratoInvalidoException : ArgumentException
{
    public ExtratoInvalidoException(string message, string paramName) : base(message, paramName)
    {
    }
}

public class RegistroInvalidoException : Exception
{
    public RegistroInvalidoException(string message) : base(message)
    {
    }
}

public class Registro
{
    public int ID { get; set; }
    public decimal Valor { get; set; }

    public void ValidarValor()
    {
        if (Valor < 0)
        {
            throw new RegistroInvalidoException("O valor do registro não pode ser negativo.");
        }
    }
}

public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }

    public void ValidarNumeroConta()
    {
        if (string.IsNullOrEmpty(NumeroConta))
        {
            throw new ExtratoInvalidoException("O número da conta é inválido.", nameof(NumeroConta));
        }
    }
}
```

Essa implementação demonstra como herdar de exceções base para criar exceções mais específicas e tratá-las adequadamente, promovendo um código mais claro e específico.

---

Esse exemplo de herança com `Exception` e `ArgumentException` mostra como aproveitar o conceito de herança na criação de exceções personalizadas.
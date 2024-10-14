### Polimorfismo: Conceito de Sobrescrita e Sobrecarga de Métodos

O **polimorfismo** é um dos pilares fundamentais da programação orientada a objetos. Ele permite que objetos de diferentes classes sejam tratados de maneira uniforme, enquanto cada classe pode ter sua própria implementação de métodos. Existem dois tipos principais de polimorfismo: **sobrescrita de métodos** (runtime) e **sobrecarga de métodos** (compile-time).

#### 1. **Sobrescrita de Métodos (Override)**

A sobrescrita de métodos ocorre quando uma classe derivada redefine um método de uma classe base. Isso é útil quando queremos que a classe derivada tenha um comportamento específico, mas que seja tratada da mesma forma que a classe base.

### Exemplo de Sobrescrita de Métodos

Neste exemplo, temos uma classe base `Animal` com um método virtual `EmitirSom()`. As classes derivadas `Cachorro` e `Gato` sobrescrevem esse método para implementar sons específicos para cada animal.

```csharp
public class Animal
{
    public string Nome { get; set; }

    public Animal(string nome)
    {
        Nome = nome;
    }

    // Método virtual que pode ser sobrescrito nas classes derivadas
    public virtual void EmitirSom()
    {
        Console.WriteLine("Animal está fazendo um som.");
    }
}

public class Cachorro : Animal
{
    public Cachorro(string nome) : base(nome) { }

    // Sobrescrevendo o método EmitirSom
    public override void EmitirSom()
    {
        Console.WriteLine($"{Nome} está latindo: Au Au!");
    }
}

public class Gato : Animal
{
    public Gato(string nome) : base(nome) { }

    // Sobrescrevendo o método EmitirSom
    public override void EmitirSom()
    {
        Console.WriteLine($"{Nome} está miando: Miau!");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        Animal animal = new Animal("Animal");
        animal.EmitirSom();

        Animal cachorro = new Cachorro("Rex");
        cachorro.EmitirSom();

        Animal gato = new Gato("Felix");
        gato.EmitirSom();
    }
}
```

#### Saída:

```
Animal está fazendo um som.
Rex está latindo: Au Au!
Felix está miando: Miau!
```

Nesse exemplo, embora `cachorro` e `gato` sejam do tipo `Animal`, eles chamam suas próprias implementações de `EmitirSom()`, exibindo o comportamento adequado para cada subclasse.

---

#### 2. **Sobrecarga de Métodos (Overload)**

A sobrecarga de métodos ocorre quando dois ou mais métodos têm o mesmo nome, mas aceitam diferentes parâmetros. O compilador escolhe qual método chamar com base nos tipos e na quantidade de argumentos passados.

### Exemplo de Sobrecarga de Métodos

Vamos criar uma classe `Calculadora` que sobrecarrega o método `Somar()`, permitindo somar números inteiros e números de ponto flutuante.

```csharp
public class Calculadora
{
    // Sobrecarga para soma de inteiros
    public int Somar(int a, int b)
    {
        return a + b;
    }

    // Sobrecarga para soma de números decimais
    public decimal Somar(decimal a, decimal b)
    {
        return a + b;
    }

    // Sobrecarga para soma de três inteiros
    public int Somar(int a, int b, int c)
    {
        return a + b + c;
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        Calculadora calc = new Calculadora();

        int resultado1 = calc.Somar(5, 10);              // Chama a versão com inteiros
        decimal resultado2 = calc.Somar(3.5m, 2.2m);     // Chama a versão com decimais
        int resultado3 = calc.Somar(1, 2, 3);            // Chama a versão com três inteiros

        Console.WriteLine($"Resultado 1: {resultado1}");
        Console.WriteLine($"Resultado 2: {resultado2}");
        Console.WriteLine($"Resultado 3: {resultado3}");
    }
}
```

#### Saída:

```
Resultado 1: 15
Resultado 2: 5.7
Resultado 3: 6
```

Aqui, a classe `Calculadora` define três versões do método `Somar()` que aceitam diferentes tipos e números de parâmetros, mostrando como a sobrecarga funciona.

---

### Comparação: Sobrescrita vs Sobrecarga

| Característica             | Sobrescrita                                | Sobrecarga                                     |
|----------------------------|--------------------------------------------|------------------------------------------------|
| Contexto                    | Ocorre em herança                          | Ocorre na mesma classe                         |
| Propósito                   | Alterar o comportamento de um método herdado| Definir múltiplas versões de um método         |
| Parâmetros                  | Deve ter a mesma assinatura que o método base | Diferentes assinaturas (número ou tipo)       |
| Palavra-chave               | `override` (opcional se `virtual`)         | Não requer palavra-chave específica            |
| Tempo de execução           | Decidido em tempo de execução               | Decidido em tempo de compilação                |

---

### Exemplo de Sobrescrita e Sobrecarga Juntas

Para mostrar como sobrecarga e sobrescrita podem coexistir, vamos adicionar métodos sobrecarregados à nossa classe `Animal`.

```csharp
public class Animal
{
    public string Nome { get; set; }

    public Animal(string nome)
    {
        Nome = nome;
    }

    public virtual void EmitirSom()
    {
        Console.WriteLine("Animal está fazendo um som.");
    }

    // Sobrecarga de método EmitirSom com parâmetro
    public void EmitirSom(int vezes)
    {
        for (int i = 0; i < vezes; i++)
        {
            Console.WriteLine("Animal está fazendo um som.");
        }
    }
}

public class Cachorro : Animal
{
    public Cachorro(string nome) : base(nome) { }

    public override void EmitirSom()
    {
        Console.WriteLine($"{Nome} está latindo: Au Au!");
    }

    // Sobrecarga de método EmitirSom com parâmetro
    public void EmitirSom(int vezes)
    {
        for (int i = 0; i < vezes; i++)
        {
            Console.WriteLine($"{Nome} está latindo: Au Au!");
        }
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        Cachorro rex = new Cachorro("Rex");

        // Sobrescrita
        rex.EmitirSom();

        // Sobrecarga
        rex.EmitirSom(3);
    }
}
```

#### Saída:

```
Rex está latindo: Au Au!
Rex está latindo: Au Au!
Rex está latindo: Au Au!
Rex está latindo: Au Au!
```

Aqui, temos uma combinação de **sobrecarga** e **sobrescrita** no método `EmitirSom()`. O método foi sobrescrito em `Cachorro` e também sobrecarregado com uma versão que aceita um número inteiro para indicar quantas vezes o som deve ser emitido.

---
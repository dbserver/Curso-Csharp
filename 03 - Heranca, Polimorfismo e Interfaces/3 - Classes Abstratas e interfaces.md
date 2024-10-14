### Classes Abstratas e Interfaces: Conceitos

#### 1. Classes Abstratas

Uma **classe abstrata** é uma classe que não pode ser instanciada diretamente. Seu propósito é servir como uma base para outras classes. As classes abstratas podem conter métodos abstratos (sem implementação) e métodos concretos (com implementação). Elas permitem que você defina um comportamento comum que deve ser implementado pelas subclasses.

##### Características de Classes Abstratas:
- **Não podem ser instanciadas:** Você não pode criar um objeto diretamente a partir de uma classe abstrata.
- **Métodos Abstratos:** Uma classe abstrata pode ter métodos abstratos que devem ser implementados pelas classes derivadas.
- **Métodos Concretos:** Além de métodos abstratos, também pode ter métodos concretos que fornecem implementação padrão.
- **Construtores:** Classes abstratas podem ter construtores, que podem ser chamados pelas classes derivadas.

##### Exemplo de Classe Abstrata

```csharp
public abstract class Animal
{
    public string Nome { get; set; }

    public Animal(string nome)
    {
        Nome = nome;
    }

    // Método abstrato
    public abstract void EmitirSom();

    // Método concreto
    public void Dormir()
    {
        Console.WriteLine($"{Nome} está dormindo.");
    }
}

public class Cachorro : Animal
{
    public Cachorro(string nome) : base(nome) { }

    // Implementação do método abstrato
    public override void EmitirSom()
    {
        Console.WriteLine($"{Nome} está latindo: Au Au!");
    }
}

public class Gato : Animal
{
    public Gato(string nome) : base(nome) { }

    // Implementação do método abstrato
    public override void EmitirSom()
    {
        Console.WriteLine($"{Nome} está miando: Miau!");
    }
}
```

##### Uso da Classe Abstrata

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        Animal cachorro = new Cachorro("Rex");
        cachorro.EmitirSom(); // Saída: Rex está latindo: Au Au!
        cachorro.Dormir();     // Saída: Rex está dormindo.

        Animal gato = new Gato("Felix");
        gato.EmitirSom();     // Saída: Felix está miando: Miau!
        gato.Dormir();        // Saída: Felix está dormindo.
    }
}
```

#### 2. Interfaces

Uma **interface** é um contrato que define um conjunto de métodos e propriedades que uma classe deve implementar. As interfaces não podem conter implementações de métodos (a partir de C# 8.0, elas podem ter métodos padrão, mas a ideia principal de uma interface ainda é ser um contrato). Uma classe pode implementar várias interfaces, permitindo que diferentes classes compartilhem o mesmo conjunto de métodos.

##### Características de Interfaces:
- **Não podem ter implementação:** As interfaces não contêm implementações de métodos, apenas suas declarações.
- **Múltipla Implementação:** Uma classe pode implementar várias interfaces, permitindo a reutilização do código e flexibilidade.
- **Propriedades e Eventos:** Interfaces podem incluir declarações de propriedades, eventos e indexadores, além de métodos.

##### Exemplo de Interface

```csharp
public interface IAnimal
{
    void EmitirSom();
    void Dormir();
}

public class Cachorro : IAnimal
{
    public void EmitirSom()
    {
        Console.WriteLine("Au Au!");
    }

    public void Dormir()
    {
        Console.WriteLine("Cachorro está dormindo.");
    }
}

public class Gato : IAnimal
{
    public void EmitirSom()
    {
        Console.WriteLine("Miau!");
    }

    public void Dormir()
    {
        Console.WriteLine("Gato está dormindo.");
    }
}
```

##### Uso da Interface

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        IAnimal cachorro = new Cachorro();
        cachorro.EmitirSom(); // Saída: Au Au!
        cachorro.Dormir();     // Saída: Cachorro está dormindo.

        IAnimal gato = new Gato();
        gato.EmitirSom();     // Saída: Miau!
        gato.Dormir();        // Saída: Gato está dormindo.
    }
}
```

### Comparação: Classes Abstratas vs Interfaces

| Característica               | Classes Abstratas                      | Interfaces                              |
|------------------------------|----------------------------------------|-----------------------------------------|
| Instanciação                 | Não pode ser instanciada               | Não pode ser instanciada                |
| Métodos Abstratos            | Sim                                    | Não (apenas declarações de métodos)    |
| Múltipla Herança             | Não (uma única classe base)           | Sim (uma classe pode implementar várias)|
| Implementação de Métodos     | Pode ter métodos concretos             | Sim apartir do  C# 8.0|
| Propriedades                  | Pode ter propriedades                  | Pode ter propriedades                   |
| Construtores                 | Pode ter construtores                  | Não pode ter construtores               |

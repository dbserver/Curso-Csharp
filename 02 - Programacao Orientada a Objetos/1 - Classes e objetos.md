### Classes e Objetos em C#

#### Definição de Classes
Uma **classe** em C# é uma estrutura de código que define um tipo de dado, que contém propriedades (dados) e métodos (funções ou comportamentos). Ela serve como um molde ou um plano para criar objetos, encapsulando dados e comportamentos. 

A **sintaxe básica** de uma classe em C# é:

```csharp
public class NomeDaClasse
{
    // Definição de propriedades
    public int Propriedade1 { get; set; }
    public string Propriedade2 { get; set; }

    // Definição de métodos
    public void Metodo1()
    {
        // Comportamento do método
    }
}
```

#### Criação de Classes e Instâncias de Objetos
A seguir, vamos utilizar as entidades sugeridas para exemplificar.

##### Entidade: **EXTRATO**

```csharp
public class Extrato
{
    public int ID { get; set; }
    public string NumeroConta { get; set; }
    public string NomeTitular { get; set; }    

    // Método para exibir detalhes do extrato
    public void ExibirDetalhes()
    {
        Console.WriteLine($"ID: {ID}, Conta: {NumeroConta}, Titular: {NomeTitular}");
    }
}
```


#### Instanciação de Objetos

Agora que temos as classes definidas, vamos ver como podemos **instanciar** objetos a partir delas. Em C#, instanciar um objeto é o processo de criar uma cópia concreta de uma classe na memória.

```csharp
class Program
{
    static void Main(string[] args)
    {
        // Instanciando um objeto da classe Extrato
        Extrato extrato1 = new Extrato();
        extrato1.ID = 1;
        extrato1.NumeroConta = "123456";
        extrato1.NomeTitular = "João da Silva";
        extrato1.ExibirDetalhes();
    }
}
```

##### Saída Esperada:

```
ID: 1, Conta: 123456, Titular: João da Silva
```

### Explicação Técnica

#### Propriedades
As **propriedades** (`ID`, `NumeroConta`, `Valor`, etc.) permitem encapsular os dados da classe, fornecendo uma maneira controlada de acessar e modificar esses valores. Usamos a convenção `get` e `set` para permitir a leitura e a modificação dessas propriedades:

```csharp
public int ID { get; set; }
```

#### Métodos
Os **métodos** são usados para definir o comportamento das classes. No exemplo, o método `ExibirDetalhes` exibe os dados armazenados na classe para o usuário:

```csharp
public void ExibirDetalhes()
{
    Console.WriteLine($"ID: {ID}, Conta: {NumeroConta}, Titular: {NomeTitular}");
}
```

#### Instância de Objetos
Quando criamos um objeto, como:

```csharp
Extrato extrato1 = new Extrato();
```

Estamos criando uma **instância** da classe `Extrato`, e o método construtor é automaticamente chamado para inicializar o objeto.

#### Visibilidade de Propriedades e Métodos
Em C#, usamos modificadores de acesso como `public` e `private` para definir a **visibilidade** das propriedades e métodos. No exemplo, as propriedades e métodos são públicos, o que significa que podem ser acessados de qualquer parte do código. No entanto, você pode querer restringir o acesso em alguns casos, por exemplo:

```csharp
private string NomeTitular { get; set; }
```

Aqui, `NomeTitular` só pode ser acessado e modificado dentro da própria classe `Extrato`.

### Documentação e Comentários

É importante adicionar **comentários** e documentar suas classes e métodos para garantir que outros desenvolvedores (ou você mesmo no futuro) compreendam o código com facilidade.

```csharp
/// <summary>
/// Representa um extrato bancário.
/// </summary>
public class Extrato
{
    /// <summary>
    /// Identificador único do extrato.
    /// </summary>
    public int ID { get; set; }

    /// <summary>
    /// Número da conta bancária associada ao extrato.
    /// </summary>
    public string NumeroConta { get; set; }

    /// <summary>
    /// Nome do titular da conta.
    /// </summary>
    public string NomeTitular { get; set; }

    /// <summary>
    /// Exibe os detalhes do extrato.
    /// </summary>
    public void ExibirDetalhes()
    {
        Console.WriteLine($"ID: {ID}, Conta: {NumeroConta}, Titular: {NomeTitular}");
    }
}
```
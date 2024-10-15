### Exceções Personalizadas

As exceções personalizadas são uma maneira eficaz de gerenciar erros em seu código. Elas permitem que você defina suas próprias condições de erro, fornecendo mensagens claras e específicas sobre o que deu errado. Isso é especialmente útil em aplicações complexas, onde as exceções padrão do .NET podem não ser suficientes para descrever problemas específicos de negócio ou lógicas de sua aplicação.

### Por Que Usar Exceções Personalizadas?

1. **Clareza**: Fornecem mensagens de erro mais claras e significativas em comparação com as exceções padrão.
2. **Especificidade**: Permitem que você categorize erros de maneira mais precisa, facilitando o tratamento de exceções em diferentes partes do seu código.
3. **Manutenção**: Facilitam a manutenção do código, uma vez que você pode gerenciar erros de maneira centralizada.

### Criando Exceções Personalizadas

Para criar uma exceção personalizada em C#, você precisa herdar da classe `Exception` ou de uma de suas subclasses. Aqui está a estrutura básica:

```csharp
public class MinhaExcecaoPersonalizada : Exception
{
    public MinhaExcecaoPersonalizada() { }

    public MinhaExcecaoPersonalizada(string mensagem) : base(mensagem) { }

    public MinhaExcecaoPersonalizada(string mensagem, Exception innerException)
        : base(mensagem, innerException) { }
}
```

### Exemplo de Exceção Personalizada

Vamos criar um exemplo prático para ilustrar como usar exceções personalizadas em um cenário de validação de entradas.

#### Cenário: Validação de Saldo em Conta

Imagine que você está desenvolvendo um sistema bancário e deseja garantir que um usuário não tente retirar mais dinheiro do que tem em sua conta. Para isso, você pode criar uma exceção personalizada chamada `SaldoInsuficienteException`.

```csharp
using System;

public class SaldoInsuficienteException : Exception
{
    public SaldoInsuficienteException() : base("Saldo insuficiente para realizar esta operação.") { }

    public SaldoInsuficienteException(decimal saldo, decimal valorTentativa)
        : base($"Tentativa de saque de {valorTentativa:C} com saldo disponível de {saldo:C}.") { }
}

public class ContaBancaria
{
    public decimal Saldo { get; private set; }

    public ContaBancaria(decimal saldoInicial)
    {
        Saldo = saldoInicial;
    }

    public void Sacar(decimal valor)
    {
        if (valor > Saldo)
        {
            throw new SaldoInsuficienteException(Saldo, valor);
        }
        Saldo -= valor;
        Console.WriteLine($"Saque de {valor:C} realizado com sucesso. Saldo atual: {Saldo:C}");
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            ContaBancaria conta = new ContaBancaria(100);
            Console.WriteLine("Saldo inicial: " + conta.Saldo);
            conta.Sacar(150); // Tentativa de saque que causará exceção
        }
        catch (SaldoInsuficienteException ex)
        {
            Console.WriteLine($"Erro: {ex.Message}");
        }
        finally
        {
            Console.WriteLine("Operação de saque finalizada.");
        }
    }
}
```

### Explicação do Exemplo

1. **Classe `SaldoInsuficienteException`**: Esta classe herda de `Exception` e tem dois construtores:
   - Um construtor padrão que fornece uma mensagem padrão.
   - Um segundo construtor que aceita o saldo atual e o valor da tentativa de saque, fornecendo uma mensagem personalizada.

2. **Classe `ContaBancaria`**: Esta classe representa uma conta bancária e tem um método `Sacar`, que verifica se há saldo suficiente. Se não houver, ela lança a exceção `SaldoInsuficienteException`.

3. **Tratamento de Exceção**: No método `Main`, uma conta bancária é criada com um saldo de 100. Ao tentar sacar 150, uma `SaldoInsuficienteException` é lançada e capturada, exibindo a mensagem de erro apropriada.


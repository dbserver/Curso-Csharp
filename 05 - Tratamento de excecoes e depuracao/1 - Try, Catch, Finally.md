### Lançando Exceções

Em C#, você pode lançar exceções manualmente usando a palavra-chave `throw`. Isso é útil quando você deseja interromper a execução normal do código em resposta a uma condição específica, como um erro de entrada ou uma violação de regra de negócios. Ao lançar uma exceção, você pode fornecer informações sobre o erro que ocorreu, permitindo que outras partes do seu código tratem essa exceção adequadamente.

### Estrutura Básica do `throw`

A sintaxe básica para lançar uma exceção é a seguinte:

```csharp
throw new TipoDaExcecao("Mensagem de erro");
```

Você pode lançar exceções personalizadas ou as exceções integradas fornecidas pelo .NET, como `ArgumentNullException`, `InvalidOperationException`, etc.

### Exemplo Prático

Vamos ver um exemplo prático que ilustra como lançar exceções em C#.

#### Exemplo: Validação de Entrada do Usuário

Neste exemplo, criaremos um método que aceita um número inteiro positivo. Se o número fornecido não for positivo, lançaremos uma `ArgumentOutOfRangeException`.

```csharp
using System;

public class Program
{
    public static void Main()
    {
        try
        {
            Console.Write("Digite um número positivo: ");
            int numero = int.Parse(Console.ReadLine());
            ValidarNumeroPositivo(numero);
            Console.WriteLine("Número válido: " + numero);
        }
        catch (ArgumentOutOfRangeException ex)
        {
            Console.WriteLine($"Erro: {ex.Message}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine("Erro: O valor digitado não é um número válido.");
        }
        finally
        {
            Console.WriteLine("Finalizando o programa.");
        }
    }

    public static void ValidarNumeroPositivo(int numero)
    {
        if (numero <= 0)
        {
            throw new ArgumentOutOfRangeException(nameof(numero), "O número deve ser maior que zero.");
        }
    }
}
```

### Explicação do Exemplo

1. **Entrada do Usuário**: O programa solicita que o usuário insira um número.
2. **Validação**: O método `ValidarNumeroPositivo` verifica se o número é maior que zero.
3. **Lançamento de Exceção**: Se o número não for positivo, o método lança uma `ArgumentOutOfRangeException` com uma mensagem que descreve o erro.
4. **Tratamento de Exceções**:
   - O bloco `catch` correspondente captura a exceção lançada e exibe a mensagem de erro.
   - Um bloco `catch` adicional captura erros de formato caso o usuário insira um valor que não possa ser convertido em inteiro.
5. **Bloco `finally`**: Este bloco sempre será executado, independentemente de uma exceção ter ocorrido ou não.

### Lançando Exceções Personalizadas

Além das exceções integradas, você pode criar suas próprias exceções personalizadas. Para isso, você deve herdar da classe `Exception`.

#### Exemplo de Exceção Personalizada

```csharp
using System;

public class NumeroInvalidoException : Exception
{
    public NumeroInvalidoException(string mensagem) : base(mensagem)
    {
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            Console.Write("Digite um número positivo: ");
            int numero = int.Parse(Console.ReadLine());
            ValidarNumeroPositivo(numero);
            Console.WriteLine("Número válido: " + numero);
        }
        catch (NumeroInvalidoException ex)
        {
            Console.WriteLine($"Erro: {ex.Message}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine("Erro: O valor digitado não é um número válido.");
        }
        finally
        {
            Console.WriteLine("Finalizando o programa.");
        }
    }

    public static void ValidarNumeroPositivo(int numero)
    {
        if (numero <= 0)
        {
            throw new NumeroInvalidoException("O número deve ser maior que zero.");
        }
    }
}
```

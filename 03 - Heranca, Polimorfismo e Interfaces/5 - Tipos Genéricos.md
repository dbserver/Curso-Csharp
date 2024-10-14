### Tipos Genéricos: Classes e Métodos Genéricos em C#

Os tipos genéricos são uma funcionalidade poderosa da linguagem C# que permite a definição de classes, interfaces e métodos que funcionam com qualquer tipo de dado. Essa flexibilidade promove a reutilização de código e a criação de estruturas de dados mais robustas e eficientes. Neste tópico, vamos explorar como criar classes e métodos genéricos em C#, incluindo exemplos práticos.

### 1. Classes Genéricas

As classes genéricas permitem que você defina uma classe com um ou mais parâmetros de tipo. Esses parâmetros podem ser utilizados em todo o corpo da classe, proporcionando uma maneira eficiente de trabalhar com diferentes tipos de dados.

#### Exemplo de Classe Genérica

```csharp
public class Caixa<T>
{
    private T conteudo;

    public void AdicionarConteudo(T item)
    {
        conteudo = item;
    }

    public T ObterConteudo()
    {
        return conteudo;
    }
}
```

#### Uso da Classe Genérica

```csharp
public class Program
{
    public static void Main()
    {
        // Criando uma caixa de inteiros
        var caixaInt = new Caixa<int>();
        caixaInt.AdicionarConteudo(42);
        Console.WriteLine($"Conteúdo da caixa de int: {caixaInt.ObterConteudo()}");

        // Criando uma caixa de strings
        var caixaString = new Caixa<string>();
        caixaString.AdicionarConteudo("Olá, Mundo!");
        Console.WriteLine($"Conteúdo da caixa de string: {caixaString.ObterConteudo()}");
    }
}
```

### 2. Métodos Genéricos

Além de classes, você também pode definir métodos genéricos. Um método genérico pode aceitar parâmetros de qualquer tipo, tornando-o mais versátil.

#### Exemplo de Método Genérico

```csharp
public class Util
{
    public static void Trocar<T>(ref T a, ref T b)
    {
        T temp = a;
        a = b;
        b = temp;
    }
}
```

#### Uso do Método Genérico

```csharp
public class Program
{
    public static void Main()
    {
        // Troca de inteiros
        int x = 10;
        int y = 20;
        Console.WriteLine($"Antes da troca: x = {x}, y = {y}");
        Util.Trocar(ref x, ref y);
        Console.WriteLine($"Depois da troca: x = {x}, y = {y}");

        // Troca de strings
        string str1 = "primeira";
        string str2 = "segunda";
        Console.WriteLine($"\nAntes da troca: str1 = {str1}, str2 = {str2}");
        Util.Trocar(ref str1, ref str2);
        Console.WriteLine($"Depois da troca: str1 = {str1}, str2 = {str2}");
    }
}
```

### 3. Restrições em Tipos Genéricos

Você pode restringir os tipos que podem ser usados como argumentos para um parâmetro de tipo em uma classe ou método genérico. Isso é útil quando você deseja garantir que apenas tipos específicos sejam utilizados.

#### Exemplo de Restrições

```csharp
public class Comparador<T> where T : IComparable
{
    public T Maior(T a, T b)
    {
        return a.CompareTo(b) > 0 ? a : b;
    }
}
```

#### Uso da Classe com Restrições

```csharp
public class Program
{
    public static void Main()
    {
        var comparador = new Comparador<int>();
        int maiorInt = comparador.Maior(5, 10);
        Console.WriteLine($"O maior número é: {maiorInt}");

        var comparadorString = new Comparador<string>();
        string maiorString = comparadorString.Maior("Maçã", "Banana");
        Console.WriteLine($"A maior string é: {maiorString}");
    }
}
```
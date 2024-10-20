### Leitura e Escrita em Arquivos em C#

Manipular arquivos é uma tarefa essencial em muitas aplicações, como a leitura de configurações, geração de relatórios, processamento de logs, e muito mais. Em C#, as classes **StreamReader** e **StreamWriter** fornecem uma maneira eficiente de trabalhar com arquivos de texto, permitindo que os desenvolvedores leiam e escrevam dados de forma sequencial.

Nesta seção, exploraremos os conceitos fundamentais de leitura e escrita em arquivos utilizando as classes `StreamReader` e `StreamWriter`. Além disso, vamos explorar boas práticas e algumas nuances para melhorar o desempenho e a robustez ao manipular arquivos.

---

### 1. Introdução às Classes StreamReader e StreamWriter

#### 1.1 StreamReader

A classe **StreamReader** é usada para **ler arquivos de texto**. Ela oferece métodos que permitem ler caracteres, linhas ou todo o conteúdo de um arquivo. A leitura é feita de maneira sequencial, ou seja, o leitor começa a ler do início do arquivo e continua até o final ou até a leitura ser interrompida.

#### 1.2 StreamWriter

A classe **StreamWriter** é usada para **escrever em arquivos de texto**. Assim como o `StreamReader`, a escrita é sequencial, ou seja, o conteúdo é gravado no arquivo em ordem, a partir do início ou do ponto em que a gravação foi interrompida.

---

### 2. Trabalhando com StreamReader

#### 2.1 Leitura Básica de Arquivos

Para ler arquivos, primeiro é necessário criar uma instância da classe `StreamReader` e, em seguida, utilizar os métodos disponíveis para ler o conteúdo. O exemplo a seguir demonstra a leitura de um arquivo linha por linha:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string caminhoArquivo = "exemplo.txt";
        
        // Verificar se o arquivo existe antes de tentar lê-lo
        if (File.Exists(caminhoArquivo))
        {
            // Criar uma instância de StreamReader para ler o arquivo
            using (StreamReader sr = new StreamReader(caminhoArquivo))
            {
                string linha;

                // Ler o arquivo linha por linha
                while ((linha = sr.ReadLine()) != null)
                {
                    Console.WriteLine(linha);
                }
            }
        }
        else
        {
            Console.WriteLine("O arquivo não foi encontrado.");
        }
    }
}
```

#### Explicação do Código:
1. **Verificação de Existência**: Antes de tentar ler o arquivo, o método `File.Exists` é usado para verificar se o arquivo realmente existe.
2. **Bloco `using`**: O `StreamReader` é utilizado dentro de um bloco `using` para garantir que o arquivo será fechado automaticamente após a leitura.
3. **`sr.ReadLine()`**: Este método lê o arquivo linha por linha até chegar ao final (`null`).

#### 2.2 Leitura de Todo o Conteúdo de Uma Vez

Se o arquivo for pequeno ou se quisermos ler o conteúdo de uma única vez, podemos utilizar o método `ReadToEnd` da classe `StreamReader`:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string caminhoArquivo = "exemplo.txt";

        if (File.Exists(caminhoArquivo))
        {
            using (StreamReader sr = new StreamReader(caminhoArquivo))
            {
                // Ler todo o conteúdo do arquivo de uma vez
                string conteudo = sr.ReadToEnd();
                Console.WriteLine(conteudo);
            }
        }
        else
        {
            Console.WriteLine("O arquivo não foi encontrado.");
        }
    }
}
```

---

### 3. Trabalhando com StreamWriter

#### 3.1 Escrita Básica em Arquivos

A classe `StreamWriter` é usada para gravar texto em um arquivo. Assim como na leitura, podemos escrever linha por linha ou todo o conteúdo de uma vez. O exemplo a seguir mostra como escrever texto em um arquivo:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string caminhoArquivo = "exemplo.txt";

        // Criar ou sobrescrever o arquivo exemplo.txt
        using (StreamWriter sw = new StreamWriter(caminhoArquivo))
        {
            // Escrever uma linha no arquivo
            sw.WriteLine("Este é um exemplo de escrita com StreamWriter.");
            
            // Escrever várias linhas no arquivo
            sw.WriteLine("Linha 1");
            sw.WriteLine("Linha 2");
            sw.WriteLine("Linha 3");
        }

        Console.WriteLine("Texto gravado com sucesso no arquivo.");
    }
}
```

#### Explicação do Código:
1. **Sobrescrita Automática**: O `StreamWriter` sobrescreve o arquivo existente por padrão. Se o arquivo não existir, ele será criado.
2. **Bloco `using`**: Assim como no `StreamReader`, o uso do bloco `using` garante que o arquivo será fechado automaticamente após a escrita.
3. **`sw.WriteLine()`**: O método `WriteLine` é usado para gravar uma linha de texto no arquivo. Ele adiciona automaticamente uma nova linha ao final.

#### 3.2 Acrescentando Dados ao Final de um Arquivo (Append)

Para adicionar dados ao final de um arquivo sem sobrescrevê-lo, podemos usar um dos sobrecargas do `StreamWriter` que aceita um segundo parâmetro `true`, indicando que queremos **acrescentar** o texto ao arquivo existente:

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string caminhoArquivo = "exemplo.txt";

        // Abrir o arquivo em modo de append (acrescentar)
        using (StreamWriter sw = new StreamWriter(caminhoArquivo, true))
        {
            sw.WriteLine("Esta linha será adicionada ao final do arquivo.");
        }

        Console.WriteLine("Texto adicionado ao arquivo com sucesso.");
    }
}
```

---

### 4. Tratamento de Exceções

É importante sempre prever a possibilidade de erros ao manipular arquivos, como permissões insuficientes ou o arquivo estar em uso por outro processo. Para lidar com esses cenários, podemos utilizar blocos **try-catch**.

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string caminhoArquivo = "exemplo.txt";

        try
        {
            using (StreamWriter sw = new StreamWriter(caminhoArquivo))
            {
                sw.WriteLine("Escrevendo em um arquivo.");
            }
        }
        catch (UnauthorizedAccessException e)
        {
            Console.WriteLine($"Erro de permissão: {e.Message}");
        }
        catch (IOException e)
        {
            Console.WriteLine($"Erro de I/O: {e.Message}");
        }
    }
}
```

#### Principais Exceções:
- **UnauthorizedAccessException**: Ocorre quando o processo não tem permissão para acessar o arquivo.
- **IOException**: Ocorre quando há um erro de entrada/saída, como o arquivo estar em uso.

---

### 5. Manipulando Arquivos Grandes

Em alguns casos, você pode precisar lidar com arquivos grandes, onde ler o arquivo inteiro de uma vez não é viável. Para isso, a leitura linha por linha com `StreamReader` é ideal, pois permite processar o arquivo de maneira eficiente, sem sobrecarregar a memória.

#### Exemplo: Leitura Eficiente de Arquivo Grande

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        string caminhoArquivo = "arquivo_grande.txt";

        if (File.Exists(caminhoArquivo))
        {
            using (StreamReader sr = new StreamReader(caminhoArquivo))
            {
                string linha;
                int contador = 0;

                // Ler linha por linha
                while ((linha = sr.ReadLine()) != null)
                {
                    // Processar a linha (apenas como exemplo, imprimir no console)
                    Console.WriteLine($"Linha {++contador}: {linha}");
                    
                    // Se necessário, adicionar lógica para interromper o processamento
                    // por exemplo, após processar 1000 linhas.
                }
            }
        }
        else
        {
            Console.WriteLine("O arquivo não foi encontrado.");
        }
    }
}
```

---

### 6. Escrita de Dados Binários e Manipulação de Fluxos (Avançado)

Embora `StreamReader` e `StreamWriter` sejam usados principalmente para arquivos de texto, C# também permite manipular dados binários com classes como `BinaryReader` e `BinaryWriter`, que são úteis para trabalhar com formatos de arquivo mais complexos.

Aqui, no entanto, estamos focando em texto, então vale a pena lembrar que **`StreamReader`** e **`StreamWriter`** são as escolhas ideais para manipulação simples de arquivos de texto em C#.

---
# Serialization e Deserialization: XML e JSON

A **serialização** é o processo de converter um objeto em um formato que pode ser facilmente armazenado ou transmitido, como JSON ou XML. Esse processo permite que os dados sejam salvos ou enviados em uma forma textual para, mais tarde, serem reconstruídos no formato original através da **desserialização**.

#### Serialização
- **Definição**: Serialização é o ato de transformar um objeto em uma sequência de bytes (ou string), com o intuito de preservar seu estado para armazená-lo em um arquivo, enviá-lo pela rede, ou outro meio de transmissão.
- **Formato Comum**: JSON (JavaScript Object Notation) e XML (eXtensible Markup Language).

#### Desserialização
- **Definição**: O processo de reconstruir o objeto original a partir da sequência de bytes (ou string) serializada.
- **Usos**: Receber dados via APIs, carregar objetos a partir de arquivos, etc.

Em C#, existem várias maneiras de realizar a serialização e a desserialização de dados em XML e JSON. Abaixo exploraremos ambos os formatos com exemplos.

---

### Serialização e Desserialização em JSON

Em C#, a biblioteca mais comum para trabalhar com JSON é o **System.Text.Json**, disponível nas versões mais recentes do .NET. Outra biblioteca popular é o **Newtonsoft.Json**, que oferece suporte a recursos adicionais e é amplamente usada na comunidade.

#### Serialização em JSON

A serialização de objetos em JSON é uma forma eficiente de transformar objetos complexos em uma representação textual.

#### Exemplo de Código:
```csharp
using System;
using System.Text.Json;

class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}

class Program
{
    static void Main()
    {
        Produto produto = new Produto
        {
            Id = 1,
            Nome = "Teclado",
            Preco = 199.99m
        };

        // Serializar o objeto para JSON
        string json = JsonSerializer.Serialize(produto);
        Console.WriteLine("JSON serializado:");
        Console.WriteLine(json);
    }
}
```

#### Saída Esperada:
```json
{
  "Id": 1,
  "Nome": "Teclado",
  "Preco": 199.99
}
```

---

#### Desserialização em JSON

A desserialização é o processo inverso, onde a string JSON é convertida de volta em um objeto.

#### Exemplo de Código:
```csharp
using System;
using System.Text.Json;

class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}

class Program
{
    static void Main()
    {
        string json = "{\"Id\":1,\"Nome\":\"Teclado\",\"Preco\":199.99}";

        // Desserializar o JSON para um objeto
        Produto produto = JsonSerializer.Deserialize<Produto>(json);
        Console.WriteLine("Objeto desserializado:");
        Console.WriteLine($"Id: {produto.Id}, Nome: {produto.Nome}, Preço: {produto.Preco}");
    }
}
```

#### Saída Esperada:
```
Objeto desserializado:
Id: 1, Nome: Teclado, Preço: 199.99
```

### Serialização e Desserialização com Newtonsoft.Json

A biblioteca **Newtonsoft.Json** oferece mais funcionalidades e opções avançadas, como formatação personalizada e controle mais detalhado sobre como os dados são serializados.

#### Exemplo com Newtonsoft.Json:
```csharp
using System;
using Newtonsoft.Json;

class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}

class Program
{
    static void Main()
    {
        Produto produto = new Produto
        {
            Id = 1,
            Nome = "Teclado",
            Preco = 199.99m
        };

        // Serializar o objeto para JSON usando Newtonsoft.Json
        string json = JsonConvert.SerializeObject(produto, Formatting.Indented);
        Console.WriteLine("JSON serializado:");
        Console.WriteLine(json);

        // Desserializar o JSON para um objeto usando Newtonsoft.Json
        Produto desserializado = JsonConvert.DeserializeObject<Produto>(json);
        Console.WriteLine($"Objeto desserializado: {desserializado.Nome}, {desserializado.Preco}");
    }
}
```

---

### Serialização e Desserialização em XML

A serialização e desserialização em XML é comumente usada quando precisamos de uma estrutura hierárquica mais explícita, ou quando lidamos com sistemas legados que ainda utilizam XML como principal formato de troca de dados.

No .NET, a **XmlSerializer** da biblioteca `System.Xml.Serialization` é a classe mais usada para serializar e desserializar objetos em XML.

#### Serialização em XML

#### Exemplo de Código:
```csharp
using System;
using System.IO;
using System.Xml.Serialization;

[Serializable]
public class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}

class Program
{
    static void Main()
    {
        Produto produto = new Produto
        {
            Id = 1,
            Nome = "Teclado",
            Preco = 199.99m
        };

        XmlSerializer serializer = new XmlSerializer(typeof(Produto));
        using (StringWriter writer = new StringWriter())
        {
            // Serializar o objeto para XML
            serializer.Serialize(writer, produto);
            string xml = writer.ToString();
            Console.WriteLine("XML serializado:");
            Console.WriteLine(xml);
        }
    }
}
```

#### Saída Esperada:
```xml
<?xml version="1.0" encoding="utf-16"?>
<Produto xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <Id>1</Id>
  <Nome>Teclado</Nome>
  <Preco>199.99</Preco>
</Produto>
```

---

#### Desserialização em XML

#### Exemplo de Código:
```csharp
using System;
using System.IO;
using System.Xml.Serialization;

[Serializable]
public class Produto
{
    public int Id { get; set; }
    public string Nome { get; set; }
    public decimal Preco { get; set; }
}

class Program
{
    static void Main()
    {
        string xml = @"<?xml version=""1.0"" encoding=""utf-16""?>
        <Produto xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"">
          <Id>1</Id>
          <Nome>Teclado</Nome>
          <Preco>199.99</Preco>
        </Produto>";

        XmlSerializer serializer = new XmlSerializer(typeof(Produto));
        using (StringReader reader = new StringReader(xml))
        {
            // Desserializar o XML para um objeto
            Produto produto = (Produto)serializer.Deserialize(reader);
            Console.WriteLine("Objeto desserializado:");
            Console.WriteLine($"Id: {produto.Id}, Nome: {produto.Nome}, Preço: {produto.Preco}");
        }
    }
}
```

#### Saída Esperada:
```
Objeto desserializado:
Id: 1, Nome: Teclado, Preço: 199.99
```

---

### Diferenças entre XML e JSON

- **Leveza**: JSON é mais compacto que XML e geralmente preferido em APIs modernas devido à sua simplicidade.
- **Estrutura**: XML é mais formal e suporta schemas e namespaces, tornando-o útil para sistemas mais complexos ou legados.
- **Legibilidade**: JSON tende a ser mais legível e fácil de manipular em linguagens de programação modernas.

---
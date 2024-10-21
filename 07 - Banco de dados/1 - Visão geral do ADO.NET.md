### Visão Geral do ADO.NET

**ADO.NET** (ActiveX Data Objects .NET) é a tecnologia da Microsoft destinada a facilitar o acesso e manipulação de dados de diferentes fontes de dados, como bancos de dados relacionais, serviços web e fontes de dados XML. É parte integrante do framework .NET e oferece um conjunto de classes que permitem que os desenvolvedores construam aplicações que interajam com dados de maneira eficiente e segura.

### O que é o ADO.NET?

ADO.NET é um conjunto de APIs que possibilita a comunicação entre uma aplicação e uma fonte de dados. Ele fornece suporte para operações como conexão com o banco de dados, execução de comandos, recuperação e manipulação de dados. O ADO.NET lida tanto com o acesso a dados conectados (através de conexões abertas para ler/escrever diretamente em um banco de dados) quanto com o acesso a dados desconectados (usando conjuntos de dados em memória).

#### Principais Características:
- **Orientado a Dados**: Projetado para permitir que aplicações .NET interajam com dados em várias formas, especialmente bancos de dados relacionais como SQL Server, Oracle, MySQL, entre outros.
- **Desconectado**: Um dos principais paradigmas do ADO.NET é o uso de datasets, que permitem que os dados sejam acessados e manipulados localmente, sem uma conexão constante com a fonte de dados.
- **Rápido e Eficiente**: Permite acessar dados de maneira otimizada e gerenciar conexões e transações com eficiência.
- **Segurança**: ADO.NET tem suporte para segurança de conexão, utilizando autenticação integrada, criptografia de conexões e outras funcionalidades que aumentam a segurança no acesso a dados.

### Componentes Principais do ADO.NET

ADO.NET é constituído de vários componentes, mas os principais são:

#### 1. **Connection**
O componente `Connection` permite estabelecer uma conexão com uma fonte de dados, como um banco de dados SQL Server ou Oracle. Ele especifica como conectar a aplicação à base de dados, utilizando parâmetros como servidor, nome do banco de dados, credenciais e outras propriedades.

Exemplo de uso:

```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        string connectionString = "Data Source=servidor;Initial Catalog=meuBancoDeDados;Integrated Security=True";
        
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
            Console.WriteLine("Conexão aberta com sucesso.");
        }
    }
}
```

Neste exemplo, estamos usando a classe `SqlConnection` para abrir uma conexão com um banco de dados SQL Server. A string de conexão contém todas as informações necessárias para se conectar ao banco.

#### 2. **Command**
O componente `Command` é usado para executar comandos SQL ou armazenados no banco de dados. Ele pode ser usado para executar consultas SELECT, comandos INSERT, UPDATE, DELETE ou procedimentos armazenados.

Exemplo de uso:

```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        string connectionString = "Data Source=servidor;Initial Catalog=meuBancoDeDados;Integrated Security=True";
        
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
            string query = "SELECT COUNT(*) FROM Produtos";

            using (SqlCommand command = new SqlCommand(query, connection))
            {
                int count = (int)command.ExecuteScalar();
                Console.WriteLine($"Total de produtos: {count}");
            }
        }
    }
}
```

Aqui, usamos o método `ExecuteScalar` para executar uma consulta que retorna um único valor, no caso, a contagem de produtos.

#### 3. **DataReader**
O `DataReader` é uma maneira rápida e eficiente de ler dados retornados por uma consulta SQL. Ele funciona de maneira **forward-only**, ou seja, os dados são lidos uma vez e não podem ser acessados novamente após avançar para a próxima linha.

Exemplo de uso:

```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        string connectionString = "Data Source=servidor;Initial Catalog=meuBancoDeDados;Integrated Security=True";
        
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
            string query = "SELECT Id, Nome FROM Produtos";

            using (SqlCommand command = new SqlCommand(query, connection))
            {
                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        Console.WriteLine($"ID: {reader["Id"]}, Nome: {reader["Nome"]}");
                    }
                }
            }
        }
    }
}
```

Neste exemplo, o `SqlDataReader` lê linha por linha os resultados da consulta, permitindo o acesso aos valores retornados.

#### 4. **DataAdapter**
O `DataAdapter` age como um "ponte" entre a fonte de dados e o `DataSet`. Ele permite que dados sejam lidos da fonte de dados e preencham um `DataSet`, além de facilitar a aplicação de mudanças do `DataSet` de volta à base de dados.

Exemplo de uso com `DataAdapter` e `DataSet`:

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        string connectionString = "Data Source=servidor;Initial Catalog=meuBancoDeDados;Integrated Security=True";
        string query = "SELECT * FROM Produtos";

        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            SqlDataAdapter adapter = new SqlDataAdapter(query, connection);
            DataSet dataset = new DataSet();

            adapter.Fill(dataset, "Produtos");

            foreach (DataRow row in dataset.Tables["Produtos"].Rows)
            {
                Console.WriteLine($"ID: {row["Id"]}, Nome: {row["Nome"]}, Preço: {row["Preco"]}");
            }
        }
    }
}
```

No exemplo acima, o `DataAdapter` preenche um `DataSet` com os dados retornados pela consulta SQL, e então usamos o `DataSet` para iterar pelos dados desconectados da fonte.

#### 5. **DataSet**
O `DataSet` é um objeto desconectado que armazena dados em memória. Ele pode conter múltiplas tabelas (no formato de `DataTable`), permitindo manipulação de dados localmente sem necessidade de uma conexão contínua com o banco.

Exemplo:

```csharp
using System;
using System.Data;

class Program
{
    static void Main()
    {
        DataSet dataSet = new DataSet("Loja");

        DataTable produtos = new DataTable("Produtos");
        produtos.Columns.Add("Id", typeof(int));
        produtos.Columns.Add("Nome", typeof(string));
        produtos.Columns.Add("Preco", typeof(decimal));

        produtos.Rows.Add(1, "Teclado", 199.99m);
        produtos.Rows.Add(2, "Mouse", 99.99m);

        dataSet.Tables.Add(produtos);

        foreach (DataRow row in dataSet.Tables["Produtos"].Rows)
        {
            Console.WriteLine($"ID: {row["Id"]}, Nome: {row["Nome"]}, Preço: {row["Preco"]}");
        }
    }
}
```

Aqui, criamos um `DataSet` e preenchemos uma `DataTable` localmente com dados, que então são manipulados diretamente em memória.

### Cenários de Uso do ADO.NET

#### Conexões Conectadas vs Desconectadas
- **Conexões Conectadas**: Utilizam `Command` e `DataReader` para acessar dados diretamente de uma fonte, com uma conexão contínua. Isso é útil quando você precisa de operações rápidas e com pouca memória, como leitura de dados de forma sequencial.
- **Conexões Desconectadas**: Utilizam `DataAdapter` e `DataSet` para permitir o trabalho com dados em memória, sem manter uma conexão ativa com o banco de dados. São úteis em cenários onde as operações são longas ou quando é necessário realizar várias operações com os dados antes de atualizá-los na fonte.

### Transações em ADO.NET
Para garantir a integridade dos dados, o ADO.NET suporta transações, permitindo que uma série de operações sejam tratadas como uma unidade atômica.

Exemplo de uso de transações:

```csharp
using System;
using System.Data.SqlClient;

class Program
{
    static void Main()
    {
        string connectionString = "Data Source=servidor;Initial Catalog=meuBancoDeDados;Integrated Security=True";

        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
            SqlTransaction transaction = connection.BeginTransaction();

            try
            {
                SqlCommand command = connection.CreateCommand();
                command.Transaction = transaction;

                // Operações de inserção
                command.CommandText = "INSERT INTO Produtos (Nome, Preco) VALUES ('Teclado', 199.99)";
                command.ExecuteNonQuery();

                command.CommandText = "INSERT INTO Produtos (Nome, Preco) VALUES ('Mouse', 99.99)";
                command.ExecuteNonQuery();

                // Confirmar a transação
                transaction.Commit();
                Console.WriteLine("Transação confirmada.");
            }
            catch (Exception ex)
            {
                // Reverter a transação em caso de erro
                transaction.Rollback();
                Console.WriteLine($"Erro: {ex.Message}. Transação revertida.");
            }
        }
    }
}
```

### Conclusão

O ADO.NET
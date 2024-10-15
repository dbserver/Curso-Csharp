### Logs em C#: Introdução e Boas Práticas

O uso de **logs** em aplicações C# é uma prática essencial para monitorar a execução do software, identificar erros e manter um histórico das atividades do sistema. Logs ajudam a rastrear o comportamento da aplicação durante o desenvolvimento, depuração e produção.

#### 1. **O que são Logs?**
Logs são mensagens gravadas durante a execução de um programa, que podem incluir informações como:
- Eventos ocorridos na aplicação (ex: inicialização, execução de tarefas, finalização).
- Erros e exceções lançadas.
- Operações de banco de dados ou API.
- Mensagens de debug e monitoramento.

#### 2. **Níveis de Logs**
Os logs geralmente são categorizados por níveis de severidade, o que ajuda a classificar a importância de cada mensagem:
- **Trace**: Mensagens detalhadas e de baixo nível.
- **Debug**: Informações úteis para depurar a aplicação.
- **Information**: Eventos informativos, como a conclusão de uma operação com sucesso.
- **Warning**: Mensagens de alerta, que indicam possíveis problemas, mas que não impediram a execução.
- **Error**: Indicativo de erros que afetam a funcionalidade, mas não derrubam o sistema.
- **Critical**: Erros graves que podem resultar na falha total da aplicação.

#### 3. **Bibliotecas de Logging**
Para realizar logs de forma eficaz em C#, existem bibliotecas e frameworks que facilitam o processo, como:
- **Serilog**: Fácil de usar, configurável e com suporte a vários "sinks" (destinos para os logs, como arquivos, console, banco de dados).
- **NLog**: Popular e flexível, com suporte para muitas configurações.
- **Log4Net**: Um dos mais antigos, usado em muitos sistemas legados.

#### 4. **Configurando Logs com Serilog**

Aqui está um exemplo de como configurar e usar o **Serilog** em uma aplicação .NET.

##### Instalação
Para começar, adicione o pacote **Serilog** ao seu projeto. No **NuGet Package Manager**, execute o seguinte comando:

```bash
Install-Package Serilog.AspNetCore
```

##### Configuração
Configure o Serilog no arquivo `Program.cs` para capturar logs globais.

```csharp
using Serilog;

public class Program
{
    public static void Main(string[] args)
    {
        // Configura o Serilog
        Log.Logger = new LoggerConfiguration()
            .MinimumLevel.Debug() // Define o nível mínimo de logs
            .WriteTo.Console() // Logs no console
            .WriteTo.File("logs/log.txt", rollingInterval: RollingInterval.Day) // Logs em arquivo
            .CreateLogger();

        try
        {
            Log.Information("Inicializando a aplicação...");
            CreateHostBuilder(args).Build().Run();
        }
        catch (Exception ex)
        {
            Log.Fatal(ex, "Erro crítico durante a inicialização");
        }
        finally
        {
            Log.CloseAndFlush(); // Encerra o logger
        }
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .UseSerilog() // Substitui o sistema de logs padrão pelo Serilog
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

#### 5. **Exemplo de Logs em Ação**

Vamos criar um exemplo simples de uma classe que registra logs para operações bancárias usando a entidade **Extrato**.

```csharp
public class ExtratoService
{
    private readonly ILogger<ExtratoService> _logger;

    public ExtratoService(ILogger<ExtratoService> logger)
    {
        _logger = logger;
    }

    public void AdicionarRegistro(Registro registro)
    {
        _logger.LogInformation("Iniciando a adição de um novo registro. Conta: {Conta}", registro.ExtratoId);
        
        try
        {
            if (registro.Valor < 0)
            {
                _logger.LogWarning("Tentativa de adicionar um valor negativo. Registro: {RegistroId}", registro.Id);
                throw new ArgumentException("O valor do registro não pode ser negativo");
            }

            // Simulação da adição do registro (persistência)
            _logger.LogInformation("Registro {RegistroId} adicionado com sucesso ao extrato {ExtratoId}", registro.Id, registro.ExtratoId);
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Erro ao adicionar registro {RegistroId}", registro.Id);
            throw;
        }
    }
}
```

Neste exemplo:
- Logs de **Information** são usados para registrar eventos comuns, como o início da operação de adição de um registro e a confirmação de sucesso.
- Logs de **Warning** são usados para indicar uma possível anomalia (um valor negativo no registro).
- Logs de **Error** capturam exceções e fornecem detalhes sobre o que aconteceu quando a operação falha.

#### 6. **Destino dos Logs (Sinks)**
O Serilog permite enviar os logs para vários destinos, incluindo:
- **Console**: Ótimo para desenvolvimento e depuração.
- **Arquivo**: Logs armazenados localmente para análise posterior.
- **ElasticSearch**: Para monitoramento e análise em sistemas distribuídos.
- **Seq**: Um sistema de logs estruturados para análise avançada.
- **Banco de Dados**: Armazenamento de logs em um banco relacional, como SQL Server.

##### Exemplo de configuração com arquivo e console:

```csharp
Log.Logger = new LoggerConfiguration()
    .MinimumLevel.Debug()
    .WriteTo.Console()
    .WriteTo.File("logs/log.txt", rollingInterval: RollingInterval.Day)
    .CreateLogger();
```

#### 7. **Boas Práticas para Uso de Logs**
- **Evitar logging excessivo**: Gravar muitos logs pode dificultar a leitura e aumentar o uso de recursos.
- **Incluir informações úteis**: Inclua identificadores como ID do usuário, ID da transação, etc., para rastrear facilmente.
- **Proteger informações sensíveis**: Não registre dados confidenciais diretamente nos logs, como senhas ou informações pessoais.
- **Use o nível correto de log**: Cada mensagem de log deve ser categorizada adequadamente para facilitar a análise posterior (ex: use `Error` apenas para erros reais).
- **Logs estruturados**: Sempre que possível, use logs estruturados (como os fornecidos pelo Serilog) para melhor análise em ferramentas como Kibana ou Grafana.
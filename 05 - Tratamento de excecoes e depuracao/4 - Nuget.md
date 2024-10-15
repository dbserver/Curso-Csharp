### O que é NuGet?

**NuGet** é o gerenciador de pacotes padrão para o ecossistema .NET, utilizado para compartilhar, instalar e gerenciar bibliotecas de código. Ele facilita o desenvolvimento, permitindo que desenvolvedores reutilizem pacotes de terceiros ou distribuam seus próprios pacotes.

Um **pacote NuGet** é um arquivo `.nupkg`, que contém código compilado (bibliotecas), arquivos de dependências e metadados. Ele é armazenado em repositórios como **NuGet.org** ou em repositórios privados, e pode ser facilmente adicionado a projetos .NET.

### Por que usar o NuGet?

- **Reutilização de código**: Permite o uso de bibliotecas já prontas para evitar a "reinvenção da roda".
- **Gerenciamento de dependências**: Facilita o controle de versões de bibliotecas externas.
- **Facilidade de instalação**: Um simples comando ou clique baixa e configura pacotes com todas as dependências necessárias.

### Como instalar e usar pacotes NuGet no .NET?

#### 1. **Instalação de um pacote via CLI**
Para adicionar um pacote NuGet a um projeto .NET, você pode usar a interface de linha de comando do **dotnet**. Por exemplo, para adicionar o pacote **Newtonsoft.Json**, basta rodar o seguinte comando:

```bash
dotnet add package Newtonsoft.Json
```

Isso irá:
- Adicionar o pacote ao seu projeto.
- Atualizar o arquivo `csproj` com a referência ao pacote.
- Baixar o pacote e suas dependências.

#### 2. **Instalação pelo Visual Studio**
Se estiver usando o **Visual Studio**, você pode adicionar pacotes NuGet pelo Gerenciador de Pacotes NuGet:
1. Clique com o botão direito no seu projeto na solução.
2. Selecione **Manage NuGet Packages** (Gerenciar Pacotes NuGet).
3. Na aba **Browse**, pesquise pelo pacote desejado.
4. Clique em **Install** (Instalar) para adicionar o pacote ao projeto.

#### 3. **Restaurando pacotes**
O NuGet Package Restore restaura todas as dependências de um projeto que estão listadas em um arquivo de projeto ou em um arquivo `packages.config`. Você pode restaurar pacotes manualmente com , `dotnet restore` (Net Core +), `msbuild -t:restore`, ou por meio do Visual Studio. 

**Os comandos dotnet build e dotnet run restauram pacotes automaticamente, e você pode configurar o Visual Studio para restaurar pacotes automaticamente quando ele compila um projeto.**

* [Documentação Nuget](https://learn.microsoft.com/en-us/nuget/consume-packages/package-restore)

### Exemplo de Uso: Adicionando um Pacote

Vamos adicionar e usar o pacote **Newtonsoft.Json** em um projeto para serializar um objeto para JSON.

#### Passo 1: Crie um novo projeto console no visual studio

#### Passo 2: Adicione o pacote `Newtonsoft.Json`

**Tools > NuGet Package Manager > Manage NuGet Packages for Solution > Browse**

![Nuget](../assets/nuget.png)


Atenção as versões do pacote, escolha a versão que seja compativel com o seu projeto. 

![Nuget](../assets/Nuget%20manager.PNG)



#### Passo 3: Use o pacote no código
Abra o arquivo `Program.cs` e modifique o código para:

```csharp
using System;
using Newtonsoft.Json;

public class Pessoa
{
    public string Nome { get; set; }
    public int Idade { get; set; }
}

class Program
{
    static void Main(string[] args)
    {
        Pessoa pessoa = new Pessoa { Nome = "Maria", Idade = 30 };
        
        // Serializa o objeto para JSON usando Newtonsoft.Json
        string json = JsonConvert.SerializeObject(pessoa);
        
        Console.WriteLine(json);
    }
}
```

#### Passo 4: Execute o projeto
```bash
dotnet run
```

Saída esperada:
```json
{"Nome":"Maria","Idade":30}
```
## Interface Segregation e Dependency Inversion (SOLID)

O princípio SOLID é um conjunto de diretrizes para ajudar na criação de software orientado a objetos que seja mais compreensível, flexível e de fácil manutenção. Dois dos princípios fundamentais do SOLID são o **Princípio da Segregação da Interface** e o **Princípio da Inversão de Dependência**. Vamos explorar cada um deles com exemplos em C#.

### 1. Princípio da Segregação da Interface (Interface Segregation Principle - ISP)

O **Princípio da Segregação da Interface** afirma que uma classe não deve ser forçada a implementar interfaces que não usa. Em outras palavras, é melhor ter várias interfaces específicas do que uma única interface geral. Isso evita que uma classe implemente métodos que não são relevantes para ela, promovendo um design mais limpo e modular.

#### Exemplo do ISP

Vamos considerar um sistema de notificação que utiliza um único serviço para enviar diferentes tipos de notificações.

**Exemplo Ruim:**

```csharp
public interface INotificacao
{
    void EnviarEmail(string email);
    void EnviarSMS(string numero);
    void EnviarPush(string mensagem);
}

public class NotificacaoEmail : INotificacao
{
    public void EnviarEmail(string email)
    {
        // Lógica para enviar e-mail
    }

    public void EnviarSMS(string numero)
    {
        throw new NotImplementedException();
    }

    public void EnviarPush(string mensagem)
    {
        throw new NotImplementedException();
    }
}
```

No exemplo acima, a classe `NotificacaoEmail` é forçada a implementar métodos que não são relevantes para ela, como `EnviarSMS` e `EnviarPush`.

**Solução com ISP:**

```csharp
public interface INotificacaoEmail
{
    void EnviarEmail(string email);
}

public interface INotificacaoSMS
{
    void EnviarSMS(string numero);
}

public interface INotificacaoPush
{
    void EnviarPush(string mensagem);
}

public class NotificacaoEmail : INotificacaoEmail
{
    public void EnviarEmail(string email)
    {
        // Lógica para enviar e-mail
    }
}

public class NotificacaoSMS : INotificacaoSMS
{
    public void EnviarSMS(string numero)
    {
        // Lógica para enviar SMS
    }
}

public class NotificacaoPush : INotificacaoPush
{
    public void EnviarPush(string mensagem)
    {
        // Lógica para enviar notificação push
    }
}

public class Notificacao : INotificacaoEmail, INotificacaoSMS, INotificacaoPush
{
    private readonly INotificacaoEmail email;
    private readonly INotificacaoSMS sms;
    private readonly INotificacaoPush push;
    Notificacao(INoticacaoEmail email, INotificacaoSMS sms, INotificacaoPush push)
    {
        this.email = email;
        this.sms = sms;
        this.push = push;
    }

    public void EnviarEmail(string email)
    {
        email.EnviarEmail(email);
    }

    public void EnviarSMS(string numero)
    {
        sms.EnviarSMS(numero);
    }
    
    public void EnviarPush(string mensagem)
    {
        push.EnviarPush(mensagem);
    }
}
```

Agora, cada classe implementa apenas os métodos que realmente utiliza, seguindo o Princípio da Segregação da Interface.

### 2. Princípio da Inversão de Dependência (Dependency Inversion Principle - DIP)

O **Princípio da Inversão de Dependência** estabelece que as classes de alto nível não devem depender de classes de baixo nível, mas sim de abstrações. Isso promove um design mais flexível e menos acoplado, facilitando a manutenção e a evolução do sistema.

#### Exemplo do DIP

Vamos considerar um cenário onde temos uma classe de serviço que depende diretamente de um repositório para realizar operações de dados.

**Exemplo Ruim:**

```csharp
public class RepositorioProduto
{
    public void AdicionarProduto(Produto produto)
    {
        // Lógica para adicionar produto ao banco de dados
    }
}

public class ServicoProduto
{
    private RepositorioProduto repositorio;

    public ServicoProduto()
    {
        repositorio = new RepositorioProduto();
    }

    public void CriarProduto(Produto produto)
    {
        repositorio.AdicionarProduto(produto);
    }
}
```

No exemplo acima, a classe `ServicoProduto` depende diretamente da implementação do `RepositorioProduto`, o que a torna rígida e difícil de testar.

**Solução com DIP:**

```csharp
public interface IRepositorioProduto
{
    void AdicionarProduto(Produto produto);
}

public class RepositorioProduto : IRepositorioProduto
{
    public void AdicionarProduto(Produto produto)
    {
        // Lógica para adicionar produto ao banco de dados
    }
}

public class ServicoProduto
{
    private readonly IRepositorioProduto repositorio;

    public ServicoProduto(IRepositorioProduto repositorio)
    {
        this.repositorio = repositorio;
    }

    public void CriarProduto(Produto produto)
    {
        repositorio.AdicionarProduto(produto);
    }
}
```

Agora, a classe `ServicoProduto` depende de uma abstração (`IRepositorioProduto`), em vez de depender de uma implementação concreta. Isso facilita a substituição do repositório por uma implementação diferente (por exemplo, um repositório em memória para testes) e torna a classe mais fácil de testar.

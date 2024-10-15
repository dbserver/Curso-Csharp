Aqui estão as soluções corrigidas dos exercícios envolvendo exceções personalizadas com base nas classes `TipoRegistro`, `TipoEntrada`, `TipoSaida`, `Registro`, `Transacao`, `RegistroEntrada`, `RegistroSaida`, e `Extrato`:

---

### Exercício 1: Validação de TipoRegistro Inválido

**Solução**:

```csharp
using System;

public class TipoRegistroInvalidoException : Exception
{
    public TipoRegistroInvalidoException() 
        : base("Tipo de registro inválido. Deve ser 'Entrada' ou 'Saida'.") { }
}

public class TipoRegistro
{
    public string Tipo { get; set; }

    public TipoRegistro(string tipo)
    {
        if (tipo != "Entrada" && tipo != "Saida")
        {
            throw new TipoRegistroInvalidoException();
        }
        Tipo = tipo;
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            TipoRegistro registro = new TipoRegistro("Desconhecido");
        }
        catch (TipoRegistroInvalidoException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

### Explicação:
- Uma exceção personalizada `TipoRegistroInvalidoException` é lançada se o tipo de registro não for `Entrada` ou `Saida`.
- A exceção é tratada no bloco `try-catch`.

---

### Exercício 2: Registro Sem Extrato Associado

**Solução**:

```csharp
using System;

public class RegistroSemExtratoException : Exception
{
    public RegistroSemExtratoException()
        : base("Não é possível adicionar um registro sem um extrato associado.") { }
}

public class Extrato
{
    public int ID { get; set; }
}

public class Registro
{
    public int ExtratoID { get; set; }

    public Registro(int extratoID)
    {
        if (extratoID == 0)
        {
            throw new RegistroSemExtratoException();
        }
        ExtratoID = extratoID;
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            Registro registro = new Registro(0);
        }
        catch (RegistroSemExtratoException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

### Explicação:
- Uma exceção personalizada `RegistroSemExtratoException` é lançada se o `ExtratoID` for nulo ou zero.
- O `try-catch` captura e exibe a mensagem da exceção.

---

### Exercício 3: Exceção de Transação Não Permitida

**Solução**:

```csharp
using System;

public class TransacaoNaoPermitidaException : Exception
{
    public TransacaoNaoPermitidaException(decimal saldo, decimal valor)
        : base($"Transação não permitida. Valor da transação ({valor}) excede o saldo disponível ({saldo}).") { }
}

public class Extrato
{
    public decimal Saldo { get; set; }

    public Extrato(decimal saldo)
    {
        Saldo = saldo;
    }
}

public class RegistroSaida
{
    public decimal Valor { get; set; }

    public void ExecutarTransacao(Extrato extrato)
    {
        if (Valor > extrato.Saldo)
        {
            throw new TransacaoNaoPermitidaException(extrato.Saldo, Valor);
        }
        extrato.Saldo -= Valor;
        Console.WriteLine("Transação de saída realizada com sucesso.");
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            Extrato extrato = new Extrato(100);
            RegistroSaida saida = new RegistroSaida { Valor = 150 };
            saida.ExecutarTransacao(extrato);
        }
        catch (TransacaoNaoPermitidaException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

### Explicação:
- A exceção `TransacaoNaoPermitidaException` é lançada quando o valor da transação excede o saldo do extrato.
- A exceção é tratada no bloco `try-catch`, com uma mensagem informando sobre o erro.

---

### Exercício 4: Valor de Registro Inválido

**Solução**:

```csharp
using System;

public class ValorRegistroInvalidoException : Exception
{
    public ValorRegistroInvalidoException()
        : base("O valor do registro não pode ser negativo.") { }
}

public class Registro
{
    public decimal Valor { get; set; }

    public Registro(decimal valor)
    {
        if (valor < 0)
        {
            throw new ValorRegistroInvalidoException();
        }
        Valor = valor;
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            Registro registro = new Registro(-10);
        }
        catch (ValorRegistroInvalidoException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

### Explicação:
- Uma exceção personalizada `ValorRegistroInvalidoException` é lançada quando o valor de um registro é negativo.
- A exceção é tratada com `try-catch`, informando o erro ao usuário.

---

### Exercício 5: Exceção de Tipos Incompatíveis em Transações

**Solução**:

```csharp
using System;

public class TiposIncompativeisException : Exception
{
    public TiposIncompativeisException(string operacao, string tipo)
        : base($"Operação '{operacao}' não permitida com tipo '{tipo}'.") { }
}

public class TipoRegistro
{
    public string Tipo { get; set; }

    public TipoRegistro(string tipo)
    {
        Tipo = tipo;
    }
}

public class RegistroEntrada
{
    public decimal Valor { get; set; }
    public TipoRegistro Tipo { get; set; }

    public void ProcessarTransacao(string operacao)
    {
        if (Tipo.Tipo != "Entrada" && operacao == "Adicionar")
        {
            throw new TiposIncompativeisException(operacao, Tipo.Tipo);
        }
        Console.WriteLine("Transação de entrada processada com sucesso.");
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            TipoRegistro tipoSaida = new TipoRegistro("Saida");
            RegistroEntrada entrada = new RegistroEntrada { Valor = 100, Tipo = tipoSaida };
            entrada.ProcessarTransacao("Adicionar");
        }
        catch (TiposIncompativeisException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

### Explicação:
- A exceção `TiposIncompativeisException` é lançada quando se tenta realizar uma operação de entrada com um `TipoRegistro` de saída.
- A exceção é capturada e tratada no bloco `try-catch`, com uma mensagem clara para o usuário.

---
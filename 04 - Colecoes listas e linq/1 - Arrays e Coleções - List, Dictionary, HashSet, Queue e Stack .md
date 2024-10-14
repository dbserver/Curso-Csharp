## Arrays e Coleções em C#

Em C#, arrays e coleções são estruturas de dados fundamentais utilizadas para armazenar grupos de elementos. Enquanto os arrays têm um tamanho fixo, as coleções oferecem flexibilidade e funcionalidades adicionais. Neste tópico, exploraremos algumas das coleções mais utilizadas em C#: **List**, **Dictionary**, **HashSet**, **Queue** e **Stack**.

### 1. Arrays

Os arrays são a forma mais simples de armazenar coleções de dados. Eles têm um tamanho fixo e são usados quando você sabe quantos elementos deseja armazenar.

#### Exemplo de Array

```csharp
int[] numeros = new int[5]; // Array de inteiros com tamanho 5
numeros[0] = 10;
numeros[1] = 20;
numeros[2] = 30;
numeros[3] = 40;
numeros[4] = 50;

foreach (int numero in numeros)
{
    Console.WriteLine(numero);
}
```

### 2. List<T>

`List<T>` é uma coleção que pode conter um número variável de elementos. É uma implementação da interface `IList<T>` e oferece funcionalidades como adição, remoção e busca de elementos.

#### Exemplo de List<T>

```csharp
using System.Collections.Generic;

List<string> frutas = new List<string>();
frutas.Add("Maçã");
frutas.Add("Banana");
frutas.Add("Laranja");

// Remover um elemento
frutas.Remove("Banana");

// Iterar sobre a lista
foreach (string fruta in frutas)
{
    Console.WriteLine(fruta);
}
```

### 3. Dictionary<TKey, TValue>

`Dictionary<TKey, TValue>` é uma coleção que armazena pares de chave-valor. É útil quando você precisa associar valores a chaves únicas.

#### Exemplo de Dictionary<TKey, TValue>

```csharp
using System.Collections.Generic;

Dictionary<int, string> pessoas = new Dictionary<int, string>();
pessoas.Add(1, "Alice");
pessoas.Add(2, "Bob");
pessoas.Add(3, "Carol");

// Acessar um valor usando a chave
Console.WriteLine(pessoas[2]); // Saída: Bob

// Iterar sobre o dicionário
foreach (KeyValuePair<int, string> pessoa in pessoas)
{
    Console.WriteLine($"ID: {pessoa.Key}, Nome: {pessoa.Value}");
}
```

### 4. HashSet<T>

`HashSet<T>` é uma coleção que armazena elementos únicos e não permite duplicatas. É útil quando você precisa garantir que todos os elementos sejam distintos.

#### Exemplo de HashSet<T>

```csharp
using System.Collections.Generic;

HashSet<string> nomes = new HashSet<string>();
nomes.Add("Alice");
nomes.Add("Bob");
nomes.Add("Alice"); // Não será adicionado, pois é duplicado

// Iterar sobre o HashSet
foreach (string nome in nomes)
{
    Console.WriteLine(nome);
}
```

### 5. Queue<T>

`Queue<T>` é uma coleção que segue o princípio FIFO (First In, First Out). Os elementos são adicionados no final e removidos do início.

#### Exemplo de Queue<T>

```csharp
using System.Collections.Generic;

Queue<string> fila = new Queue<string>();
fila.Enqueue("Cliente 1");
fila.Enqueue("Cliente 2");
fila.Enqueue("Cliente 3");

// Remover o primeiro elemento da fila
Console.WriteLine(fila.Dequeue()); // Saída: Cliente 1

// Iterar sobre a fila
foreach (string cliente in fila)
{
    Console.WriteLine(cliente);
}
```

### 6. Stack<T>

`Stack<T>` é uma coleção que segue o princípio LIFO (Last In, First Out). Os elementos são adicionados e removidos do topo da pilha.

#### Exemplo de Stack<T>

```csharp
using System.Collections.Generic;

Stack<string> pilha = new Stack<string>();
pilha.Push("Item 1");
pilha.Push("Item 2");
pilha.Push("Item 3");

// Remover o último elemento da pilha
Console.WriteLine(pilha.Pop()); // Saída: Item 3

// Iterar sobre a pilha
foreach (string item in pilha)
{
    Console.WriteLine(item);
}
```

### Comparação das Estruturas de Dados

| Estrutura de Dados | Tipo de Acesso | Permite Duplicatas | Ordenado | Notas |
|--------------------|----------------|---------------------|----------|-------|
| Array              | Índice         | Sim                 | Sim      | Tamanho fixo |
| List<T>            | Índice         | Sim                 | Sim      | Tamanho dinâmico |
| Dictionary<TKey, TValue> | Chave       | Não (chaves únicas) | Não      | Par chave-valor |
| HashSet<T>         | Não (conjunto) | Não                  | Não      | Elementos únicos |
| Queue<T>           | FIFO           | Sim                 | Não      | Adiciona no final, remove do início |
| Stack<T>           | LIFO           | Sim                 | Não      | Adiciona e remove do topo |


### Exercícios

1. **Criar e manipular um array**: Crie um array de inteiros com 10 elementos, inicialize-o com valores aleatórios e imprima a soma dos elementos.

2. **Usar List<T>**: Crie uma lista de estudantes. Adicione, remova e imprima os nomes dos estudantes da lista. 

3. **Implementar Dictionary<TKey, TValue>**: Crie um dicionário que armazene a idade de pessoas. Adicione pelo menos cinco pessoas e suas idades e imprima as idades.

4. **Trabalhar com HashSet<T>**: Crie um `HashSet` que armazene os nomes de frutas. Tente adicionar algumas frutas duplicadas e imprima a coleção final.

5. **Gerenciar uma fila com Queue<T>**: Implemente uma fila de atendimento ao cliente. Adicione três clientes e imprima qual cliente está sendo atendido.

6. **Gerenciar uma pilha com Stack<T>**: Crie uma pilha de livros e implemente operações para adicionar e remover livros, imprimindo o título do último livro removido.

Esses exercícios ajudarão a fixar o conhecimento sobre arrays e coleções em C#.
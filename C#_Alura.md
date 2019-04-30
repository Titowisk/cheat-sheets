# Cursos de C# da Alura

## História e Ecossistema .NET:

A máquina virtual que fica acima do sistema operacional é a CLR (Common Language Runtime), nesse mundo C#. 
Na camada logo acima, teremos a biblioteca, chamada de .NET Framework, e subindo uma mais, teremos a Aplicação .NET. 
Com as alterações, ficamos com a seguinte ordenação das camadas. 

- Linguagens: C# | VB | F# | ...
- Aplicação .NET (MSIL)
- .NET Framework (biblioteca MSIL)
- CLR - Common Language Runtime (Máquina Virtual)
- Sistemas Operacionais: Windows | Linux | ...

## Tipos e Conversões

- C# é uma linguagem de tipagem forte (similar ao java)
- double, int, float, char, string...
- A conversão é implícita quando se faz de um tipo menor para um maior:
Ex: int para double

* **Aspas simples '' são para caracteres, aspas duplas "" são para textos**
- Tipo string permite multilinhas se colocar @"";
Ex:
```
string lista_cursos2 = 
@"
- .Net
- Java
- Python
";
```
- Tipo string possui uma sinaxe para inserção de variáveis no texto **($"... {} ...")**:
```
int idade = 20;
string frase = $"Minha idade é {idade}";
```
- É possível fazer conversões com casting:
```
double d = 2;
int i = (int) d;
```
- É possível fazer conversões usando `as`, mas somente para alguns tipos:
https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/as

- É possível utilizar uma variável que irá ter o tipo do valor que está sendo atribuida a ela:
```
// antes
ContaCorrente conta = new ContaCorrente(344,56456556);
GerenciadorBonificacao gerenciador = new GerenciadorBonificacao();
List<GerenciadorBonificacao> gerenciadores = new List<GerenciadorBonificacao>();
string frase = "Olá Mundo!";
int idade = 35;

// depois (var)
var conta = new ContaCorrente(344,56456556);
var gerenciador = new GerenciadorBonificacao();
var gerenciadores = new List<GerenciadorBonificacao>();
var frase = "Olá Mundo!";
var idade = 35;
```

### String
Métodos, propriedades...
https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netframework-4.8

## If else
Mesmo do Java if () {}
Mas pode ser usado assim:
```
Se a condição é verdade, executa a primeira expressão após o if
if (condition)
  expression
```
### Switch
```
switch (variavelASerTestada) {
    case opção1:
            comando(s) caso a opção 1 tenha sido escolhida
            break;
    case opção2:
            comando(s) caso a opção 2 tenha sido escolhida
            break;
    case opção3:
            comando(s) caso a opção 3 tenha sido escolhida
            break;
    default:
            comando(s) caso nenhuma das opções anteriores tenha sido escolhida
}
```
## Classes

```
public class ContaCorrente
{
    public string titular;
    public int agencia;
    public int numero;
    public double saldo;
}
```
Esses atributos já possuem valores default no CSharp. 
Tipo int por exemplo é 0, assim como double.
Tipo boolean é false

### Métodos:
```
public class ContaCorrente
{
    public string titular;
    public int agencia;
    public int numero;
    public double saldo;


    public bool Sacar(double valor)
    {
        if(this.saldo < valor)
        {
            return false;
        }
        else
        {
            this.saldo -= valor;
            return true;
        }
    }
}
```
- Argumentos Opcionais:
```
// Definição
meuMetodo(int numero = 5, double dinheiro = 100.5)
{
  // código
}

// chamada

meuMetodo() // o compilador vai assumir os valores fornecidos na definição
```

- Argumentos Nomeados:

```
meuMetodo(dinheiro: 250.56) // troca o valor somente do parâmetro "dinheiro"
```
- **Funções Lambda**:
Funciona de forma similar a `arrow functions` do javascript
```
var contasOrdenadas = contas.OrderBy(conta =>
    {
        if(conta == null)
        {
            return int.MaxValue;
        }
        return conta.Numero;
    });
```

### Namespaces:
Serve para definir um conjunto de classes sendo utilizadas:
Ex: Usar a classe Cliente dentro da classe ContaCorrente
```
// Projeto: 05-ByteBank
// arquivo-classe: Cliente.cs
namespace _05_ByteBank
{
    public class Cliente
    {
    }
}
```

```
// Projeto: 05-ByteBank
// arquivo-classe: ContaCorrente.cs

using _05_ByteBank;

public class ContaCorrente
{
    public Cliente titular;
    public int agencia;
    public int numero;
    public double saldo;
...
}
```
Se a classe for criada dentro de uma pasta, o namespace deve incorporar o nome dessa pasta tb

### Getters and Setters:
No C# pode-se contruir-los manualente, ou utilizando atalhos:
```
private string _name
// getter
public string getName () {return name}
// ou
get {return _name}

// setter
public void setName (name) {return _name = name}
// ou
set 
{
  _name = value; // value é uma palavra reservada
}

// getter and setter
private string Name {get; set;} // primeira letra maiúscula
```
* _<property_name> é uma convenção para propriedades/atributos privados da classe.
* digitar prop me dá um snippet para criação de propriedades
* Atributo **readOnly**:
A construção abaixo torna o atributo Numero readOnly, isso significa que ele só pode ser 'setado' uma única vez
no construtor.
```
// Classe ContaCorrente
public int Numero { get }
```
Equivalente a:
```
private readonly int _numero;
public int Numero 
  {
      get
      {
          return _numero;
      }
  }
```

### Contructors
```
public ContaCorrente(int agencia, int numero)
{
    // força a atribuição de valores às propriedades determinadas.
    Agencia = agencia;
    Numero = numero;
}
```

Para usar construtores com parâmetros ao longo de classes com herança:
```
// classe pai Funcionario
public Funcionario(string cpf)
{
    Console.WriteLine("Criando FUNCIONARIO");

    CPF = cpf;

    TotalDeFuncionarios ++;
}

// classe filha Diretor
public Diretor(string cpf) : base(cpf) 
{
...
}
```
Para usar indexadores no constructor (myClassItem[index]):
https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/indexers/using-indexers

### Static Methods and Properties:
São acessadas pelo nome da classe, inclusive dentro de seu próprio contexto.
```
ContaCorrente.TotalDeContasCriadas;
```
Propriedades podem ser estáticas e seus getters and setters privados
```
// É permitido pegar o valor de TotalDeContasCriadas fora do contexto da classe
// mas não é permitido atribuir valor a ela fora do contexto da classe
public static int TotalDeContasCriadas { get; private set; }
```
**Obs:** métodos e variáveis estáticos para tipos genéricos:  uma variável estática declarada em uma classe genérica é compartilhada entre todas as classes **de mesmo tipo genérico**. Mas, não é compartilhada entre classes de tipo genérico diferente.

### Herança:
A notação ```classe filha : classe pai``` indica a herança.
A palavra reservada ```base``` permite acessar recursos da classe pai, dentro do contexto da classe filha.

EX:
```
public class Diretor : Funcionario
    {
        public override double GetBonificacao()
        {
            return Salario + base.GetBonificacao();
        }
    }
```

### Overriding and Overloading:
O overloading é apenas duas funções com nomes iguais mas parâmetros diferentes.

Mas no caso do overriding, o método da classe pai precisa receber a palavra reservada
```virtual``` e o método da classe filha precisa receber a palavra reservada ```override```.
Ex:
```
// classe pai
public virtual double GetBonificacao()
{
    return Salario * 0.10;
}

// classe filha
public override double GetBonificacao()
{
    return Salario;
}
```
### protected
Permite tornar um atributo/propriedade/método, exclusivo do contexto de classes pai e filhas.
O "private" torna um atriuto/propriedade/método exclusivo somente para um contexto.
O "protected" permite seu uso a toda hierarquia de heranças de classes.

## 6.Classes Abstratas
Torna uma classe não instânciável, pois ela serve apenas de molde para suas classes filhas.

### Métodos Abstratos:
Força a nível de compilação, que as classes filhas implementem os métodos herdados da classe abstrata pai.

## 7.Herança Multipla:
Herança múltipla não é permitido em C#. No caso são utilizados Interfaces

- Uma classe só pode herdar uma única classe, mas pode herdar diversas interfaces;
- Classes abstratas podem ter implementações (de métodos de uma interface por exemplo);
- Interfaces não podem ter implementações;

## Exceptions:
O c# possui a seguinte sintaxe para capturar/lidar com exceções:
```
try
{
  // some code
}
catch(exception someVar)
{
  // some code
  Console.WriteLine(someVar.Message); // imprime mensagem de erro da exceção
  Console.WriteLine(someVar.StackTrace); // imprime Call Stack do erro da exceção
  throw; // palavra reservada do C# para lançar erro/exceção
}
catch(exception2 someVar)
{
  // some code
  Console.WriteLine(someVar.Message); // imprime mensagem de erro da exceção
  Console.WriteLine(someVar.StackTrace); // imprime Call Stack do erro da exceção
  throw; // palavra reservada do C# para lançar erro/exceção
}
...
```
**Obs:** `throw;` sem parâmetro (throw exception; por exemplo), preserva o `StackTrace` do erro.

### Exceções Customizadas (altera exceções existentes)
Posso criar exceções customizadas, ArgumentException permite a customização de mensagem e do parâmetro utilizado:
```
public ContaCorrente(int agencia, int numero)
    {
        // exceções personalizads com mensagens
        if (agencia <= 0) throw new ArgumentException($"{nameof(agencia)} deve ser maior que 0", nameof(agencia));
        if (numero <= 0) throw new ArgumentException($"{nameof(numero)} deve ser maior que 0", nameof(numero));
        
        Agencia = agencia;
        Numero = numero;

        TotalDeContasCriadas++;
    }
```
**Obs:** `nameof()` retorna o nome de um atributo como string

### Criação de exceções (cria exceções novas):

É possível criar também classes de exceção, basta derivar da classe Exception.
```
namespace ByteBank
{
    public class SaldoInsuficienteException : Exception
    {
        public double Saldo { get; } // readonly
        public double ValorDeSaque { get; } // readonly
        public SaldoInsuficienteException()
        {
        }

        public SaldoInsuficienteException(string message) : base(message)
        {

        }

        public SaldoInsuficienteException(double saldo, double valor) 
            : this($"Tentativa de saque no valor de {valor} com saldo de: {saldo}")
        {
            Saldo = saldo;
            ValorDeSaque = valor;
        }
    }
}
```
### Inner Exceptions:
É possivel criar inner exceptions para gerenciar acessibilidade à informação sensível da aplicação:
Exemplo, pessoa que Saca dinheiro pode ter acesso ao valor de seu saque e ao saldo de sua conta na mensagem de erro,
porém uma outra pessoa que faz a transferência talvez não possa ter esse acesso:

SaldoInsuficienteException: possui um construtor que aceita uma **exceção como argumento**
```
namespace ByteBank
{
    public class OperacaoFinanceiraException : Exception
    {
        public OperacaoFinanceiraException()
        {

        }
        public OperacaoFinanceiraException(string message) : base(message)
        {

        }

        public OperacaoFinanceiraException(string message, Exception innerException) :
            base(message, innerException)
        {

        }
    }
}
```

Sacar:
```
public void Sacar(double valor)
    {
        if (_saldo < valor)
        {
            ContadorSaquesNaoPermitidos++;
            // oferece informação de saldo e valor no erro
            throw new SaldoInsuficienteException(Saldo, valor); 
        }

        _saldo -= valor;
    }
```

Transferir:
```
public void Transferir(double valor, ContaCorrente contaDestino)
    {
        if (valor < 0)
        {
            throw new SaldoInsuficienteException("Não é possível transferir valor negativo");
        }

        try
        {
            Sacar(valor);
        }
        catch (SaldoInsuficienteException ex)
        {
            ContadorTransferenciasNaoPermitidas++;
            // não oferece informação de saldo do erro
            throw new OperacaoFinanceiraException("Operação não pôde ser realizada.", ex);
        }
        contaDestino.Depositar(valor);
    }
```

O programa pode então usar a mensagem da exceção ou da exceção interna:

```
// try block
catch (OperacaoFinanceiraException e)
    {
        Console.WriteLine(e.Message); // OperacaoFinanceiraException
        Console.WriteLine(e.StackTrace); // OperacaoFinanceiraException
        Console.WriteLine("Inner Exception ------------------");
        Console.WriteLine(e.InnerException.Message); // SaldoInsuficienteException
        Console.WriteLine(e.InnerException.StackTrace); // SaldoInsuficienteException
    }
```
### Try/Catch/Finally e Using:
Sintaxe do Try-catch-finally:
```
LeitorDeArquivo leitor = new LeitorDeArquivo("contas.txt");
try
{
    leitor.LerProximaLinha();
    leitor.LerProximaLinha();
    leitor.LerProximaLinha();
}
catch(IOException)
{
    Console.WriteLine("Exceção do tipo IOException capturada e tratada!");
}
finally
{
    leitor.Fechar();
}
```

Syntax Sugar: Using {}
```
using (LeitorDeArquivo leitor = new LeitorDeArquivo("teste.txt"))
    {
        leitor.LerProximaLinha();
    }
```
Para isso, a classe LeitorDeArquivo deve implementar o IDisposable:
```
public class LeitorDeArquivo : IDisposable
{
    // code
    
    public void Dispose()
    {
        Console.WriteLine("Fechando arquivo.");
    }
}
```

## Extensões de classes:
- Como adicionar novas funcionalidades {a classes existentes):
https://docs.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/extension-methods
```
public static class ListaExtensoes
    {
        public static void AdicionaVarios(List<int> listaDeInt, params int[] itens)
        {
            foreach (int item in itens)
            {
                listaDeInt.Add(item);
            }
        }
    }
// chamada
  List<int> idades = new List<int>();
  // código...
  ListaExtensoes.AdicionaVarios(idades, 99, 666, 042);
```
- Usando o `this`, pode-se chamar o método da própria classe criada:
```
public static class ListaExtensoes
    {
        public static void AdicionaVarios(this List<int> listaDeInt, params int[] itens)
        {
            foreach (int item in itens)
            {
                listaDeInt.Add(item);
            }
        }
    }
// chamada
idades.AdicionaVarios(99, 666, 042);
```
- Extensões usando métodos genéricos:
https://docs.microsoft.com/pt-br/dotnet/csharp/programming-guide/generics/generic-methods
```
public static class ListaExtensoes
    {
        public static void AdicionaVarios<T>(this List<T> lista, params T[] itens)
        {
            foreach (T item in itens)
            {
                lista.Add(item);
            }
        }
    }
```
## Interface IComparable e IComparer x OrderBy:
- IComparable serve para implantar um método para definir como ocorre a ordenação
em uma Classe.
```
public int CompareTo(object obj)
    {
        var outraConta = obj as ContaCorrente;

        if (outraConta == null) return 1;

        return Numero.CompareTo(outraConta.Numero);
    }
// chamada:
var contas = new List<ContaCorrente>()
    {
      new ContaCorrente(341, 57480),
      new ContaCorrente(342, 45678),
      new ContaCorrente(340, 48950),
      new ContaCorrente(290, 18950)
    };

    contas.Sort(); // compara pelo Numero
```
- IComparer serve para implantar diferentes formas de ordenação de uma classe utilizando
classes estáticas.
```
class ComparadorContaCorrentePorAgencia : IComparer<ContaCorrente>
    {
        public int Compare(ContaCorrente x, ContaCorrente y)
        {
            if (x == null) return 1;
            if (y == null) return 1;

            return x.Agencia.CompareTo(y.Agencia);
        }
    }
// chamada:
var contas = new List<ContaCorrente>()
    {
      new ContaCorrente(341, 57480),
      new ContaCorrente(342, 45678),
      new ContaCorrente(340, 48950),
      new ContaCorrente(290, 18950)
    };

    contas.Sort(new ComparadorContaCorrentePorAgencia()); // compara pela Agencia
```
- OrderBy é a funcionalidade mais adequada para comparações, pois permite que um tipo
seja ordenado por um atributo escolhido na hora usando `funções lambda`:

https://docs.microsoft.com/en-us/dotnet/api/system.linq.iorderedenumerable-1?view=netframework-4.8

## LINQ
Isso aí! Qualquer coleção que implementa a interface IEnumerable pode ser fonte de dados de uma consulta LINQ.

## Dicas:
https://www.caelum.com.br/apostila-csharp-orientacao-objetos/
https://www.caelum.com.br/apostila-csharp-orientacao-objetos/lidando-com-conjuntos/#exerccios
https://www.linqpad.net/

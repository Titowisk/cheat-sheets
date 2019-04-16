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

## Classes Abstratas
Torna uma classe não instânciável, pois ela serve apenas de molde para suas classes filhas

### Métodos Abstratos:
Força a nível de compilação, que as classes filhas implementem os métodos herdados da classe abstrata pai.

## Herança Multipla:
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
}
catch(exception2 someVar)
{
  // some code
  Console.WriteLine(someVar.Message); // imprime mensagem de erro da exceção
  Console.WriteLine(someVar.StackTrace); // imprime Call Stack do erro da exceção
}
...
```

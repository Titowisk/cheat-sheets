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


## Dicas:
https://www.caelum.com.br/apostila-csharp-orientacao-objetos/
https://www.caelum.com.br/apostila-csharp-orientacao-objetos/lidando-com-conjuntos/#exerccios
https://www.linqpad.net/

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
## If loop
Mesmo do Java if () {}
Mas pode ser usado assim:
```
Se a condição é verdade, executa a primeira expressão após o if
if (condition)
  expression
```

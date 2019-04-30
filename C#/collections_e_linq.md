# Coleções em C#

## Arrays: 

`someType[] someName = new someType[n]` n = [0, 1, 2, ..., n-1]
https://docs.microsoft.com/en-us/dotnet/api/system.array?view=netframework-4.8

**Obs: Sintax Sugar**
```
int[] idades = new int[]
    {
        32,42,19,24
    };
    // [32, 42, 19, 24]
```
**Obs:** Passando um array para uma função/método:
https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/params

- List:
https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=netframework-4.8#definition
Exemplos:
```
// Primeira aula da lista que contem a string "trabalhando"
Console.WriteLine("A primeira aula 'Trabalhando' é:" + aulas.First(aula =>  aula.Contains("Trabalhando")));

// Última aula da lista que contém a string "trabalhando"
Console.WriteLine("A última aula 'Trabalhando' é:" + aulas.Last(aula =>  aula.Contains("Trabalhando")));

// O mesmo que o outro, só que retorna uma valor default caso não satisfaça a condição
Console.WriteLine("A primeira aula 'Conclusão' é:" + aulas.FirstOrDefault(aula =>  aula.Contains("Conclusão")));
```
- Array Multidimensional:
```
string[,] resultados = new string[3,3]
        {
                {"Alemanha", "Espanha", "Itália"},
                {"Argentina", "Holanda", "França"},
                {"Holanda", "Alemanha", "Alemanha"},
        };
```
- Jagged Array (Array Denteado ou Serrilhado):
```

string [][] familias = new string [3][]

familias[0] = new string[] {"Fred", "Wilma", "Pedrita"};
familias[1] = new string[] {"Homer", "Marge", "Lisa", "Bart", "Maggie"};
familias[2] = new string[] {"Florinda", "Kiko"}
```

## Listas:

- Lista Ligada (LinkedLists): adequado para grande número de inserções e alterações no meio da lista.

As **desvantagens de uma lista ligada** implicam no acesso a um elemento de forma indexada, o que é impossível, e na busca de elementos em uma lista, causando um processo bastante demorado. Nestes casos, recomenda-se o uso de List<T>.

- Pilha (Stack): Last-in First-out

- Fila (Queue: first-in, first-out

## Dicionário:

- Dictionary: par (chave, valor) onde as chaves são guardadas sem ordem definida e dão acesso aos valores.

- SortedList: par (chave, valor) onde a chave é ordenado segundo uma lista

- SortedDicitonary: par (chave, valor) onde a chave é ordenada através de uma Árvore Binária
Permite inserções/remoções melhor que o SortedList

- HashSet (Conjuntos): valor com hash, onde não há ordem nem valores duplicados.

- SortedSet (Conjuntos ordenados): possui uma árvore binária balanceada para armazenar os valores. Não há hashs.

**Nível: Avançado (copiado da aula ALURA)**
A classe genérica SortedDictionary é uma árvore de busca binária com "comportamento de recuperação de dados" expresso na notação de complexidade O(log n), onde n é o número de elementos no dicionário.
Sob esse aspecto, ela é similar à classe genérica SortedList, e as duas possuem complexidade de recuperação equivalente: O(log n)
Porém, SortedDictionary possui operações de inserção e remoção mais rápidas, porque essas operações em SortedDictionary são O(log n), enquanto as mesmas operações no SortedList possuem complexidade O(n).

**Obs Covariância**: A covariância acontece quando um objeto de menor derivação é atribuido a um objeto de maior derivação (Ex: string para object). Em alguns casos ela pode gerar problemas, em outros não. **De qualquer forma, deve-se evitar!!!!**
```
string[] arrayMeses = new string[]
{
        "Janeiro", "Fevereiro", "Março",
        "Abril", "Maio", "Junho",
        "Julho", "Agosto", "Setembro",
        "Outubro", "Novembro", "Dezembro"
};

object[] arrayObj = arrayMeses; //COVARIÂNCIA! (irá gerar problemas)
```

```
List<string> listaMeses = new List<string>{"jan", "fev","mar"...}
IEnumerable<object> enumObj = listaMeses; //COVARIÂNCIA (não gera problemas)
```
https://docs.microsoft.com/pt-br/dotnet/csharp/programming-guide/concepts/covariance-contravariance/

## LINQ
Isso aí! Qualquer coleção que implementa a interface IEnumerable pode ser fonte de dados de uma consulta LINQ.
https://docs.microsoft.com/pt-br/dotnet/csharp/programming-guide/concepts/linq/standard-query-operators-overview

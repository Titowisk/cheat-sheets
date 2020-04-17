# Conceitos e palavras chaves importantes

## Table Per Hierarchy Inheritance

## Anemic Model
https://martinfowler.com/bliki/AnemicDomainModel.html

## Entity x ValueObjects

## IEnumerable x ICollection x Ilist

- IEnumerable: list of objects that only need to be iterated through
- iCollection: previous plus modification
- IList: previous plus sorting and other stuff

Source: https://stackoverflow.com/questions/10113244/why-use-icollection-and-not-ienumerable-or-listt-on-many-many-one-many-relatio

## Yield
palavra-chave c# que permite criar um iterador a partir de um operador, expressão ou método.
Esse iterador é diferente de uma coleção comum porque ele só sabe retornar o próximo elemento,
ele não conhece a coleção inteira que está iterando. Dessa forma, consome menos memória e as vezes é mais rápido.

Uma disvantagem é com relação ao debug, já que ele não conhece a coleção que está iterando.

https://dev.to/morganw09/benchmarking-the-yield-statement-in-c-2d8g (2019)
https://www.codeproject.com/Articles/1131583/Yield-or-Not-To-Yield (2016)


## ReadOnly x Const
ReadOnly é definido em tempo de execução
Const é definido em tempo de compilação 

https://pt.stackoverflow.com/questions/151721/qual-%C3%A9-a-diferen%C3%A7a-entre-const-e-readonly
http://www.macoratti.net/14/09/c_ctrdst.htm

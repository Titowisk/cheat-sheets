# Conceitos e palavras chaves importantes

## Table Per Hierarchy Inheritance
??????????

## Anemic Model
???????????

Fontes: 
https://martinfowler.com/bliki/AnemicDomainModel.html

## Entity x ValueObjects

## IEnumerable x ICollection x Ilist

- IEnumerable: list of objects that only need to be iterated through
- iCollection: previous plus modification
- IList: previous plus sorting and other stuff

Source: https://stackoverflow.com/questions/10113244/why-use-icollection-and-not-ienumerable-or-listt-on-many-many-one-many-relatio

## Yield and Iterations

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

## CQRS - Command Query Responsability Segregation
De forma básica, é a separação entre commands (ações) que fazem escrita no banco de dados
e queries (consultas) que fazem apenas leitura no banco de dados.

### Mediator and CQRS

É um padrão para abstração de comunicação.
No CQRS, utilizando injeção de dependência, se atrela um Handler a um comando específico.
Usando  o mediador, o comando é enviado ao mediador que irá saber qual handler utilizar naquele caso.

Fontes:
https://www.youtube.com/watch?v=G0yi5PTzhLA André Baltieri
https://balta.io/blog/aspnet-core-cqrs-mediator

### Event Sourcing and CQRS
???

---

## Dependency Injection
Uma forma de aplicar o conceito: "Usar abstrações ao invés de depender de implementações".
No caso do Net Core isso é feito ao iniciar aplicação (Startup.cs). Lá é definido como as abstrações
irão usar implementações definidas. Pode ser através de um singleton (AddScoped) ou não (AddTransient).

Então cada classe que quiser fazer uso da dependência, basta definir a abstração (Interface) correspondente
em seu construtor.

### Explicit Dependencies Principle

Fontes:
https://balta.io/blog/aspnet-core-dependency-injection

## Primitive Obssession
??????

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

Uma desvantagem é com relação ao debug, já que ele não conhece a coleção que está iterando.

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
Dessa forma, quanto mais commands, mais interfaces irão existir. E cada caso irá precisar
de uma injeção de dependência no startup.cs

Usando  o mediador, o comando é enviado ao mediador que irá saber qual handler utilizar naquele caso.

Fontes:
https://www.youtube.com/watch?v=G0yi5PTzhLA André Baltieri
https://balta.io/blog/aspnet-core-cqrs-mediator

### Event Sourcing and CQRS
???


## Dependency Injection
Uma forma de aplicar o conceito: "Usar abstrações ao invés de depender de implementações".
No caso do Net Core isso é feito ao iniciar aplicação (Startup.cs). Lá é definido como as abstrações
irão usar implementações definidas. Pode ser através de um singleton (AddSingleton), Scoped (AddScoped) ou Transient (AddTransient). A diferença entre eles está na fontes.

Então cada classe que quiser fazer uso da dependência, basta definir a abstração (Interface) correspondente
em seu construtor.

### Explicit Dependencies Principle

Fontes:
https://balta.io/blog/aspnet-core-dependency-injection
https://stackoverflow.com/questions/38138100/addtransient-addscoped-and-addsingleton-services-differences

## Primitive Obssession
??????

## WebRequest x HttpClient x WebClient x HttpWebRequest x RestSharp
O mais recomendado para net core é HttpClient
Importante lembrar de utiliza-lo como um elemento stático da classe

```
private static readonly HttpClient _httpClient = new HttpClient();
```

Fontes:
http://www.macoratti.net/16/08/net_web1.htm
https://www.reddit.com/r/csharp/comments/ex80tv/so_i_created_a_benchmark_to_compare_the_following/

## XUnit + Moq
Utilizando Moq é possível contabilizar quantas vezes um método é chamado. Porém esse número de chamadas é acumulado pois o construtor é chamado x vezes para uma quantidade x de métodos definidos no teste (Constructor and Dispose).
Utilizando o Dispose dessa forma de testes do XUnit, pode-se resetar essa quantidade de chamadas para serem verificadas de forma correta em cada teste.
?

Fontes:
https://xunit.net/docs/shared-context
https://stackoverflow.com/questions/4163679/reset-mock-verification-in-moq


## Unit of Work: DataContext x TransactionScope:
????????

Fontes:


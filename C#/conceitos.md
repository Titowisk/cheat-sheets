# Conceitos e palavras chaves importantes

## Enum x Enumerations x Table Per Hierarchy Inheritance
Os três representar formas de se categorizar uma entidade. Evitam criar novas tabelas.

### Enum
Um conjunto de constantes que repesentam valores inteiros.

### Enumerations
Enumerations utiliza uma classe abstrata para definir enumerações mais verbosas e com mais funcionalidades.

### TPH
Consiste em implementar várias entidades diferentes porém similares utilizando uma mesma tabela do banco. Reduzindo assim a quantidade de tabelas no banco e também, possivelmente, a quantidade de joins para obter dados.

Fontes:

https://docs.microsoft.com/pt-br/dotnet/csharp/language-reference/builtin-types/enum
https://docs.microsoft.com/pt-br/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/enumeration-classes-over-enum-types
https://www.learnentityframeworkcore.com/inheritance/table-per-hierarchy
https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/SeedWork/Enumeration.cs
https://lostechies.com/jimmybogard/2008/08/12/enumeration-classes/
https://ardalis.com/enum-alternatives-in-c/


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

### One interface with multiple implementations
Cria-se um factory method que utiliza  `IServiceProvider.GetService(Type serviceType)`para buscar serviços em tempo de execução (runtime)
Tem pessoas argumentando que essa estratégia é um (service locator anti-pattern), que seria melhor utilizar abstract factory de uma determinada forma.

Fontes:

https://stackoverflow.com/questions/39072001/dependency-injection-resolving-by-name

https://www.c-sharpcorner.com/article/dependency-injection-with-multiple-implementations-of-the-same-interface/

https://blog.ploeh.dk/2010/02/03/ServiceLocatorisanAnti-Pattern/ 

https://stackoverflow.com/questions/31950362/factory-method-with-di-and-ioc/31956803#31956803 (abstract factory suggestion)

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

## Perfomance: Tasks e Async/Await

### .NET ThreadPool starvation

Fontes:

https://www.reddit.com/r/csharp/comments/giexhm/performance_best_practices_in_c/

https://medium.com/criteo-labs/net-threadpool-starvation-and-how-queuing-makes-it-worse-512c8d570527

### Separate Configuration Classes
Usa um arquivo por entidade do modelo para configurar mapeamento com o banco de dados

Fontes:
https://www.learnentityframeworkcore.com/configuration/fluent-api#separate-configuration-classes

## Security

### Passwords
Guardando em texto puro definitivamente não é seguro.

Usando algoritmos de encriptagem? evita certos problemas. Mas o hash gerado por uma determinada palavra é sempre a mesma. Então se um atacante pegar uma lista das senhas
mais comuns e passar por encriptagem? ele pode acabar descobrindo o algoritmo utilizado. (partindo do pressuposto que ele possua acesso ao banco claro)

Usando um salt, duas palavras iguais irão gerar hashs diferentes. O que é mais seguro.

Fontes:

https://medium.com/dealeron-dev/storing-passwords-in-net-core-3de29a3da4d2#:~:text=BCrypt%20and%20PBKDF2%20are%20both,slower%20the%20algorithm%2C%20the%20better.

## NOLOCK x READPAST
Normalmente transações do tipo Write, bloqueiam outras transações. Se eu tentar ler uma tabela bloqueada não vou conseguir. 
É necessário esperar um rollback ou um commit.

**NOLOCK**: usando o nolock, é possível ler os dados bloqueados e obter os resultados de suas operações. Se ocorrer rollback, isso
significa que meu READ obteve dados que não existem.

**READPAST**: também torna possível fazer leitura em dados bloqueados, mas somente irão ler aqueles que não sofrem alterações
das transações WRITE abertas.


## Data Table as Parameters

????????????

Fontes:
- https://stackoverflow.com/questions/13806395/is-it-possible-to-get-table-type-definitions-from-information-schema
- https://codingsight.com/passing-data-table-as-parameter-to-stored-procedures/#:~:text=A%20table%2Dvalued%20parameter%20is,of%20the%20table%2Dvalued%20parameters.

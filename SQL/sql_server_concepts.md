## NOLOCK x READPAST
Normalmente transações do tipo Write, bloqueiam outras transações. Se eu tentar ler uma tabela bloqueada não vou conseguir. 
É necessário esperar um rollback ou um commit.

NOLOCK: usando o nolock, é possível ler os dados bloqueados e obter os resultados de suas operações. Se ocorrer rollback, isso
significa que meu READ obteve dados que não existem.

READPAST: também torna possível fazer leitura em dados bloqueados, mas somente irão ler aqueles que não sofrem alterações
das transações WRITE abertas.

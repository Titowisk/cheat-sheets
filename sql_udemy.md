# O Curso Completo de Banco de Dados e SQL, sem mistérios!
## Link com todos os softwares do curso
https://www.dropbox.com/sh/dnvvg3dvwbmla0u/AACJj-BkIHgjO-l_kenEOwPda?dl=0

## Configurações

- Imagem de CD de Adicionais de Convidados
- Ir no services e parar a atualização automática do Windows 10
- Área de Transferência > Bidirecional. (ctrl+c e ctrl+v funcionam entre ambientes)
- dispositivos > pastas compartilhadas (tornar permanente e montar automaticamente)

## Instalação do My SQL Server Community
O professor utilizou configurações customizadas ( disponíveis no vídeo ).
- Type and Networking:
Standalone é quando o banco de dados funciona localmente: cliente e servidor na mesma máquina ou em máquinas diferentes.
Cluster é quando o banco de dados funciona em uma máquina externa (quando necessário mais poder de processamento)

## SGBD - Comand Line Client

```
show variables like 'datadir';
```
Mostra o diretório de dados do MySQL

## Modelagem
- Modelagem Conceitual - rascunho
- Modelagem Lógica - usa programas que fazem diagramas UML
- Modelagem Física - scripts

## Filtros
Filtro com WHERE
```
SELECT NAME, GENDER, ADDRESS FROM CLIENTE 
WHERE GENDER = 'M';


```
Filtro com LIKE e caracter coringa (diminui perfomance da consulta)
```
SELECT NAME, ADDRESS FROM CLIENTE
 WHERE ADDRESS LIKE '%RJ%';
```

## COUNT, GROUPBY E PERFOMANCE DE OPERADORES LÓGICOS:
- operadores lógicos:
```
SELECT NAME, EMAIL FROM CLIENTE
WHERE GENDER = "M" OR ADDRESS LIKE "%RJ";

SELECT NAME, EMAIL FROM CLIENTE
WHERE GENDER = "M" AND ADDRESS LIKE "%RJ";
```

- group by:
```
SELECT GENDER, COUNT(*) AS 'QUANTIDADE' FROM CLIENTE
GROUP BY GENDER;
```

- Dica de perfomance:

AO FAZER OS FILTROS, A ORDEM IMPORTA NA OTIMIZAÇÃO DE PERFOMANCE.
EXEMPLO:
Em um banco de dados com 70% de mulheres e 30% de moradores do RJ
a consulta:
```
SELECT NOME, SEXO, ENDERECO 
FROM CLIENTE
WHERE
    SEXO = 'F'
    OR CIDADE = 'RIO DE JANEIRO'
```
Em 70% dos casos, a consulta só precisa verificar o SEXO para trazer os dados solicitados.
E somente em 30% dos casos a consulta irá verificar SEXO e CIDADE 


## Usando UPDATE:
- O update deve SEMPRE ser utilizado com where, se não afeta toda a tabela.
```
UPDATE CLIENTE
SET EMAIL = 'LILLIAN@HOTMAIL.COM'
WHERE NAME = 'LILLIAN';
```

## Usando DELETE:
- O mesmo ocorre com o delete, se não usar o WHERE ele afeta toda a tabela.
```
DELETE FROM CLIENTE
WHERE NAME = 'ANA';
```

## Modelagem de Banco de Dados para sistemas:

### Normalização 3NF:

- 1ª Forma Normal:
1- TODO CAMPO VETORIZADO SE TORNA UMA TABELA
* VETOR/LISTA DE ELEMENTOS DE MESMA NATUREZA

2- TODO CAMPO MULTIVALORADO SE TORNA UMA TABELA
* CAMPO QUE PODE SER DIVIDIDO EM MÚLTIPLOS VETORES

3- TODA TABELA NECESSITA DE UM CAMPO QUE IDENTIFIQUE TODO O REGISTRO
COMO SENDO ÚNICO - CHAVE PRIMÁRIA OU PRIMARY KEY

- Cardinalidade x Obrigatoriedade:
(X,Y) 
OBRIGATORIEDADE
QUANDO X = 1 É OBRIGATORIO
QUANDO X = 0 É OPCIONAL

CARDINALIDADE
QUANDO Y = 1 ITEM ÚNICO
QUANDO Y = N O ITEM PODE TER QUANTIDADE >= 1 

### Seleção, Projeção e Junção:

- Seleção:

- Projeção:

- Junção (JOIN):

### Views:

- criar e apagar view:

### Order by:

### Delimitador e Estado do servidor:


## Procedures - Procedimentos Armazenados:


### Procedures com parâmetros:

### Procedures com tabelas:

### Funções agregadoras:

## Subqueries:



## Palavras-Chave
- SGBD - Sistema de Gerenciamento de Banco de Dados


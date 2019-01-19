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

### Foreign Key:
```
CREATE TABLE ADDRESS (
    ID_ADDRESS INT PRIMARY KEY AUTO_INCREMENT,
    STREET VARCHAR(30) NOT NULL,
    NEIGHBORHOOD VARCHAR(30) NOT NULL,
    CITY VARCHAR(30) NOT NULL,
    STATE CHAR(2) NOT NULL,
    
    -- FOREIGN KEY STRUCTURE
    FK_CLIENT INT UNIQUE,
    FOREIGN KEY(FK_CLIENT)
    REFERENCES CLIENT(ID_CLIENT)
);
```
É A PRIMARY KEY DE UMA TABELA QUE VAI PARA OUTRA TABELA FAZER O LINK 
A LOCALIZAÇÃO DA FK É DE ACORDO COM AS REGRAS DE NEGÓCIO (E BOM SENSO)

### Seleção, Projeção e Junção:

- Seleção: RETIRAR UM SUBCONJUNTO DE UM CONJUNTO

- Projeção: TUDO QUE QUEREMOS PROJETAR NA TABELA

- Junção (JOIN):
```
SELECT C.NAME, C.GENDER, 
  A.NEIGHBORHOOD, A.CITY, 
  P.TYPE, P.NUMBER
FROM CLIENT AS C
INNER JOIN ADDRESS A ON C.ID_CLIENT = A.FK_CLIENT
INNER JOIN PHONE P ON C.ID_CLIENT = P.FK_CLIENT;
```

### Views:

- criar e apagar view:
*dica: FAZER QUERY NA VIEW TEM MENOS PERFORMANCE QUE FAZER A QUERY DIRETA

```
CREATE VIEW RELATORIO AS
SELECT 
    C.NAME, C.GENDER, IFNULL(C.EMAIL, '---') AS "E-MAIL",
    P.TYPE, P.NUMBER,
    A.NEIGHBORHOOD, A.CITY, A.STATE
FROM CLIENT AS C
INNER JOIN PHONE P ON P.FK_CLIENT = C.ID_CLIENT
INNER JOIN ADDRESS A ON A.FK_CLIENT = C.ID_CLIENT;
```

- As views aparecem no show tables, e podem ser apagadas com o comando drop <nome_da_view>.
É possível fazer queies em views, mas não é possível fazer insert ou delete.

### Order by:
```
SELECT NAME, GENDER, CPF, CITY FROM CLIENT
INNER JOIN ADDRESS ON FK_CLIENT = ID_CLIENT
ORDER BY NAME, CPF ASC;
```
### Delimitador e Estado do servidor:

- É possível mudar o delimitador padrão do my_sql ";".
```
DELIMITER $
```

- Para saber informações sobre o banco:
```STATUS```


## Procedures - Procedimentos Armazenados:

FAZ O PROCESSAMENTO DA REGRA DE NEGÓCIO, SEM A NECESSIDADE DE UMA LINGUAGEM BACKEND
COMO JAVA, PYTHON...

QUANDO A REGRA DE NEGÓCIO (RN) ESTIVER NO CONTROLLER,
É MAIS FÁCIL MIGRAR DE BANCO DE DADOS, POIS O BD SÓ ESTARÁ
ARMAZENANDO DADOS QUE SÃO IMUTÁVEIS...

- PRIMEIRO PASSO (IMPORTANTE NA HORA DE CRIAR, NA DE CHAMAR NÃO)

```
DELIMITER $
```

- CRIANDO

```
CREATE PROCEDURE CONTA()
BEGIN
    SELECT 10 + 10 AS 'CONTA';
END
$
```

- CHAMANDO

```CALL CONTA()$```

-- APAGANDO

```DROP PROCEDURE CONTA```

### Procedures com parâmetros:

```
DELIMITER $

CREATE PROCEDURE CONTA(N1 INT, N2 INT)
BEGIN
    SELECT N1 + N2 AS 'CONTA';
END
$

DELIMITER ;
```

### Procedures com tabelas:
- Procedure para fazer cadastro de curso em uma tabela CURSO:

```
DELIMITER $$

CREATE PROCEDURE CAD_CURSO(P_NOME VARCHAR(30), P_HORAS INT(3), P_VALOR FLOAT(10,2))
BEGIN 
    INSERT INTO CURSOS (NOME, HORAS, VALOR)
    VALUES(P_NOME, P_HORAS, P_VALOR);
END 
$$

DELIMITER ;
```

```
CALL CAD_CURSO('BI SQL SERVER', 35, 200.00);
```

### Funções agregadoras:
MAX(), MIN(), AVG(), SUM(), COUNT() ...

*dica: TRUNCATE()
```
SELECT MAX(JANEIRO) AS MAX_JAN,
       MIN(JANEIRO) AS MIN_JAN,
	   TRUNCATE( VG(JANEIRO), 2) AS MEDIA
	   FROM VENDEDORES;
```

## Subqueries:

```
SELECT NOME, MARCO FROM VENDEDORES
WHERE MARCO = (SELECT MIN(MARCO) FROM VENDEDORES);

SELECT NOME, FEVEREIRO FROM VENDEDORES 
WHERE FEVEREIRO > (SELECT AVG(FEVEREIRO) FROM VENDEDORES);
```

## Operações em linha:
AS FORMULAS MOSTRADAS TRABALHAM EM COLUNA,
PARA OPERAR COM LINHAS É NECESSÁRIO FAZER MANUALMENTE

```
SELECT NOME, JANEIRO, FEVEREIRO, MARCO,
    (JANEIRO + FEVEREIRO + MARCO) AS 'TOTAL',
    TRUNCATE( (JANEIRO + FEVEREIRO + MARCO)/ 3, 2) AS 'MEDIA'
    FROM VENDEDORES;
```

## Alterar Tabelas:
 É possível adicionar colunas, alterar tipos, adicionar PK ou FK, renomear tabela...
 (melhor pesquisar a sintaxe do que botar todas as opções aqui)

- Mostrar detalhes da tabela criada:
```
SHOW CREATE TABLE <NOME_DA_TABELA>
```

## Organização de chaves:
Quando uma FK é criada, o BD cria, automaticamente, uma CONSTRAINT que representa esse relacionamento. Porém
o melhor é criar isso manualmente para organizar melhor.

É uma boa prática, criar as tabelas e depois criar as CONSTRAINTS.

-- Como criar CONSTRAINTS:

## Triggers:

- Estrutura de uma trigger:

- Trabalhar com tabelas de diferentes databases:

*Dica: cuidado com after e before em uma trigger de insert

- Sugestão de trigger: auditoria

## Autorelacionamento:
Quando a tabela se relaciona consigo:
```
CREATE TABLE CURSOS (
    ID_CURSO INT PRIMARY KEY AUTO_INCREMENT,
    NOME VARCHAR(30),
    HORAS INT,
    VALOR FLOAT(10,2),
    IDK_PREREQ INT
);

ALTER TABLE CURSOS ADD CONSTRAINT FK_PREREQ
FOREIGN KEY(IDK_PREREQ) REFERENCES CURSOS(ID_CURSO);
```
No caso, a chave primária de CURSOS serve como FK dela mesma.

## Cursores:
Cursor é um vetor [].
Pode-se utilizar-lo com iteração para gerar novas tabelas com cálculos:
```
CREATE PROCEDURE INSEREDADOS()
BEGIN
    DECLARE FIM INT DEFAULT 0;
    DECLARE VAR1, VAR2, VAR3, VTOTAL, VMEDIA INT;
    DECLARE VNOME VARCHAR(50);

    DECLARE REG CURSOR FOR(
        SELECT NOME, JAN, FEV, MAR FROM VENDEDORES
    );
    

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET FIM = 1;

    OPEN REG;

    REPEAT
        FETCH REG INTO VNOME, VAR1, VAR2, VAR3;
        IF NOT FIM THEN
            SET VTOTAL = VAR1 + VAR2 + VAR3;
            SET VMEDIA = VTOTAL / 3;
            DELETE FROM VEND_TOTAL WHERE NOME = VNOME;
            INSERT INTO VEND_TOTAL VALUES(VNOME, VAR1, VAR2, VAR3, VTOTAL, VMEDIA);
        END IF;
    UNTIL FIM END REPEAT;

    CLOSE REG;

END
$
```
Ela então pega a tabela VENDEDORES, itera sobre suas linhas e cria um Total e uma Média para cada linha.
- REG = [(nome, jan, fev, mar), (nome, jan, fev, mar), (nome, jan, fev, mar)...]
- REG É ARMAZENADO NA MEMÓRIA RAM.
- REG DEVE SER FECHADO APÓS SUA UTILIZAÇÃO PARA LIBERAR ESPAÇO NA MEMÓRIA


## Segunda e Terceira forma nominal:
 PRIMEIRA FN
	 ATOMICIDADE - UM CAMPO NAO PODE SER DIVISIVEL
	 UM CAMPO NAO PODE SER VETORIZADO
	 PK CHAVE PRIMARIA
 
 Segunda FN
    	Dependência direta
Terceira FN
 	dependência transitória
	
```

CREATE DATABASE CONSULTORIO;

USE CONSULTORIO;

CREATE TABLE PACIENTE(
	ID_PACIENTE INT PRIMARY KEY AUTO_INCREMENT,
	NOME VARCHAR(30),
	SEXO CHAR(1),
	EMAIL VARCHAR(30),
	NASCIMENTO DATE
);

CREATE TABLE MEDICO(
	ID_MEDICO INT PRIMARY KEY AUTO_INCREMENT,
	NOME VARCHAR(30),
	SEXO CHAR(1),
	ESPECIALIDADE VARCHAR(30),
	FUNCIONARIO ENUM('S','N')
);

CREATE TABLE HOSPITAL(
	ID_HOSPITAL INT PRIMARY KEY AUTO_INCREMENT,
	NOME VARCHAR(30),
	BAIRRO VARCHAR(30),
	CIDADE VARCHAR(30),
	ESTADO CHAR(2)
);

CREATE TABLE CONSULTA(
	ID_CONSULTA INT PRIMARY KEY AUTO_INCREMENT, -- SEGUNDA FORMA NORMAL
	IDK_PACIENTE INT,
	IDK_MEDICO INT,
	IDK_HOSPITAL INT,
	DATA DATETIME,
	DIAGNOSTICO VARCHAR(50)
);

CREATE TABLE INTERNACAO(
	ID_INTERNACAO INT PRIMARY KEY AUTO_INCREMENT,
	ENTRADA DATETIME,
	QUARTO INT,
	SAIDA DATETIME,
	OBSERVACOES VARCHAR(50),
	IDK_CONSULTA INT UNIQUE	-- TERCEIRA FORMA NORMAL
);  

-- RELACIONAMENTOS
-- FK_(DE ONDE VEM)_(PARA ONDE VAI)

ALTER TABLE CONSULTA ADD CONSTRAINT FK_PACIENTE_CONSULTA
FOREIGN KEY (IDK_PACIENTE) REFERENCES PACIENTE(ID_PACIENTE);

ALTER TABLE CONSULTA ADD CONSTRAINT FK_MEDICO_CONSULTA
FOREIGN KEY (IDK_MEDICO) REFERENCES MEDICO(ID_MEDICO);

ALTER TABLE CONSULTA ADD CONSTRAINT FK_HOSPITAL_CONSULTA
FOREIGN KEY (IDK_HOSPITAL) REFERENCES HOSPITAL(ID_HOSPITAL);

ALTER TABLE INTERNACAO ADD CONSTRAINT FK_CONSULTA_INTERNACAO
FOREIGN KEY (IDK_CONSULTA) REFERENCES CONSULTA(ID_CONSULTA);
```

## Palavras-Chave
- SGBD - Sistema de Gerenciamento de Banco de Dados


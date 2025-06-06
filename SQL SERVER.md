# SQL Server -> Servidor de comunicação dos bancos de dados.

SQL  Server Management Studio -> SSMS, gerenciador de banco de dados e faz a comunicação e comandos no SQL Server.

Abrir o SSMS - Conexão é feita com o database engine e server name: localhost\SQLEXPRESS

Restaurar um banco de dados -> abrir o SSMS, ir em Databases, com o botão direito e ir em Restore Databases.

--- 

SELECT: Seleciona linhas do meu banco de dados.
Query: select FirstName, LastName from Person.Person;

---

DISTINCT: Omitir dados duplicados de uma ou mais colunas.
Query: select DISTINCT FirstName from Person.Person;

---

WHERE: filtra os dados de acordo com suas condições.
'=' Igual
'>' MAIOR QUE
'<' MENOR QUE
'>=' MAIOR QUE OU IGUAL
'<=' MENOR QUE OU IGUAL
'<>' DIFERENTE DE
'AND'  OPERADOR E
'OR' OPERADOR OU

---

Query: select * from Person.Person where LastName = 'miller' AND FirstName = 'anna';

```
select * from production.Product where color = 'blue' or color = 'black';

select * from production.Product where ListPrice > 1500 and ListPrice < 5000;
```

```
1° Desafio
Select distinct(Name), weight from Production.Product  where weight > 500 and weight <= 700;

2° Desafio

SELECT p.FirstName, p.LastName FROM HumanResources.Employee e
LEFT JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID
WHERE e.MaritalStatus = 'M' AND e.SalariedFlag = 1;

3° Desafio

SELECT p.FirstName, p.LastName, e.EmailAddress FROM Person.Person p 
LEFT JOIN Person.EmailAddress e 
    ON e.BusinessEntityID = p.BusinessEntityID
WHERE p.LastName = 'krebs' ;
```

---

COUNT: Utilizado para contar a quantidade de linhas que são retornadas em uma condição

```
SELECT COUNT(title) from person.person

SELECT COUNT(DISTINCT title) from person.person
```

```
1° Desafio
Select COUNT(*) as qtd_itens from Production.Product;

2° Desafio
Select COUNT(Size) as qtd_distict_products from Production.Product;
```

---

TOP: filtrar, limitando a quantidade de retornos possíveis.

```
SELECT TOP 10 * from Production.Product;
```

---

ORDER BY: ordena os resultados de acordo com uma ou mais linhas de forma crescente ou decrescente.

```
SELECT coluna1, coluna2 from tabela order by coluna1 asc/desc

SELECT * from person.Person order by FirstName asc, LastName desc;

SELECT * from person.Person order by FirstName asc, LastName desc;
```

```
1° Desafio
SELECT TOP 10 * from Production.Product order by ListPrice desc;

2° Desafio
SELECT TOP 10 Name, ProductNumber from Production.Product where ProductID < 5 order by Name asc
```

---

BETWEEN: Usado para encontrar valor entre um valor mínimo e máximo. DATA e INT/FLOAT

```
Select * from Production.Product where ListPrice between 1000 and 1500;
```

---

NOT:  pode ser usado na negação 

```
Select * from Production.Product where ListPrice NOT between 1000 and 1500;

Select * from HumanResources.Employee where HireDate BETWEEN '2009/01/01' AND '2010/01/01' order by HireDate
```

---

IN: Para verificar se um valor correspondem com qualquer valor passado na lista de valores.

color in ('BLUE', 'BLACK')
valor in (SELECT valor from nomeDaTabela) -> SubQuery

```
Select * from Person.Person where BusinessEntityID in (2,7,13)
```

---

LIKE: Quando você precisa encontrar algo que contém uma parte específica 

```
SELECT * from Person.Person WHERE FirstName like 'ovi%'

SELECT * from Person.Person WHERE FirstName like '%TO'

SELECT * from Person.Person WHERE FirstName like '%essa%'

SELECT * from Person.Person WHERE FirstName like '%ro_'
```

```
1° Desafio
select COUNT(name) as countlist from Production.Product where 1 = 1 and ListPrice > 1500

2° Desafio
select COUNT(BusinessEntityID) as countpersons from Person.Person where 1 = 1 and LastName like 'P%'

3° Desafio
select COUNT( DISTINCT(Address.CITY)) from Person.Address where 1 = 1

4° Desafio
select  DISTINCT(Address.CITY) from Person.Address where 1 = 1

5° Desafio
select COUNT(Product.Color ) from Production.Product where 1 = 1 AND Product.Color = 'Red' AND Product.ListPrice >= 500 and Product.ListPrice <= 1000

6° Desafio
select COUNT(Product.Name) from Production.Product where 1 = 1 and Product.Name like '%road%'
```

---

REGEX: + avançado que o LIKE

Regex normalmente vem entre // nas linguagens.

as letras ao final significam flags que vão mudar alguns comportamentos do REGEX

g -> global, todas as ocorrências, não só uma

i -> insensitive, A <> a

m -> multiline

. -> significa qualquer caractere

| -> OR

() -> group

[a-z] | [0-9] -> sequência

^ -> exceto, ou seja, se tiver um [^et], irá pegar todas as letras menos o 'e' e o 't'.
    Se estiver no começo da expressão, ele irá ver se começa com aquela sequência: /^este/

+ -> agrupa como um único grupo caso os valores seguintes sejam iguais: essencial > /(s+)/ > 'ss' como um array único

* -> quando for 0 ou mais, ou seja, é o + com a opção do 0

? -> torna aquele grupo opcional, caso não exista irá ignorar

s{2,3} -> pega onde existe 2 ou 3 valores seguidos

$ -> precisa terminar com um valor: /este$/

\ -> saber o caractere literal: /\./ para encontrar um . no texto

[a-z0-9] -> Já junta letras a números

```
LeetCode test: ((^|\s)RA[a-zA-Z0-9]{5}-[a-zA-Z0-9]{2}(\s|$))

Validar e-mail: /([a-z0-9\.\-]{2,}@)([a-z0-9]{2,}\.)([a-z]{2,})(\.[a-z]{2,})?/

Validar telefone: /([\(0-9\)]{4})\s(9)?([0-9]{4})-([0-9]{4})/
```

```
SELECT * FROM products WHERE description REGEXP '^* SN[0-9]{4}-[0-9]{4}(?![0-9])' ORDER BY product_id;
```

---

MIN, MAX, SUM e AVG: Funções de agregação, basicamente agregam ou combinam dados de uma tabela em 1 resultado único.

```
select SUM(SalesOrderDetail.LineTotal) as "SUM" from Sales.SalesOrderDetail where 1 = 1 

select MAX(SalesOrderDetail.LineTotal) from Sales.SalesOrderDetail where 1 = 1 

select MIN(SalesOrderDetail.LineTotal) from Sales.SalesOrderDetail where 1 = 1 

select AVG(SalesOrderDetail.LineTotal) from Sales.SalesOrderDetail where 1 = 1 
```

---

GROUP BY: Basicamente divide o resultado da sua pesquisa em grupos. Para cada grupo você pode aplicar uma função de agregação.

```
SELECT coluna1, função(coluna2) from nomeTabela GROUP BY coluna1

Select SpecialOfferID, SUM(UnitPrice) as "SOMA" from Sales.SalesOrderDetail GROUP BY SpecialOfferID

Select ProductID, SUM(UnitPrice) as "SOMA" from Sales.SalesOrderDetail GROUP BY ProductID

Select ProductID, SUM(ProductID) as "QUANTOS" from Sales.SalesOrderDetail GROUP BY ProductID

Select Color, AVG(ListPrice) as Média from Production.Product GROUP BY Color
```

```
1° Desafio
Select MiddleName, COUNT(MiddleName) from Person.Person GROUP BY MiddleName

2° Desafio
Select ProductID, AVG(OrderQty) as "AVGQTY" from Sales.SalesOrderDetail GROUP BY ProductID

Select Product.Name, AVG(OrderQty) as "AVGQTY" from Sales.SalesOrderDetail LEFT JOIN Production.Product on SalesOrderDetail.ProductID = Product.ProductID GROUP BY Product.Name

3° Desafio
Select TOP 10 SalesOrderID, SUM(LineTotal) as "TOTAL" from Sales.SalesOrderDetail GROUP BY SalesOrderID order by TOTAL DESC

4° Desafio
select ProductID, Count(ProductID) as "Count_Sales", AVG(OrderQty) as "AVG_QTY" from Production.WorkOrder group by ProductID
```

---

Having: O having é basicamente muito usado em junção com o group by para filtrar resultados de um agrupamento.

De uma forma mais simples eu gosto de entender ele como um where para dados agrupados.

```
Select coluna1, funcaoAgregacao(coluna2)
from nomeTabela
GROUP BY coluna1
HAVING condicao;
```

A grande diferença entre HAVING e WHERE.
Having -> depois do agrupamento 
Where -> antes do agrupamento

```
Select FirstName, count(FirstName) as "quantidade" from Person.Person group by FirstName having COUNT(FirstName) > 10 order by quantidade, FirstName

Select ProductID, SUM(LineTotal) as "Total" from
Sales.SalesOrderDetail group by ProductID having SUM(LineTotal) >= 162000 AND SUM(LineTotal) <= 500000
```

```
1° Desafio
select StateProvinceID, COUNT(StateProvinceID) as "QTD_State" from Person.Address group by StateProvinceID having COUNT(StateProvinceID) > 1000 order by QTD_State DESC

2° Desafio
Select ProductID, AVG(LineTotal) as "TOTAL" from Sales.SalesOrderDetail group by ProductID having AVG(LineTotal) < 1000000
```

---

INNER JOIN: Juntar tabelas por meio de uma coluna de idêntificação(chave primária), apenas a intercessão 

```
Select C.ClienteId, C.Nome, E.Rua, E.cidade from Cliente C
INNER JOIN Endereco E on E.EnderecoId = C.EnderecoId

Select p.BusinessEntityID, p.FirstName, p.LastName, pe.EmailAddress from Person.Person as P INNER JOIN Person.EmailAddress PE on P.BusinessEntityID = PE.BusinessEntityID
```

---

LEFT / RIGHT JOIN =  Juntar tabelas por meio de uma coluna de idêntificação(chave primária), porém pega os dados que não possuem correspondência também

```
SELECT * FROM Person.Person PP LEFT JOIN Sales.PersonCreditCard PC ON PP.BusinessEntityID = PC.BusinessEntityID
```

---

UNION: Ajuda a combinar dois ou mais resultados em um select.

```
SELECT  coluna1, coluna2
FROM tabela1
UNION
SELECT coluna1, coluna2
FROM tabela2
```

---

UNION ALL -> mostra duplicatas

```
Select ProductID, Product.Name, ProductNumber from Production.Product WHERE Product.Name LIKE '%CHAIN%'
UNION
Select ProductID, Product.Name, ProductNumber from Production.Product WHERE Product.Name LIKE '%Decal%'
```

---

SELF-JOIN: 

```
select A.ContactName, B.ContactName from Customers as A INNER JOIN Customers as B on A.Region = B.Region

Select A.FirstName, A.HireDate, B.FirstName, B.HireDate from Employees AS A LEFT JOIN Employees AS B on A.EmployeeID = B.EmployeeID where DATEPART(YEAR, A.HireDate) = DATEPART(YEAR, B.HireDate)

Select A.ProductID, A.Discount, B.ProductID, B.Discount from dbo.Order Details as A INNER JOIN dbo.Order Details as B ON A.Discount = B.Discount

SELECT A.column_name, B.column_name
FROM table_name AS A, table_name AS B
WHERE condition;
```

---

SUBQUERY: uma query dentro de outra que é utilizada para algum tipo de comparação.

```
select * from Production.Product where ListPrice > (select AVG(ListPrice) from Production.Product)

SELECT * from Person.Address where StateProvinceID in ( SELECT StateProvinceID from person.StateProvince WHERE NAME = 'Alberta')
```

---

DATEPART: saber informações relevantes de datas.

```
SELECT SalesOrderId, DATEPART(year,  OrderDate) as 'Mês' FROM Sales.SalesOrderHeader

SELECT AVG(TotalDue) as Media, DATEPART(month,  OrderDate) as 'Mês' FROM Sales.SalesOrderHeader GROUP BY DATEPART(month,  OrderDate)
```

---

OFFSET: serve para ignorar as primeiras x linhas de retorno e pode ser combinado com o LIMIT

Por exemplo: Gostaria de pegar os o segundo melhor funcionário em questão de salário

```
select e.name from Employee as e order by e.salary Offset 1 limit 1
```

---

OPERAÇÃO EM STRINGS 

```
SELECT CONCAT(FirstName, ' ', LastName) from Person.Person 

SELECT UPPER(FirstName), LOWER(FirstName) from Person.Person 

SELECT LEN(FirstName) from Person.Person 

SELECT SUBSTRING(FirstName, 1,3) from Person.Person

SELECT REPLACE(ProductNumber, '-', '#') from Production.Product
```

---

FUNÇÕES MATEMÁTICAS

```
SELECT MAX(LineTotal) from Sales.SalesOrderDetail

SELECT MIN(LineTotal) from Sales.SalesOrderDetail

SELECT AVG(LineTotal) from Sales.SalesOrderDetail

SELECT ROUND(AVG(LineTotal),2) from Sales.SalesOrderDetail

SELECT SQRT(LineTotal) from Sales.SalesOrderDetail
```

---

MODA:

```
SELECT
    tipo,
    COUNT(*) AS frequencia
FROM
    produtos
GROUP BY
    tipo
ORDER BY
    frequencia DESC
LIMIT 1;
```

---

TIPOS DE DADOS

1. Boleanos
2. Caracteres
3. Números
4. Temporais

Boleano -> int, podendo ser 1 ou 0

Caracteres ->
tamanho fixo - char. O valor definido sempre vai ser alocado na memória independente do valor utilizado. 

tamanhos variáveis - varchar ou nvarchar. Permite inserir até uma quantidade máxima e irá utilizar até a quantidade utilizada na memória.

Números -> 
Valores Exatos

1. TINYINT -  não tem valores fracionados
2. SMALLINT - TINYINT com maior valor inteiro
3. INT - SMALLINT com maior valor inteiro
4. BIGINT - INT com maior valor inteiro
5. NUMERIC ou DECIMAL - valores exatos, porém permite ter parte fracionadas que também podem ser especificadas a precisão e a escala (escala é o número de digitos na parte fracional) ex: NUMERIC (5,2) 113,44

Valores Aproximados
1. REAL - tem precisão aproximada de até 15 digitos
2. FLOAT - mesmo conceito de REAL

---

Temporais

DATE - armazena data no formato aaaa/mm/dd
DATETIME - armazena data e horas no formato aaaa/mm/dd::hh::mm::ss
DATETIME2 - armazena data e horas com milissegundos no formato aaaa/mm/dd::hh::mm::sssssss
SMALLDATETIME - data e horas nos respeitando o limite entre '1900-01-01:00:00:00' até '2079-06-06:23:59:59'
TIME - horas, minutos, segundos e milissegundos respeitando o limite de '00:00:00.0000000' até '23:59:59.9999999'
DATETIMEOFFSET - permite armazenar informações de data e horas incluindo o fuso horário

---

CHAVE PRIMARIA E ESTRANGEIRA

* Chave primária, coluna que possui registro único para identificar uma coluna.
* Chave estrangeira, coluna de uma tabela que possui o registro único de outra
* Relacionamento é fazer vínculo entre chave primária com chave secundária de outra

---

CRIAR TABELA

```
CREATE TABLE nome_tabela (
	nomeColuna tipoDado PRIMARY KEY
	nomeColuna tipoDado ...
)
```

Principais tipos de restrições que podem ser aplicadas
NOT NULL - não permite nulos
UNIQUE - Força que todos os valores sejam diferentes
PRIMARY KEY - uma junção de NOT NULL e UNIQUE
FOREIGN KEY - identifica unicamente uma linha outra tabela
CHECK - FORÇA uma condição específica em uma coluna
DEFAULT - força um valor padrão caso seja nulo

---

INSERT INTO - Insere valores em uma tabela 

```
INSERT INTO nomeTabela(coluna1, coluna2, ...) 
VALUES (valor1, valor2, ...),
 (valor1, valor2, ...),
 (valor1, valor2, ...),
```

---

UPDATE - Atualiza informações de uma tabela

```
UPDATE nomeTabela
set coluna1 = valor1
coluna2 = valor2
WHERE condicao
```

---

DELETE - deleta informações de uma tabela

```
DELETE from nomeTabela
where condicao
```

---

ALTER TABLE - Alterar a estrutura de uma tabela

ALTER TABLE nomeTabela
ACAO

- Add, Remover or alterar uma coluna
- Setar valores padrões para uma coluna
- Add ou Remover restrições de colunas
- Renomear uma tabela

```
ALTER TABLE youtube add ativo bit

ALTER TABLE youtube ALTER COLUMN categoria varchar(300) NOT NULL

EXEC sp_RENAME 'nomeTabela.nomeColunaAtual', 'nomeColunaNova', 'COLUMN'

EXEC sp_RENAME 'nomeTabela', 'nomeTabelaNova'
```

---

DROP TABLE - exclui uma tabela

```
DROP TABLE nomeTabela
```

---

TRUNCATE - Limpa a tabela

```
TRUNCATE TABLE Person.password
```

---

CHECK CONSTRAINT - Checar valores 

```
CREATE TABLE CarteiraMotorista(
	 id int NOT NULL,
	 Nome varchar(255) NOT NULL,
	 Idade int CHECK ( Idade >= 18)
);
```

---

NOT NULL - Não deixar nulo um valor

```
CREATE TABLE CarteiraMotorista(
	 id int NOT NULL,
	 Nome varchar(255) NOT NULL,
	 Idade int CHECK ( Idade >= 18)
);
```

---

UNIQUE - Não deixar adicionar valor repetido

```
CREATE TABLE CarteiraMotorista(
	 id int NOT NULL,
	 Nome varchar(255) NOT NULL,
	 Idade int CHECK ( Idade >= 18),
	 CodigoCNH int NOT NULL UNIQUE
);
```

---

VIEW - Guarda informações de select em uma variável 

```
CREATE VIEW '[Pessoas Simplificado]' AS
SELECT FirstName, MiddleName, LastName
from Person.Person
where title = 'Ms.'
```
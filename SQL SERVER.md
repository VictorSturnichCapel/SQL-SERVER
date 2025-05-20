SQL Server -> Servidor de comunicação dos bancos de dados.

SQL  Server Management Studio -> SSMS, gerenciador de banco de dados e faz a comunicação e comandos no SQL Server.

 Abrir o SSMS - Conexão é feita com o database engine e server name: localhost\SQLEXPRESS

Restaurar um banco de dados -> abrir o SSMS, ir em Databases, com o botão direito e ir em Restore Databases.

SELECT: Seleciona linhas do meu banco de dados.
Query: select FirstName, LastName from Person.Person;

DISTINCT: Omitir dados duplicados de uma ou mais colunas.
Query: select DISTINCT FirstName from Person.Person;

WHERE: filtra os dados de acordo com suas condições.
'=' Igual
'>' MAIOR QUE
'<' MENOR QUE
'>=' MAIOR QUE OU IGUAL
'<=' MENOR QUE OU IGUAL
'<>' DIFERENTE DE
'AND'  OPERADOR E
'OR' OPERADOR OU

Query: select * from Person.Person where LastName = 'miller' AND FirstName = 'anna';

select * from production.Product where color = 'blue' or color = 'black';

select * from production.Product where ListPrice > 1500 and ListPrice < 5000;

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

COUNT: Utilizado para contar a quantidade de linhas que são retornadas em uma condição

SELECT COUNT(title) from person.person

SELECT COUNT(DISTINCT title) from person.person

1° Desafio
Select COUNT(*) as qtd_itens from Production.Product;

2° Desafio
Select COUNT(Size) as qtd_distict_products from Production.Product;


TOP: filtrar, limitando a quantidade de retornos possíveis.

SELECT TOP 10 * from Production.Product;

ORDER BY: ordena os resultados de acordo com uma ou mais linhas de forma crescente ou decrescente.

SELECT coluna1, coluna2 from tabela order by coluna1 asc/desc

SELECT * from person.Person order by FirstName asc, LastName desc;

SELECT * from person.Person order by FirstName asc, LastName desc;

1° Desafio
SELECT TOP 10 * from Production.Product order by ListPrice desc;

2° Desafio
SELECT TOP 10 Name, ProductNumber from Production.Product where ProductID < 5 order by Name asc

BETWEEN: Usado para encontrar valor entre um valor mínimo e máximo. DATA e INT/FLOAT

Select * from Production.Product where ListPrice between 1000 and 1500;

NOT:  pode ser usado na negação 

Select * from Production.Product where ListPrice NOT between 1000 and 1500;

Select * from HumanResources.Employee where HireDate BETWEEN '2009/01/01' AND '2010/01/01' order by HireDate

IN: Para verificar se um valor correspondem com qualquer valor passado na lista de valores.

color in ('BLUE', 'BLACK')
valor in (SELECT valor from nomeDaTabela) -> SubQuery

Select * from Person.Person where BusinessEntityID in (2,7,13)

LIKE: Quando você precisa encontrar algo que contém uma parte específica 

SELECT * from Person.Person WHERE FirstName like 'ovi%'

SELECT * from Person.Person WHERE FirstName like '%TO'

SELECT * from Person.Person WHERE FirstName like '%essa%'

SELECT * from Person.Person WHERE FirstName like '%ro_'

REGEX: + Avançado que o LIKE

SELECT * FROM products
WHERE description REGEXP '^* SN[0-9]{4}-[0-9]{4}(?![0-9])'
ORDER BY product_id;

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

MIN, MAX, SUM e AVG: Funções de agregação, basicamente agregam ou combinam dados de uma tabela em 1 resultado único.

select SUM(SalesOrderDetail.LineTotal) as "SUM" from Sales.SalesOrderDetail where 1 = 1 

select MAX(SalesOrderDetail.LineTotal) from Sales.SalesOrderDetail where 1 = 1 

select MIN(SalesOrderDetail.LineTotal) from Sales.SalesOrderDetail where 1 = 1 

select AVG(SalesOrderDetail.LineTotal) from Sales.SalesOrderDetail where 1 = 1 


GROUP BY: Basicamente divide o resultado da sua pesquisa em grupos. Para cada grupo você pode aplicar uma função de agregação.

SELECT coluna1, função(coluna2) from nomeTabela GROUP BY coluna1

Select SpecialOfferID, SUM(UnitPrice) as "SOMA" from Sales.SalesOrderDetail GROUP BY SpecialOfferID

Select ProductID, SUM(UnitPrice) as "SOMA" from Sales.SalesOrderDetail GROUP BY ProductID

Select ProductID, SUM(ProductID) as "QUANTOS" from Sales.SalesOrderDetail GROUP BY ProductID

Select Color, AVG(ListPrice) as Média from Production.Product GROUP BY Color

1° Desafio
Select MiddleName, COUNT(MiddleName) from Person.Person GROUP BY MiddleName

2° Desafio
Select ProductID, AVG(OrderQty) as "AVGQTY" from Sales.SalesOrderDetail GROUP BY ProductID

Select Product.Name, AVG(OrderQty) as "AVGQTY" from Sales.SalesOrderDetail LEFT JOIN Production.Product on SalesOrderDetail.ProductID = Product.ProductID GROUP BY Product.Name

3° Desafio
Select TOP 10 SalesOrderID, SUM(LineTotal) as "TOTAL" from Sales.SalesOrderDetail GROUP BY SalesOrderID order by TOTAL DESC

4° Desafio
select ProductID, Count(ProductID) as "Count_Sales", AVG(OrderQty) as "AVG_QTY" from Production.WorkOrder group by ProductID

Having: O having é basicamente muito usado em junção com o group by para filtrar resultados de um agrupamento.

De uma forma mais simples eu gosto de entender ele como um where para dados agrupados.

Select coluna1, funcaoAgregacao(coluna2)
from nomeTabela
GROUP BY coluna1
HAVING condicao;

A grande diferença entre HAVING e WHERE.
Having -> depois do agrupamento 
Where -> antes do agrupamento

Select FirstName, count(FirstName) as "quantidade" from Person.Person group by FirstName having COUNT(FirstName) > 10 order by quantidade, FirstName

Select ProductID, SUM(LineTotal) as "Total" from
Sales.SalesOrderDetail group by ProductID having SUM(LineTotal) >= 162000 AND SUM(LineTotal) <= 500000

1° Desafio
select StateProvinceID, COUNT(StateProvinceID) as "QTD_State" from Person.Address group by StateProvinceID having COUNT(StateProvinceID) > 1000 order by QTD_State DESC

2° Desafio
Select ProductID, AVG(LineTotal) as "TOTAL" from Sales.SalesOrderDetail group by ProductID having AVG(LineTotal) < 1000000

INNER JOIN: Juntar tabelas por meio de uma coluna de idêntificação(chave primária), apenas a intercessão 

Select C.ClienteId, C.Nome, E.Rua, E.cidade from Cliente C
INNER JOIN Endereco E on E.EnderecoId = C.EnderecoId

Select p.BusinessEntityID, p.FirstName, p.LastName, pe.EmailAddress from Person.Person as P INNER JOIN Person.EmailAddress PE on P.BusinessEntityID = PE.BusinessEntityID

LEFT / RIGHT JOIN =  Juntar tabelas por meio de uma coluna de idêntificação(chave primária), porém pega os dados que não possuem correspondência também

SELECT * FROM Person.Person PP LEFT JOIN Sales.PersonCreditCard PC ON PP.BusinessEntityID = PC.BusinessEntityID

UNION: Ajuda a combinar dois ou mais resultados em um select.

SELECT  coluna1, coluna2
FROM tabela1
UNION
SELECT coluna1, coluna2
FROM tabela2

UNION ALL -> mostra duplicatas

Select ProductID, Product.Name, ProductNumber from Production.Product WHERE Product.Name LIKE '%CHAIN%'
UNION
Select ProductID, Product.Name, ProductNumber from Production.Product WHERE Product.Name LIKE '%Decal%'

SELF-JOIN: 

select A.ContactName, B.ContactName from Customers as A INNER JOIN Customers as B on A.Region = B.Region

Select A.FirstName, A.HireDate, B.FirstName, B.HireDate from Employees AS A LEFT JOIN Employees AS B on A.EmployeeID = B.EmployeeID where DATEPART(YEAR, A.HireDate) = DATEPART(YEAR, B.HireDate)

Select A.ProductID, A.Discount, B.ProductID, B.Discount from dbo.Order Details as A INNER JOIN dbo.Order Details as B ON A.Discount = B.Discount

```
SELECT A.column_name, B.column_name
FROM table_name AS A, table_name AS B
WHERE condition;
```

SUBQUERY: uma query dentro de outra que é utilizada para algum tipo de comparação.

select * from Production.Product where ListPrice > (select AVG(ListPrice) from Production.Product)

SELECT * from Person.Address where StateProvinceID in ( SELECT StateProvinceID from person.StateProvince WHERE NAME = 'Alberta')

DATEPART: saber informações relevantes de datas.

SELECT SalesOrderId, DATEPART(year,  OrderDate) as 'Mês' FROM Sales.SalesOrderHeader

SELECT AVG(TotalDue) as Media, DATEPART(month,  OrderDate) as 'Mês' FROM Sales.SalesOrderHeader GROUP BY DATEPART(month,  OrderDate)

OFFSET: serve para ignorar as primeiras x linhas de retorno e pode ser combinado com o LIMIT

Por exemplo: Gostaria de pegar os o segundo melhor funcionário em questão de salário

select e.name from Employee as e order by e.salary Offset 1 limit 1



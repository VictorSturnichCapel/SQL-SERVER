# 📚 Resumo de Estudo: SQL Server e SQL

## 🎯 Conceitos Iniciais

- **SQL Server**: Servidor que gerencia bancos de dados relacionais.
- **SQL Server Management Studio (SSMS)**: Interface para interagir com o SQL Server.
- **Conexão no SSMS**:
  - Database Engine
  - Server Name: `localhost\SQLEXPRESS`
- **Restaurar Banco de Dados**:
  - SSMS → Databases → Botão direito → *Restore Database*

---

## 🧾 Comandos SQL Básicos

### SELECT
- Seleciona dados do banco.
```sql
SELECT FirstName, LastName FROM Person.Person;
```

### DISTINCT
- Remove duplicatas.
```sql
SELECT DISTINCT FirstName FROM Person.Person;
```

### WHERE
- Filtra registros com condições:
  - `=`, `>`, `<`, `>=`, `<=`, `<>`
  - `AND`, `OR`
```sql
SELECT * FROM Person.Person WHERE LastName = 'miller' AND FirstName = 'anna';
```

---

## 🔍 Filtros Avançados

### BETWEEN
```sql
SELECT * FROM Production.Product WHERE ListPrice BETWEEN 1000 AND 1500;
```

### NOT BETWEEN
```sql
SELECT * FROM Production.Product WHERE ListPrice NOT BETWEEN 1000 AND 1500;
```

### IN
```sql
SELECT * FROM Person.Person WHERE BusinessEntityID IN (2, 7, 13);
```

### LIKE
```sql
SELECT * FROM Person.Person WHERE FirstName LIKE 'ovi%';
```

---

## 🔢 Funções de Agregação

- `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`

```sql
SELECT COUNT(title) FROM Person.Person;
SELECT SUM(LineTotal) FROM Sales.SalesOrderDetail;
```

---

## 📊 Agrupamento e Ordenação

### GROUP BY
```sql
SELECT Color, AVG(ListPrice) AS Media FROM Production.Product GROUP BY Color;
```

### HAVING
```sql
SELECT ProductID, SUM(LineTotal) AS Total 
FROM Sales.SalesOrderDetail 
GROUP BY ProductID 
HAVING SUM(LineTotal) >= 162000;
```

### ORDER BY & TOP
```sql
SELECT TOP 10 * FROM Production.Product ORDER BY ListPrice DESC;
```

---

## 🔗 Joins

### INNER JOIN
```sql
SELECT p.BusinessEntityID, p.FirstName, p.LastName, pe.EmailAddress 
FROM Person.Person p 
INNER JOIN Person.EmailAddress pe ON p.BusinessEntityID = pe.BusinessEntityID;
```

### LEFT JOIN / RIGHT JOIN
```sql
SELECT * FROM Person.Person pp 
LEFT JOIN Sales.PersonCreditCard pc ON pp.BusinessEntityID = pc.BusinessEntityID;
```

### SELF JOIN
```sql
SELECT A.ContactName, B.ContactName 
FROM Customers AS A 
INNER JOIN Customers AS B ON A.Region = B.Region;
```

---

## 🧬 UNION e Subqueries

### UNION / UNION ALL
```sql
SELECT ProductID, Name FROM Production.Product WHERE Name LIKE '%CHAIN%'
UNION
SELECT ProductID, Name FROM Production.Product WHERE Name LIKE '%Decal%';
```

### Subquery
```sql
SELECT * FROM Production.Product 
WHERE ListPrice > (SELECT AVG(ListPrice) FROM Production.Product);
```

---

## 🧠 Desafios Práticos

> Diversos desafios utilizando `SELECT`, `COUNT`, `GROUP BY`, `JOIN`, `HAVING`, `LIKE`, `IN`, entre outros. (Consultar lista completa para prática!)

---


## Relational model

The relational model for database management is an approach to managing data using a structure and language consistent with first-order predicate logic, first described in 1969 by Edgar F. Codd, where all data is represented in terms of tuples, grouped into relations. A database organized in terms of the relational model is a relational database.

The purpose of the relational model is to provide a declarative method for specifying data and queries: users directly state what information the database contains and what information they want from it, and let the database management system software take care of describing data structures for storing the data and retrieval procedures for answering queries.

Most relational databases use the SQL data definition and query language; these systems implement what can be regarded as an engineering approximation to the relational model. A table in an SQL database schema corresponds to a predicate variable; the contents of a table to a relation; key constraints, other constraints, and SQL queries correspond to predicates. However, SQL databases deviate from the relational model in many details, and Codd fiercely argued against deviations that compromise the original principles. In relational data model the data is organized into tables. These tables are called relations.

### Key Concepts  

* **Schema** - structural description of relations in database.
* **Instance** - actual contents at given point in time.
* **Database** - set of named relations (or tables).
* Each relation has a set of named **attributes** (or **columns**)
* Each **tuple** (or **row**) has a value for each attribute
* Each attribute has a **type** (or **domain**)
* **NULL** – special value for “unknown” or “undefined”
* Key – attribute whose value is unique in each tuple. Or set of attributes whose combined values are unique

![relational-model](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/relational_model.png)

### Advantages of relational databases

* **Query flexibility.** As long as your schema is normalized, you don’t have to know up front how you will query your data. You can always gather together the data you want using joins, views, filter and indexes.
* **Consistency via ACID transactions.** The relational database ensures that your commits are always atomic, consistent, isolated and durable. If an error occurrs, the whole transaction can be rolled back, restoring a consistent state. This is critical in some domains (e.g. banking).
* **Safety due to defined schema and strict constraint checks** (e.g. column types, uniqueness constraints, referential integrity). Your data has a fixed structure you can rely on. You cannot accidentally misspell a column name, submit a string instead of an integer or enter a non-existing foreign key. The relational database will refuse the query and tell you. This is very comfortable. However, data validation and constraint checking can also (and often must) be done in the application or user interface layer. Validating data only in the database is often too late. Usually the user’s input has to be checked at a upstream layer anyway. Moreover, complex business validation cannot be done by the database. Hence, it is questionable if a redundant check done by the database is really necessary (extra maintenance effort and performance hit).
* **Maturity.** 45+ years of industry experience leading to mature databases, tools, driver, programming libraries, ORM. Knowledge of RDBMS is a basic skill every software developer has.
* **Huge toolkit** (trigger, stored procedures, advanced indexes, views) available.

### Disadvantages of relational databases

* Impedance mismatch between the object-oriented and the relational world.
* The relational data model doesn’t fit in with every domain.
* Difficult schema evolution due to an inflexible data model.
* Weak distributed availability due to poor horizontal scalability.
* Performance hit due to joins, ACID transactions and strict consistency constraints (especially in distributed environments).

[Great article about pros and cons of relational databases](https://blog.philipphauer.de/relational-databases-strength-weaknesses-mongodb/)


## Relational algebra

Relational algebra, first created by Edgar F. Codd while at IBM, is a family of algebras with a well-founded semantics used for modelling the data stored in relational databases, and defining queries on it.

The main application of relational algebra is providing a theoretical foundation for relational databases, particularly query languages for such databases, chief among which is SQL.

### Relational algebra operations

For understanding it is important to remember that the **result of any operation of algebra over relations is another relationship**, which can then also be used in other operations.

**Selection (σ)** 

Selection operator is used to select tuples (rows) from a relation based on some condition. 

```
σ (Cond)(Relation Name)
```

Extract students whose age is greater than 18 from STUDENT relation

```
σ (AGE>18)(STUDENT)
```

**Projection (∏)**

A projection is an operation where only attributes from the specified domains are selected from the relation, that is, only the necessary columns are selected from the table, and if several identical tuples are obtained, then in the resulting relation there is only one copy of such a tuple.

```
∏(Column 1,Column 2….Column n)(Relation Name)
```

Extract ID and NAME columns from STUDENT relation

```
∏(ID,NAME)(STUDENT)
```

**Cross Product(X)**

Cross product is used to join two relations. For every row of Relation1, each row of Relation2 is concatenated. If Relation1 has m tuples and and Relation2 has n tuples, cross product of Relation1 and Relation2 will have m X n tuples.

```
Relation1 X Relation2
```
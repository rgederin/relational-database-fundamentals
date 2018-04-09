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

### Basic Relational algebra operations

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

**Cross Product (X)**

Cross product (Cartesian Product) is used to join two relations. For every row of Relation1, each row of Relation2 is concatenated. If Relation1 has m tuples and and Relation2 has n tuples, cross product of Relation1 and Relation2 will have m X n tuples.

```
Relation1 X Relation2
```

**Union (U)** 

Union on two relations R1 and R2 can only be computed if R1 and R2 are union compatible (These two relation should have same number of attributes and corresponding attributes in two relations have same domain) . Union operator when applied on two relations R1 and R2 will give a relation with tuples which are either in R1 or in R2. The tuples which are in both R1 and R2 will appear only once in result relation.

```
Relation1 U Relation2
```

**Minus (-)**

Minus on two relations R1 and R2 can only be computed if R1 and R2 are union compatible. Minus operator when applied on two relations as R1-R2 will give a relation with tuples which are in R1 but not in R2.

```
Relation1 - Relation2
```

**Rename (ρ)**
 
Rename operator is used to give another name to a relation. To rename STUDENT relation to STUDENT1, we can use rename operator like:

```
ρ(STUDENT1, STUDENT)
```

#### Extended Relational algebra operations

Extended operators are those operators which can be derived from basic operators.There are mainly three types of extended operators in Relational Algebra:

* Join
* Intersection
* Divide 

**Intersection (∩)** 

Intersection on two relations R1 and R2 can only be computed if R1 and R2 are union compatible (These two relation should have same number of attributes and corresponding attributes in two relations have same domain). Intersection operator when applied on two relations as R1∩R2 will give a relation with tuples which are in R1 as well as R2

```
Example: Find a person who is student as well as employee -  STUDENT ∩ EMPLOYE
```

**Conditional Join (⋈c)** 

Conditional Join is used when you want to join two or more relation based on some conditions. Example: Select students whose ROLL_NO is greater than EMP_NO of employees

**Equijoin (⋈)**
 
Equijoin is a special case of conditional join where only equality condition holds between a pair of attributes. As values of two attributes will be equal in result of equijoin, only one attribute will be appeared in result.

**Natural Join (⋈)**
 
It is a special case of equijoin in which equality condition hold on all attributes which have same name in relations R and S (relations on which join operation is applied). While applying natural join on two relations, there is no need to write equality condition explicitly. Natural Join will also return the similar attributes only once as their value will be same in resulting relation.

Example: Select students whose ROLL_NO is equal to ROLL_NO of STUDENT_SPORTS 

Natural Join is by default inner join because the tuples which does not satisfy the conditions of join does not appear in result set. e.g.; The tuple having ROLL_NO 3 in STUDENT does not match with any tuple in STUDENT_SPORTS, so it has not been a part of result set.

**Left Outer Join (⟕)** 

When applying join on two relations R and S, some tuples of R or S does not appear in result set which does not satisfy the join conditions. But Left Outer Joins gives all tuples of R in the result set. The tuples of R which do not satisfy join condition will have values as NULL for attributes of S.

**Right Outer Join (⟖)**

When applying join on two relations R and S, some tuples of R or S does not appear in result set which does not satisfy the join conditions. But Right Outer Joins gives all tuples of S in the result set. The tuples of S which do not satisfy join condition will have values as NULL for attributes of R.

**Full Outer Join (⟗)** 

When applying join on two relations R and S, some tuples of R or S does not appear in result set which does not satisfy the join conditions. But Full Outer Joins gives all tuples of S and all tuples of R in the result set. The tuples of S which do not satisfy join condition will have values as NULL for attributes of R and vice versa.

**Division Operator (÷)** 

Division operator A÷B can be applied if and only if:

* Attributes of B is proper subset of Attributes of A.
* The relation returned by division operator will have attributes = (All attributes of A – All Attributes of B)
* The relation returned by division operator will return those tuples from relation A which are associated to every B’s tuple.

![sql](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/sql.jpg)

## Structured Query Language (SQL)

Structured Query Language is a standard Database language which is used to create, maintain and retrieve the relational database.

All SQL commands could be separated as Data Definition Language, Data Manipulation Language, Transaction Control Language and Data Control Language.

![sql](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/sql-commands.jpg)


**Data Definition Language (DDL)** is used to define database structure or schema. DDL is also used to specify additional properties of the data. The storage structure and access methods used by the database system by a set of statements in a special type of DDL called a data storage and definition language. These statements defines the implementation details of the database schema, which are usually hidden from the users. The data values stored in the database must satisfy certain consistency constraints.

```
CREATE : to create objects in database
ALTER : alters the structure of database
DROP : delete objects from database
RENAME : rename an objects
```

**Data Manipulation Language (DML)**  used for managing data with in schema objects

```
SELECT : retrieve data from the database
INSERT : insert data into a table
UPDATE : update existing data within a table
DELETE : deletes all records from a table , space for the records remain
```

**Transaction Control Language (TCL)** commands are used to manage transactions in database. These are used to manage the changes made by DML-statements. It also allows statements to be grouped together into logical transactions.

```
COMMIT :    Commit command is used to permanently save any transaction
            into database.
ROLLBACK :  This command restores the database to last committed state.
            It is also use with savepoint command to jump to a savepoint
            in a transaction.
SAVEPOINT : Savepoint command is used to temporarily save a transaction so
            that you can rollback to that point whenever necessary.
```

**Data Control Language (DCL)** is a syntax similar to a computer programming language used to control access to data stored in a database (Authorization). In particular, it is a component of Structured Query Language (SQL).

```
GRANT : allow specified users to perform specified tasks.
REVOKE : cancel previously granted or denied permissions.
```

## SQL examples

For all examples I will use next database which consists of 3 tables:

```
College(cName,state,enrollment) 
Student(sID,sName,GPA,sizeHS)
Apply(sID,cName,major,decision)
```

We have the college relation: college relation contains information about the name of the colleges, the state, and the enrollment of those colleges.
We have the student relation, which contains student IDs, their names,their GPA, and the size of the high school that they come from.
And finally, the application information, that tells us that a particular student applied to a particular college for a particular major and there was a decision of that application

![sql](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/db-str.png)

### Basic select

IDs, names, and GPAs of students with GPA > 3.6:

```
select sID, sName, GPA
from Student
where GPA > 3.6;
```

Student names and majors for which they've applied - output will contains duplicates:

```
select sName, major
from Student, Apply
where Student.sID = Apply.sID;
```

Same query with **distinct** statement for removing duplicates:

```
select distinct sName, major
from Student, Apply
where Student.sID = Apply.sID;
```

Names and GPAs of students with sizeHS < 1000 applying to CS at Stanford, and the application decision:

```
select sname, GPA, decision
from Student, Apply
where Student.sID = Apply.sID
  and sizeHS < 1000 and major = 'CS' and cname = 'Stanford';
```

All large campuses with CS applicants - using name of relations for solving ambiguous column names:

```
select distinct College.cName
from College, Apply
where College.cName = Apply.cName
  and enrollment > 20000 and major = 'CS';
```

Application information (cross product for all three relations):

```
select Student.sID, sName, GPA, Apply.cName, enrollment
from Student, College, Apply
where Apply.sID = Student.sID and Apply.cName = College.cName;

```

Sort by decreasing GPA - using **order by** keyword and specifying descening order (**desc**):

```
select Student.sID, sName, GPA, Apply.cName, enrollment
from Student, College, Apply
where Apply.sID = Student.sID and Apply.cName = College.cName
order by GPA desc;
```

We could have several sorting in one querry:

```
select Student.sID, sName, GPA, Apply.cName, enrollment
from Student, College, Apply
where Apply.sID = Student.sID and Apply.cName = College.cName
order by GPA desc, enrollment;
```

Using **like** predicate - querry will return such majors like biology, marin biology, etc : 

```
select sID, major
from Apply
where major like '%bio%';

```

Add scaled GPA based on sizeHS:

```
select sID, sName, GPA, sizeHS, GPA*(sizeHS/1000.0)
from Student;
```

Rename result attribute (using **as**):

```
select sID, sName, GPA, sizeHS, GPA*(sizeHS/1000.0) as scaledGPA
from Student;
```

### Table Variables and Set Operators

Application information using table variables for increasing readability:

```
select S.sID, S.sName, S.GPA, A.cName, C.enrollment
from Student S, College C, Apply A
where A.sID = S.sID and A.cName = C.cName;
```

Pairs of students with same GPA without self-pairings and reverse-pairings:

```
select S1.sID, S1.sName, S1.GPA, S2.sID, S2.sName, S2.GPA
from Student S1, Student S2
where S1.GPA = S2.GPA and S1.sID < S2.sID;
```

List of college names and student names - using **union** operator (without duplicates, **union all** will leave duplicates):

```
select cName as name from College
union
select sName as name from Student;
```

IDs of students who applied to both CS and EE - using **intersection** operator:

```
select sID from Apply where major = 'CS'
intersect
select sID from Apply where major = 'EE';
```

IDs of students who applied to CS but not EE - using **except** operator:

```
select sID from Apply where major = 'CS'
except
select sID from Apply where major = 'EE';
```


### Subqueries in WHERE

Sub-queries are nested, select statements within the condition.

IDs and names of students applying to CS:

```
select sID, sName
from Student
where sID in (select sID from Apply where major = 'CS');
```

Students who applied to CS but not EE (query we used 'Except' for earlier):

```
select sID, sName
from Student
where sID in (select sID from Apply where major = 'CS')
  and sID not in (select sID from Apply where major = 'EE');
```
# Relational model

The relational model for database management is an approach to managing data using a structure and language consistent with first-order predicate logic, first described in 1969 by Edgar F. Codd, where all data is represented in terms of tuples, grouped into relations. A database organized in terms of the relational model is a relational database.

The purpose of the relational model is to provide a declarative method for specifying data and queries: users directly state what information the database contains and what information they want from it, and let the database management system software take care of describing data structures for storing the data and retrieval procedures for answering queries.

Most relational databases use the SQL data definition and query language; these systems implement what can be regarded as an engineering approximation to the relational model. A table in an SQL database schema corresponds to a predicate variable; the contents of a table to a relation; key constraints, other constraints, and SQL queries correspond to predicates. However, SQL databases deviate from the relational model in many details, and Codd fiercely argued against deviations that compromise the original principles. In relational data model the data is organized into tables. These tables are called relations.

## Key Concepts  

* **Schema** - structural description of relations in database.
* **Instance** - actual contents at given point in time.
* **Database** - set of named relations (or tables).
* Each relation has a set of named **attributes** (or **columns**)
* Each **tuple** (or **row**) has a value for each attribute
* Each attribute has a **type** (or **domain**)
* **NULL** – special value for “unknown” or “undefined”
* Key – attribute whose value is unique in each tuple. Or set of attributes whose combined values are unique

![relational-model](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/relational_model.png)

## Advantages of relational databases

* **Query flexibility.** As long as your schema is normalized, you don’t have to know up front how you will query your data. You can always gather together the data you want using joins, views, filter and indexes.
* **Consistency via ACID transactions.** The relational database ensures that your commits are always atomic, consistent, isolated and durable. If an error occurrs, the whole transaction can be rolled back, restoring a consistent state. This is critical in some domains (e.g. banking).
* **Safety due to defined schema and strict constraint checks** (e.g. column types, uniqueness constraints, referential integrity). Your data has a fixed structure you can rely on. You cannot accidentally misspell a column name, submit a string instead of an integer or enter a non-existing foreign key. The relational database will refuse the query and tell you. This is very comfortable. However, data validation and constraint checking can also (and often must) be done in the application or user interface layer. Validating data only in the database is often too late. Usually the user’s input has to be checked at a upstream layer anyway. Moreover, complex business validation cannot be done by the database. Hence, it is questionable if a redundant check done by the database is really necessary (extra maintenance effort and performance hit).
* **Maturity.** 45+ years of industry experience leading to mature databases, tools, driver, programming libraries, ORM. Knowledge of RDBMS is a basic skill every software developer has.
* **Huge toolkit** (trigger, stored procedures, advanced indexes, views) available.

## Disadvantages of relational databases

* Impedance mismatch between the object-oriented and the relational world.
* The relational data model doesn’t fit in with every domain.
* Difficult schema evolution due to an inflexible data model.
* Weak distributed availability due to poor horizontal scalability.
* Performance hit due to joins, ACID transactions and strict consistency constraints (especially in distributed environments).

[Great article about pros and cons of relational databases](https://blog.philipphauer.de/relational-databases-strength-weaknesses-mongodb/)


# Relational algebra

Relational algebra, first created by Edgar F. Codd while at IBM, is a family of algebras with a well-founded semantics used for modelling the data stored in relational databases, and defining queries on it.

The main application of relational algebra is providing a theoretical foundation for relational databases, particularly query languages for such databases, chief among which is SQL.

## Basic Relational algebra operations

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

## Extended Relational algebra operations

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

# Structured Query Language (SQL)

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

# SQL examples

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

## Basic select

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

## Table Variables and Set Operators

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


## Subqueries

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

Colleges such that some other college is in the same state (like Berkeley and Stanford in the same state):

```
select cName, state
from College C1
where exists (select * from College C2
              where C2.state = C1.state and C2.cName <> C1.cName);
```

Higher GPA than all other students:

```
select sName, GPA
from Student
where GPA >= all (select GPA from Student);
```

Students whose scaled GPA changes GPA by more than 1:

```
select *
from (select sID, sName, GPA, GPA*(sizeHS/1000.0) as scaledGPA
      from Student) G
where abs(scaledGPA - GPA) > 1.0;
```

## Aggregation functions

These are functions that will appear in the select clause initially and what they do is they perform computations over sets of values in multiple rows of our relations, and the basic aggregation functions supported by every SQL system are minimum, maximum, some, average and count.

Now once we've introduced the aggregation functions we can also add two new clasues to the SQL select from where statement, the **group by** and **having** clause.

The group by allows us to partition our relations into groups and then will compute aggregated aggregate functions over each group independently.
The having condition allows us to test filters on the results of aggregate values. The where condition applies to single rows at a time. The having condition will apply to the groups that we generate from the group by clause.


Average GPA of all students:

```
select avg(GPA)
from Student;
```

Lowest GPA of students applying to CS:

```
select min(GPA)
from Student, Apply
where Student.sID = Apply.sID and major = 'CS';
```

Number of colleges bigger than 15,000:

```
select count(*)
from College
where enrollment > 15000;
```

Number of applications to each college:

```
select cName, count(*)
from Apply
group by cName;
```

College enrollments by state:

```
select state, sum(enrollment)
from College
group by state;
```

Minimum + maximum GPAs of applicants to each college & major:

```
select cName, major, min(GPA), max(GPA)
from Student, Apply
where Student.sID = Apply.sID
group by cName, major;
```

Colleges with fewer than 5 applications:

```
select cName
from Apply
group by cName
having count(sID) < 5;
```

Majors whose applicant's maximum GPA is below the average:

```
select major
from Student, Apply
where Student.sID = Apply.sID
group by major
having max(GPA) < (select avg(GPA) from Student);
```

## Join Operators

Student names and majors for which they've applied

```
select distinct sName, major
from Student inner join Apply
on Student.sID = Apply.sID;
```

**Inner join** could be simplified to just **join**

```
select distinct sName, major
from Student join Apply
on Student.sID = Apply.sID;
```

Names and GPAs of students with sizeHS < 1000 applying to CS at Stanford

```
select sName, GPA
from Student join Apply
on Student.sID = Apply.sID
where sizeHS < 1000 and major = 'CS' and cName = 'Stanford';
```

THREE-WAY INNER JOIN - application info: ID, name, GPA, college name, enrollment

```
select Apply.sID, sName, GPA, Apply.cName, enrollment
from (Apply join Student on Apply.sID = Student.sID) join College on Apply.cName = College.cName;
```

NATURAL JOIN - student names and majors for which they've applied

```
select distinct sName, major
from Student natural join Apply;
```

NATURAL JOIN WITH ADDITIONAL CONDITIONS - Names and GPAs of students with sizeHS < 1000 applying to CS at Stanford

```
select sName, GPA
from Student natural join Apply
where sizeHS < 1000 and major = 'CS' and cName = 'Stanford';
```

USING clause considered safer 

```
select sName, GPA
from Student join Apply using(sID)
where sizeHS < 1000 and major = 'CS' and cName = 'Stanford';
```

SELF-JOIN - Pairs of students with same GPA

```
select S1.sID, S1.sName, S1.GPA, S2.sID, S2.sName, S2.GPA
from Student S1 join Student S2 using(GPA)
where S1.sID < S2.sID;
```

LEFT OUTER JOIN - student application info: name, ID, college name, major and Include students who haven't applied anywhere

```
select sName, sID, cName, major
from Student left outer join Apply using(sID);

select sName, sID, cName, major
from Student left join Apply using(sID);

select sName, sID, cName, major
from Student natural left outer join Apply;
```

RIGHT OUTER JOIN - student application info: name, ID, college name, major. Include applications without matching students

```
select sName, sID, cName, major
from Student natural right outer join Apply;
```

FULL OUTER JOIN - Student application info .Include students who haven't applied anywhere and applications without matching students

```
select sName, sID, cName, major
from Student full outer join Apply using(sID);
```

# Database normalization

Normalization is the process of splitting relations into well structured relations that allow users to insert, delete, and update tuples without introducing database inconsistencies. Without normalization many problems can occur when trying to load an integrated conceptual model into the DBMS. These problems arise from relations that are generated directly from user views are called anomalies. There are three types of anomalies: update, deletion and insertion anomalies.

## Anomalies

Relation which are using for anomalies examples

![sql](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/anomalies.png)

An **update anomaly** is a data inconsistency that results from data redundancy and a partial update. For example, each employee in a company has a department associated with them as well as the student group they participate in. 
If A. Bruchs’ department is an error it must be updated at least 2 times or there will be inconsistent data in the database. If the user performing the update does not realize the data is stored redundantly the update will not be done properly.

A **deletion anomaly** is the unintended loss of data due to deletion of other data. For example, if the student group Beta Alpha Psi disbanded and was deleted from the table above, J. Longfellow and the Accounting department would cease to exist. This results in database inconsistencies and is an example of how combining information that does not really belong together into one table can cause problems.

An **insertion anomaly** is the inability to add data to the database due to absence of other data. For example, assume Student_Group is defined so that null values are not allowed. If a new employee is hired but not immediately assigned to a Student_Group then this employee could not be entered into the database. This results in database inconsistencies due to omission.

Update, deletion, and insertion anomalies are very undesirable in any database. Anomalies are avoided by the process of normalization.

## Functional dependency

Functional Dependency is a constraint between two sets of attributes in a relation from a database. Functional dependency is denoted by arrow (→). If an attributed A functionally determines B, then it is written as A → B.

For example employee_id → name means employee_id functionally determines name of employee. As another example in a time table database, {student_id, time} → {lecture_room}, student ID and time determine the lecture room where student should be.

A function dependency A → B mean for all instances of a particular value of A, there is same value of B.

For example in the below table A → B is true, but B → A is not true as there are different values of A for B = 3.

```
A   B
-----
1   3
2   3
4   0
1   3
4   0
```

**Trivial Functional Dependency**

X –> Y is trivial only when Y is subset of X.

```
ABC --> AB
ABC --> A
ABC --> ABC
```

X –> Y is a **non trivial functional dependencies** when Y is not a subset of X.

X –> Y is called completely non-trivial when X intersect Y is NULL.

```
Id --> Name, 
Name --> DOB
```

## Normalization of relations. Normal forms
 
The process of designing a database using the NF method is iterative and consists in the sequential transformation of the relation from 1NF to NF of a higher order according to certain rules. 

Each next NF is limited to a certain type of functional dependencies and elimination of corresponding anomalies when performing operations on database relations, as well as preserving the properties of previous NFs

### 1 NF

If a relation contain composite or multi-valued attribute, it violates first normal form or a relation is in first normal form if it does not contain any composite or multi-valued attribute. A relation is in first normal form if every attribute in that relation is singled valued attribute.

Relation STUDENT in table 1 is not in 1NF because of multi-valued attribute STUD_PHONE. Its decomposition into 1NF has been shown in table 2.

![nf1](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/nf1.png)

### 2 NF

To be in second normal form, a relation must be in first normal form and relation must not contain any partial dependency. A relation is in 2NF iff it has No Partial Dependency, i.e., no non-prime attribute (attributes which are not part of any candidate key) is dependent on any proper subset of any candidate key of the table.

![nf2](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/nf2.png)

Partial Dependency – If proper subset of candidate key determines non-prime attribute, it is called partial dependency.

Example 1 – In relation STUDENT_COURSE given in Table 3,

```
FD set: {COURSE_NO->COURSE_NAME}
Candidate Key: {STUD_NO, COURSE_NO}
```

In FD COURSE_NO->COURSE_NAME, COURSE_NO (proper subset of candidate key) is determining COURSE_NAME (non-prime attribute). Hence, it is partial dependency and relation is not in second normal form.

To convert it to second normal form, we will decompose the relation STUDENT_COURSE (STUD_NO, COURSE_NO, COURSE_NAME) as :

```
STUDENT_COURSE (STUD_NO, COURSE_NO)
COURSE (COURSE_NO, COURSE_NAME)
```

### 3 NF

The relation is in 3NF when it is in 2NF and each non-key attribute is not reliantly (non trasitively) dependent on the primary key. Simply put, the second rule requires you to move all non-key fields whose contents can relate to several table entries in separate tables.

# Transactions

A transaction is a single logical unit of work which accesses and possibly modifies the contents of a database. Transactions access data using read and write operations.

In order to maintain consistency in a database, before and after transaction, certain properties are followed. These are called **ACID properties**.

The ACID properties, in totality, provide a mechanism to ensure correctness and consistency of a database in a way such that each transaction is a group of operations that acts a single unit, produces consistent results, acts in isolation from other operations and updates that it makes are durably stored.

## ACID

**Atomicity**

This property means that either the entire transaction takes place at once or doesn’t happen at all. There is no midway i.e. transactions do not occur partially. Each transaction is considered as one unit and either runs to completion or is not executed at all. It involves following two operations.

* Abort: If a transaction aborts, changes made to database are not visible.
* Commit: If a transaction commits, changes made are visible.

Atomicity is also known as the **‘All or nothing rule’**.

**Consistency**

Consistency in database systems refers to the requirement that any given database transaction must change affected data only in allowed ways. Any data written to the database must be valid according to all defined rules, including constraints, cascades, triggers, and any combination thereof.

This means that integrity constraints must be maintained so that the database is consistent before and after the transaction. It refers to correctness of a database. 

**Isolation**

This property ensures that multiple transactions can occur concurrently without leading to inconsistency of database state. Transactions occur independently without interference. Changes occurring in a particular transaction will not be visible to any other transaction until that particular change in that transaction is written to memory or has been committed. This property ensures that the execution of transactions concurrently will result in a state that is equivalent to a state achieved these were executed serially in some order.

**Durability**

In database systems, durability is the ACID property which guarantees that transactions that have committed will survive permanently. For example, if a flight booking reports that a seat has successfully been booked, then the seat will remain booked even if the system crashes.

Durability can be achieved by flushing the transaction's log records to non-volatile storage before acknowledging commitment.

In distributed transactions, all participating servers must coordinate before commit can be acknowledged. This is usually done by a two-phase commit protocol.

Many DBMSs implement durability by writing transactions into a transaction log that can be reprocessed to recreate the system state right before any later failure. A transaction is deemed committed only after it is entered in the log.

## Transaction phenomenas/problems

There are 4 phenomenas/problems

* Lost update
* Dirty read
* Non-repeatebale read
* Phantom read

### Lost update

If two transactions are updating different columns of the same row, then there is no conflict. The second update blocks until the first transaction is committed and the final result reflects both update changes.

If the two transactions want to change the same columns, the second transaction will overwrite the first one, therefore losing the first transaction update.

So an update is lost when a user overrides the current database state without realizing that someone else changed it between the moment of data loading and the moment the update occurs.

![lost](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/lost.png)

### Dirty read

A dirty read occurs when a transaction reads data that has not yet been committed. For example, suppose transaction 1 updates a row. Transaction 2 reads the updated row before transaction 1 commits the update. If transaction 1 rolls back the change, transaction 2 will have read data that is considered never to have existed.

![lost](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/dirty.png)

### Non-repeatable reads

A nonrepeatable read occurs when a transaction reads the same row twice but gets different data each time. For example, suppose transaction 1 reads a row. Transaction 2 updates or deletes that row and commits the update or delete. If transaction 1 rereads the row, it retrieves different row values or discovers that the row has been deleted.

![lost](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/non-rep.png)

### Phantom read

A phantom is a row that matches the search criteria but is not initially seen. For example, suppose transaction 1 reads a set of rows that satisfy some search criteria. Transaction 2 generates a new row (through either an update or an insert) that matches the search criteria for transaction 1. If transaction 1 reexecutes the statement that reads the rows, it gets a different set of rows.

![lost](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/phantom.png)

## Isolation levels

Most DBMSs offer a number of transaction isolation levels, which control the degree of locking that occurs when selecting data. For many database applications, the majority of database transactions can be constructed to avoid requiring high isolation levels (e.g. SERIALIZABLE level), thus reducing the locking overhead for the system. The programmer must carefully analyze database access code to ensure that any relaxation of isolation does not cause software bugs that are difficult to find. Conversely, if higher isolation levels are used, the possibility of deadlock is increased, which also requires careful analysis and programming techniques to avoid.

The isolation levels defined by the ANSI/ISO SQL standard are listed as follows.

### Read uncommitted

This is the lowest isolation level. In this level, dirty reads are allowed, so one transaction may see not-yet-committed changes made by other transactions.

### Read committed

In this isolation level, a lock-based concurrency control DBMS implementation keeps write locks (acquired on selected data) until the end of the transaction, but read locks are released as soon as the SELECT operation is performed (so the non-repeatable reads phenomenon can occur in this isolation level).

Putting it in simpler words, read committed is an isolation level that guarantees that any data read is committed at the moment it is read. It simply restricts the reader from seeing any intermediate, uncommitted, 'dirty' read. It makes no promise whatsoever that if the transaction re-issues the read, it will find the same data; data is free to change after it is read.

### Repeatable read

In this isolation level, a lock-based concurrency control DBMS implementation keeps read and write locks (acquired on selected data) until the end of the transaction.

Write skew is possible at this isolation level, a phenomenon where two writes are allowed to the same column(s) in a table by two different writers (who have previously read the columns they are updating), resulting in the column having data that is a mix of the two transactions.

### Serializable

This is the highest isolation level.

With a lock-based concurrency control DBMS implementation, serializability requires read and write locks (acquired on selected data) to be released at the end of the transaction. Also range-locks must be acquired when a SELECT query uses a ranged WHERE clause, especially to avoid the phantom reads phenomenon.

When using non-lock based concurrency control, no locks are acquired; however, if the system detects a write collision among several concurrent transactions, only one of them is allowed to commit. See snapshot isolation for more details on this topic.

![lost](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/isolation.png)

# Indexes

An index is a data structure that optimize searching and accessing the data. It’s like an index at the back of a book. When your database start to grow, the performance will be a concern. Hence, getting directly to a specific row in a large table in the least possible time is a priority.

One of the ways that will optimize your database searching and accessing is having indexes on the columns that you usually access the table using it.

What the DBMS will do when you ask for a specific row, it will go sequentially and check with every row; “Is this the row that I need?”, If yes return it, if no, keep searching till the end.

But, we have a better way to do that. An index, as we’ve mentioned, is a data structure, it won’t be obvious for you, but it’s stored inside the DBMS, most commonly as a B, B+ trees or hash tables.

**By default, Most of the DBMS automatically create an index on primary and unique columns.**

## How Indexes Work

Let’s say that you have an index for a primary key. This will create an ordered list of primary key values in a separate table, each entry has a pointer points to the relative value in the original table.

So, whenever you want to access a table using the primary key, it will use binary search algorithm (takes time of O(LogN)) to access the required value in the Index table, and then, go to the relative value in the original table.

![index](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/index.png)

And, definitely, you can create another index on another column, even if it’s a non-primary column, like first name, assuming that you usually access the table using that column.

The decision for choosing another column (besides the primary key) to be indexed-ed can be delayed until the database has been used for a while. This is because we want to know how users are really using our database, and what kind of queries they’re running rather than how we hoped or thought.

## Composit index

You can also create an index on a combination of columns, meaning if you often access the table using the first name, and last name, you can create an index on both, the first name and last name.

Now, the Index table will be sorted according to the first name, and for each value of the first name it will be sorted according to the last name.

When you access the data, It’s more efficient to specify the columns in the right order as in the index definition. So, here, it should be first name, then last name, and not the vice-versa.

## Clustered & Non-Clustered Indexes

A table can have only one clustered index, while it can have more than one non-clustered index.

**Clustered index**

Every table can have one and only one clustered index. The most common clustered index in any database table is the primary key column.

The database will then order the data in the table based on the clustered index; no Index table need to be created. The binary search algorithm will be used to get to the required data in the table (already ordered).

**Non-Clustered index**

If you found yourself often also accessing the data using another column, we can create a secondary index; a non-clustered index.

Let’s say we want to create a secondary index for the last name, while the clustered index is the employee id. It’s created in a separate table, it has two columns, one for the last name, and one for the corresponding employee id.

The created table is now sorted by last name, the way that we can’t actually do in the employee table, because we’re already sorted by the employee id.

Now it’s not as quick as using the clustered index. Why? We still need to read from the table created for secondary index then jump to the employee table to get to a specific employee. But, it’s much quicker than a full table scan.

![clustered](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/clustered.png)

## Advantages/Disadvantages of using indexes

**Advantages**

* Speed up SELECT query
* Helps to make a row unique or without duplicates(primary,unique) 
* If index is set to fill-text index, then we can search against large string values. for example to find a word from a sentence etc.

**Disadvantages**

* Indexes take additional disk space.
* Indexes slow down INSERT,UPDATE and DELETE, but will speed up UPDATE if the WHERE condition has an indexed field.  INSERT, UPDATE and DELETE becomes slower because on each operation the indexes must also be updated. 

## Implementation

As we mentioned previously in the SQL tutorial, DDL operations manage table and index structure. That is, we can CREATE, ALTER, or DROP an index.

The syntax to create and delete indexes varies among different databases. Therefore, you need to check the syntax for creating indexes in your database. We’ll use MySQL to get an idea on how they can be created, and deleted.

**CREATE**

There are two ways to create an index, either when creating a table, or using the CREATE INDEX statement.

```
-- Create an index in CREATE TABLE (duplicate values are allowed)
CREATE TABLE books (
    title VARCHAR(255),
    INDEX index_name (title)
);

-- Create an index in CREATE TABLE (duplicate values aren't allowed)
CREATE TABLE books (
    title VARCHAR(255),
    UNIQUE INDEX index_name (title)
);

-- Create an index (duplicate values are allowed)
CREATE INDEX index_name ON table_name (column_name);

-- Create a unique index (duplicate values aren't allowed)
CREATE UNIQUE INDEX index_name ON table_name (column_name);
```

The CREATE INDEX statement is mapped to an ALTER TABLE statement to create indexes.

If you want to create an index on a combination of columns, you can list the column names within the parentheses, separated by commas.

```
CREATE INDEX index_name ON table_name (column_A, column_B, ...);
```

The index table will be sorted on column A, then with A, there would be the B’s in order as well. So, It’s more efficient to specify the columns in the order as in the index definition to speed up queries on the table.

**ALTER**

The ALTER TABLE statement changes the structure of a table. One example is to create or destroy indexes.

```
-- Add an index to existing table
ALTER TABLE tbl_name ADD INDEX index_name (col_name);

-- Add a unique (no duplicates) index to existing table
ALTER TABLE tbl_name ADD UNIQUE INDEX index_name (col_name);

-- Delete an index in an existing table
ALTER TABLE tbl_name DROP INDEX index_name;
```

**DROP**

The DROP INDEX statement deletes an index a table. The DROP INDEX statement is mapped to an ALTER TABLE statement to drop the index. 

```
DROP INDEX index_name ON tbl_name;
```

# SQL Constraints

SQL constraints are used to specify rules for the data in a table.

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

Constraints can be column level or table level. Column level constraints apply to a column, and table level constraints apply to the whole table.

The following constraints are commonly used in SQL:

* NOT NULL - Ensures that a column cannot have a NULL value
* UNIQUE - Ensures that all values in a column are different
* PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* FOREIGN KEY - Uniquely identifies a row/record in another table
* CHECK - Ensures that all values in a column satisfies a specific condition
* DEFAULT - Sets a default value for a column when no value is specified

SQL snippets below adopted for MySQL

### NOT NULL Constraint

By default, a column can hold NULL values.

The NOT NULL constraint enforces a column to NOT accept NULL values.

This enforces a field to always contain a value, which means that you cannot insert a new record, or update a record without adding a value to this field.

The following SQL ensures that the "ID", "LastName", and "FirstName" columns will NOT accept NULL values:

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

### UNIQUE Constraint

The UNIQUE constraint ensures that all values in a column are different.

Both the UNIQUE and PRIMARY KEY constraints provide a guarantee for uniqueness for a column or set of columns.

A PRIMARY KEY constraint automatically has a UNIQUE constraint.

However, you can have many UNIQUE constraints per table, but only one PRIMARY KEY constraint per table.

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    UNIQUE (ID)
);
```

To name a UNIQUE constraint, and to define a UNIQUE constraint on multiple columns, use the following SQL syntax:

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
);
```

### PRIMARY KEY Constraint

The PRIMARY KEY constraint uniquely identifies each record in a database table.

Primary keys must contain UNIQUE values, and cannot contain NULL values.

A table can have only one primary key, which may consist of single or multiple fields.

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID)
);
```

To allow naming of a PRIMARY KEY constraint, and for defining a PRIMARY KEY constraint on multiple columns, use the following SQL syntax:

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
);
```

### FOREIGN KEY Constraint

A FOREIGN KEY is a key used to link two tables together.

A FOREIGN KEY is a field (or collection of fields) in one table that refers to the PRIMARY KEY in another table.

The table containing the foreign key is called the child table, and the table containing the candidate key is called the referenced or parent table.

Look at the following two tables:

"Persons" table:

![clustered](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/persons.png)

"Orders" table:

![clustered](https://github.com/rgederin/relational-database-fundamentals/blob/master/img/orders.png)

Notice that the "PersonID" column in the "Orders" table points to the "PersonID" column in the "Persons" table.

The "PersonID" column in the "Persons" table is the PRIMARY KEY in the "Persons" table.

The "PersonID" column in the "Orders" table is a FOREIGN KEY in the "Orders" table.

The FOREIGN KEY constraint is used to prevent actions that would destroy links between tables.

The FOREIGN KEY constraint also prevents invalid data from being inserted into the foreign key column, because it has to be one of the values contained in the table it points to.

### CHECK Constraint

The CHECK constraint is used to limit the value range that can be placed in a column.

If you define a CHECK constraint on a single column it allows only certain values for this column.

If you define a CHECK constraint on a table it can limit the values in certain columns based on values in other columns in the row.

```
CHECK constraint on the "Age" column when the "Persons" table is created. The CHECK constraint ensures that you can not have any person below 18 years:

CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);

To create a CHECK constraint on the "Age" column when the table is already created, use the following SQL:

ALTER TABLE Persons
ADD CHECK (Age>=18);

ALTER TABLE Persons
ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');

Drop check

ALTER TABLE Persons
DROP CHECK CHK_PersonAge;
```

### DEFAULT Constraint

The DEFAULT constraint is used to provide a default value for a column.
  
The default value will be added to all new records IF no other value is specified.

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);

ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';

ALTER TABLE Persons
ALTER City DROP DEFAULT;
```

# Triggers

A database trigger is procedural code that is automatically executed in response to certain events on a particular table or view in a database. The trigger is mostly used for maintaining the integrity of the information on the database. For example, when a new record (representing a new worker) is added to the employees table, new records should also be created in the tables of the taxes, vacations and salaries. Triggers can also be used to log historical data, for example to keep track of employees' previous salaries.

Triggers are event-condition-action rules.

They specify that whenever a certain type of event occurs in the database, check the condition over the database and if it's true execute an action automatically.

Triggers can be written for the following purposes:

* Generating some derived column values automatically
* Enforcing referential integrity
* Event logging and storing information on table access
* Auditing
* Synchronous replication of tables
* Imposing security authorizations
* Preventing invalid transactions

**Implementations for different RDBMS vary significantly**

## Trigger structure

```
CREATE [OR REPLACE ] TRIGGER trigger_name  
{BEFORE | AFTER | INSTEAD OF }  
{INSERT [OR] | UPDATE [OR] | DELETE}  
[OF col_name]  
ON table_name  
[REFERENCING OLD AS o NEW AS n]  
[FOR EACH ROW]  
WHEN (condition)   
action
```

* CREATE [OR REPLACE] TRIGGER trigger_name − Creates or replaces an existing trigger with the trigger_name.
* {BEFORE | AFTER | INSTEAD OF} − This specifies when the trigger will be executed. The INSTEAD OF clause is used for creating trigger on a view.
* {INSERT [OR] | UPDATE [OR] | DELETE} − This specifies the DML operation.
* [OF col_name] − This specifies the column name that will be updated.
* [ON table_name] − This specifies the name of the table associated with the trigger.
* [REFERENCING OLD AS o NEW AS n] − This allows you to refer new and old values for various DML statements, such as INSERT, UPDATE, and DELETE.
* [FOR EACH ROW] − This specifies a row-level trigger, i.e., the trigger will be executed for each row being affected. Otherwise the trigger will execute just once when the SQL statement is executed, which is called a table level trigger.
* WHEN (condition) − This provides a condition for rows for which the trigger would fire. This clause is valid only for row-level triggers.

## Triggers examples

Designed for SQLite

AFTER-INSERT TRIGGER - New students with GPA between 3.3 and 3.6 automatically apply to geology major at Stanford and biology at MIT

```
create trigger R1
after insert on Student
for each row
when New.GPA > 3.3 and New.GPA <= 3.6
begin
  insert into Apply values (New.sID, 'Stanford', 'geology', null);
  insert into Apply values (New.sID, 'MIT', 'biology', null);
end;
```

AFTER-DELETE TRIGGER - Cascaded delete for Apply(sID) references Student(sID)

```
create trigger R2
after delete on Student
for each row
begin
  delete from Apply where sID = Old.sID;
end;
```

AFTER-UPDATE TRIGGER - Cascaded update for Apply(cName) references College(cName)

```
create trigger R3
after update of cName on College
for each row
begin
  update Apply
  set cName = New.cName
  where cName = Old.cName;
end;
```

BEFORE TRIGGERS, ACTION RAISING ERROR - Enforce key constraint on College.cName (ignore colleges with same names)

```
create trigger R4
before insert on College
for each row
when exists (select * from College where cName = New.cName)
begin
  select raise(ignore);
end;

create trigger R5
before update of cName on College
for each row
when exists (select * from College where cName = New.cName)
begin
  select raise(ignore);
end;
```




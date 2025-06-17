
## Relational Database
Database are most critical components of any system, they make or break the system
Data is stored & represented in rows and columns
Database uses **ACID** properties for transations 

- Atomicity
- Consistency
- Isolation
- Durability



**Atomicity** All Statement within a transaction takes effect or none

- Whenever transaction happens all the changes should take place if one of the statement is faulty then whole process of transaction will fail

**Consistency** Data will never go incorrect , no matter what

-   You have the necessary tools to ensure your data never goes inconsistent

**Isolation** 
When multiple tranaction are executing parrallely, the isolation level determines how much changes of one transaction are visible to other


***Exercise***
[ACID properties practise](./practical/README.md)

_________________________

## Isolation Levels Database

Relational Database provides ACID gurantee and **"I"** in ACID is "Isolation" and isolation level helps us tune them

Isolation Levels dictate how much one transaction knowns about the other.

we look at each one of them and understand with example

***@Repeatable Reads***
*Consistent reads within Same transaction*

Even if other transaction commited 1st transaction would not see the changes (If already reads)

***@Read commited***
*Reads within the ame transaction always reads fresh value*

***@Read Uncommited***
*Reads even uncommited values from other transaction*
(Dirty reads)

***@Serializable***
*Every Reads is a locking read and while one transaction reads, other will have to wait.*
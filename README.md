# System-design
A system-design course for me to understand the deep knowledge about computer 
science and engineering.

it motivates me to become better engineer and it will help me to revise the topics in future project , also for foks those who are intrested in system-design will also get knowledge about it


## Table of Contents
 - **Getting Started**

    - [What is System design?](#what-is-system-design-)
    - [How you approach system design?](#how-you-approach-system-design)
    - [Relational Database ACID](#relational-database)
    - [Isolation Levels](#isolation-levels-database)


## What is System design ?

**Definition:** System design involves creating a product based on a set of requirements. It entaitals deciding the architecture and components necessary to build the system.

**Components Needed:**
- Databases for data storage
- API servers to handle requests
- CDNs for serving images, etc.

### Key Aspects of System Design
**Design Architecture:** High-level structure of the system Determines how different parts fit together

**Design Components:** Individual parts within the system (e.g., web server, database, cache in a Facebook-like application)

**Design Modules:** Detailed design of each part, such as authentication and authorization modules in a larger system


### Practical Applications 
    
- **Real-World Problems**: System design deals with real-world scenarios, making it more relatable than abstract concepts like algorithms. 

- **Problem Breakdown**: It teaches breaking down large problems into manageable parts, enhancing structured thinking.

--------------------------------------------------------

## How you approach system design?

System design is extremely practical and there is a structured way to tackle the situations

***Note:*** Take baby step,no matter what?

### Understand the problem statement 

without having a through understanding of the problem at hand we would easily digress

### break it down into components (essential)

***Note:*** do not create component for the sake of it
***Note:*** Cretae component, that you know are must

**For example:** Lets design a Facebook
let think, what are the features we need.

            components ------------------->   (Auth , Notification , feed) 


Now let breakdown further into subcomponent
**Feed**

                            |---------------|
                            |   generator   |
                            |---------------|
                                    |
                                    |
                                    |
    |---------------|               | Writers
    |   web server  |               |
    |---------------|               |
            |                       |
            |               |---------------|
            |               |               |
            |_______________|---------------|
                Readers     |   Database    |
                            |---------------|


For each sub-component think about 
 - Database caching
- Scaling & Fault tolerance
- Async processing
- communication

________________________________________________________________________________

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
[ACID properties practise](./Relational%20Database/README.md)

_________________________

## Isolation Levels Database


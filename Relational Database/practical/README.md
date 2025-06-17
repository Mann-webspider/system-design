# Relational Database Practical

## excercise

1. Setup a SQL database (mysql or postgres)
2. create a Schema For  social network ( Users . Post , Profile , Photos, following)
3. Insert Data in (User and profile) in one transaction


### Lets setup the sql database

let me use Docker to spin up the postgres container and open the terminal init

```docker
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```

After the docker instance is running, enter to the docker terminal using this command
```docker
docker exec -it some-postgres psql -U postgres
```

### Create database and schema for social network
**Create Database**
```sql
--create a database name social network
CREATE DATABASE social_network;
```
**connect to databse**
```sql
\c social_network;
```


#### **create tables**
**Users Table**
```sql
-- Create Users Table
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Profiles Table**
```sql
-- Create Profiles Table
CREATE TABLE Profiles (
    user_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    bio TEXT,
    profile_pic_url VARCHAR(255),
    FOREIGN KEY (user_id) REFERENCES Users(id)
);
``` 



### Insert data into users and Profiles in One Transaction

Making data insert with transaction 

**Sucessfull transaction**
```sql
START TRANSACTION;

-- Insert into Users table
INSERT INTO Users (username, email, password)
VALUES ('johndoe', 'johndoe@example.com', 'password123') 
RETURNING id INTO user_id;

-- Insert into Profiles table
INSERT INTO Profiles (user_id, first_name, last_name, bio, profile_pic_url)
VALUES (user_id, 'John', 'Doe', 'Hello, I am John Doe!', 'http://example.com/johndoe.jpg');

COMMIT;

```
***output***
```sql
BEGIN
INSERT 0 1
COMMIT
``` 
**Failing transaction**
```sql
BEGIN;

-- Insert into Users table with a duplicate username
WITH inserted_user AS (
    INSERT INTO Users (username, email, password)
    VALUES ('johndoe', 'johndoe2@example.com', 'password123')
    RETURNING id
)
-- Attempt to insert into Profiles table
INSERT INTO Profiles (user_id, first_name, last_name, bio, profile_pic_url)
SELECT id, 'John', 'Doe', 'Hello, I am John Doe again!', 'http://example.com/johndoe2.jpg'
FROM inserted_user;

COMMIT;

```

***Output***
```
ERROR:  duplicate key value violates unique constraint "users_username_key"
DETAIL:  Key (username)=(johndoe) already exists.
ROLLBACK
```

If any part of the transaction fails (e.g., inserting a duplicate username), the entire transaction is rolled back. No partial data will be committed to the database, ensuring data integrity.

This approach ensures that your database remains consistent even in the face of errors.
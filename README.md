# EX-8-Simulating-deadlock-scenario
### DATE:


## AIM:
To simulate a scenario of deadlock in concurrent execution of transactions.
### PROCEDURE:

### Step 1:
Create a accounts table with the schema Accounts (account_id INT PRIMARY KEY,balance DECIMAL(10, 2))

### Step 2: 
Insert the values in the accounts table

### Step 3:
Cteate a transaction T1 and T2

### Step 4:
T1 updates the balance by debiting 200

### Step 5:
Simulate a delay and make T2 inteferes T1

### Step 6:
T2 updates balance by debiting 150

### Step 7:
Simulate a delay and make T1 inteferes T2



### QUERY :
```
-- Creating Accounts table
CREATE TABLE Accounts (account_id INT PRIMARY KEY,balance DECIMAL(10, 2));
-- Inserting sample account data
INSERT INTO Accounts VALUES(1, 1000.00);
INSERT INTO Accounts VALUES(2, 2500.00);

```


### OUTPUT:
![280514431-2f35d3f2-474d-4366-ade6-d0a151da1d2c](https://github.com/Aravindsamy04/EX-8-Simulating-deadlock-scenario/assets/113497037/d7afad4c-069c-4377-a84e-a2c8d9e0750d)

Now, let's set up the two transactions T1 and T2:


### Transaction T1:
```
BEGIN TRANSACTION;
UPDATE Accounts
SET balance = balance - 200.00
WHERE account_id = 1;
-- Simulate a delay to ensure T2 interferes
WAITFOR DELAY '00:00:10'; -- This line introduces a delay
UPDATE Accounts
SET balance = balance + 200.00
WHERE account_id = 2;
COMMIT;

```
### Transaction T2:
```
BEGIN TRANSACTION;
UPDATE Accounts
SET balance = balance - 150.00
WHERE account_id = 2;
-- Simulate a delay to ensure T1 interferes
WAITFOR DELAY '00:00:10'; -- This line introduces a delay
UPDATE Accounts
SET balance = balance + 150.00
WHERE account_id = 1;
COMMIT;

```
### OUTPUT:
```
Msg 1205, Level 13, State 51, Line 3
Transaction (Process ID) was deadlocked
on resourceswith anotherprocess and has been
chosen as the deadlock victim. Rerun the transaction.

```
### RESULT:

Thus the program for the simulation of deadlock has been executed successfully.









# Triggers
What is trigger and usage


///
///RollBack- don’t change anything into the DB, reset it as it was. Reset its state to the first state.
Transaction sequence of actions  that either of them are performed or none of them is performed.

Example:
Make money transaction:
1-We check if Sender exists into the DB, 2.We check if Receiver exists into the DB, 
3.We want to send 500 euro, We check it sender has amount 500 euro, then we send it.
IF sender has 200 euro, we don’t send it. We do nothing.
BANK TRANSFER !

ROLLBACK –a change does not perform. The DB is taken to its previous State.
ROLLBACK- going back to its previous State.
COMMIT -> Save Changes !

////

A transaction is a logical unit of work that contains one or more SQL statements. 
A transaction is an atomic unit. The effects of all the SQL statements in a transaction can be either all committed (applied to the database) or all rolled back (undone from the database).
Transactions are used mostly with procedures.
Example: \
Transactions between twso bank accounts.
Sender-> Receiver
First check if Sender AccountExist, Sec Check if Receiver Account Exist.
Third Check it Sender has money enough to send to receiver.

SEE the whole  SQL Code Structure
BEGIN TRANSACTION
COMMIT
TRANSACTION is SQL Logic and code operations that will perform if all operations complete successfully, 
Or not perform if any of them dont.
Transactions guarantee somehow that into the DB will enter true data.
Transactions help us when some mistake appears to undo, to get beck.
Transactions guarantee that every operations will be done.
Either fails all the transaction or passes all the transaction.
If we insert data in seceral tables, the transaction guarantees that we will insert into the all tables, wither we will not insert anithing.
Transaction is performed wholly, not partially.
Entity Framework send data to the DB using Transactions.
ACID model
Atomic-> all passes or nothing passes, 
Are performed as one whole or all fails, either all or nothing.

Table People, Table Addresses, here the transaction guarantees that there will be no address without a man, either there will not be any man without an address.
In case of failure DB stays unchanged.
ACID model is connected with the Transactions of the DB.
Consistent data/ validated data into the DB.
Check Constraint-> is some limitation to the given Column that help us to insert into this column only given range of data./Limitation of the data inserted into a given column.Transaction obeys the rules of the DB.Transaction can not break the rules of the DB.
Transactions guarantees that the orderd to the DB are checked before the info is inserted into the DB.
Isolation : Transaction running at the same time does not interfere one another.
Durability-> it is guaranteed the security of the data into the DB. If the info is commited into the DB then it is saved. The data can not be lost after commited.
Transactions logs:
Full Transaction log-> means every transaction is kept./history of the transactions.
Automatic and manual migrations.
DB which is ACID Compamatible guarantters, Atomicity, Isolation, Durability.

The ACID properties define SQL database key properties to ensure consistent, safe and robust database modification when saved. ACID is an acronym that helps to remember the fundamental principles of a transnational system. ACID stands for Atomic, Consistent, Isolation, and Durability.

TRIGERS : Is a kind of business logic into the DB.
Trigers are like Stored Procedures for applying some rules.
2:00часа ;

Trigers are extra mechanism for data validation of the DB date, a kind of business logic.
///АФТЕР Тригер
CREATE TRIGGER tr_TownsUpdate ON Towns FOR UPDATE
AS
  IF(EXISTS(
      SELECT * FROM inserted
	  WHERE Name IS NULL OR LEN(Name) = 0))
  BEGIN
        RAISERROR('Town name can not be empty', 16, 1)
		ROLLBACK
		RETURN
  END


  UPDATE Towns SET Name = '' WHERE TownID = 1
/////////////////
CREATE TRIGGER tr_AccountProtect ON Accounts
INSTEAD OF DELETE
AS

UPDATE Accounts SET IsDeleted = 1
FROM Accounts AS a JOIN DELETED AS d ON a.Id = d.Id
WHERE a.IsDeleted = 0
///

A trigger is a special type of stored procedure that automatically runs when an event occurs in the database server. DML triggers run when a user tries to modify data through a data manipulation language (DML) event. ... SQL Server lets you create multiple triggers for any specific statement.S
DML events are INSERT, UPDATE, or DELETE statements on a table or view. These triggers fire when any valid event fires, whether table rows are affected or not. For more information, see DML Triggers.

////
When to use triggers
Because a trigger resides in the database and anyone who has the required privilege can use it, a trigger lets you write a set of SQL statements that multiple applications can use. It lets you avoid redundant code when multiple programs need to perform the same database operation.
You can use triggers to perform the following actions, as well as others that are not found in this list:
•	Create an audit trail of activity in the database. For example, you can track updates to the orders table by updating corroborating information to an audit table.
•	Implement a business rule. For example, you can determine when an order exceeds a customer's credit limit and display a message to that effect.
•	Derive additional data that is not available within a table or within the database. For example, when an update occurs to the quantity column of the items table, you can calculate the corresponding adjustment to the total_price column.
•	Enforce referential integrity. When you delete a customer, for example, you can use a trigger to delete corresponding rows that have the same customer number in the orders table.
///
In this chapter, we will discuss Triggers in PL/SQL. Triggers are stored programs, which are automatically executed or fired when some events occur. Triggers are, in fact, written to be executed in response to any of the following events −
•	A database manipulation (DML) statement (DELETE, INSERT, or UPDATE)
•	A database definition (DDL) statement (CREATE, ALTER, or DROP).
•	A database operation (SERVERERROR, LOGON, LOGOFF, STARTUP, or SHUTDOWN).
Triggers can be defined on the table, view, schema, or database with which the event is associated.
Benefits of Triggers
Triggers can be written for the following purposes −
•	Generating some derived column values automatically
•	Enforcing referential integrity
•	Event logging and storing information on table access
•	Auditing
•	Synchronous replication of tables
•	Imposing security authorizations
•	Preventing invalid transactions
/

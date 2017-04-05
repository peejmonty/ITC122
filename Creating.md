# ITC122
SQLNotes
--creating tables
--this is a single line comment
/*This is a mulitple line comment*/

Use TestTables



 Create table Person
 (

	PersonKey int identity(1,1) primary key, --(1,1) This is an autonumbering command. (starting from 1, counting by 1)
	PersonLastName nvarchar(255) not null,
	PersonFirstName nvarchar(255) null,
	PersonEmail nvarchar(255) not null,
	PersonAddedDate Datetime default GetDate()
 )

 Create table PersonAddress
 (
	PersonAddressKey int identity(1,1),
	PersonAddressStreet nvarchar(255) not null, --(255) could also be replaced with (max) which would allow you to store up to 2GBs of date. 14k bytes are stored per row. while you cant query it you can still retrieve data. 
	PersonAddressCity nvarchar(255) default 'Seattle',
	PersonKey int, --Foreign Key references Person(personKey) 
		--advantage of doing this is you get to create your own naming convention
	constraint PK_PersonAddress primary key(PersonAddressKey),
	constraint FK_PersonAddress Foreign key(personKey) --no comma here because reference is a continuation of the command.
		references Person(PersonKey)

 )

 Create table PersonContact
 (
	PersonContactKey int identity(1,1),
	PersonContactHomePhone nchar(14), --nchar allows you to do characters. Specifically good if you are never doing math with values. 
	PersonKey int, 

 )

 Alter table PersonContact --this allows you to ammend a table without dropping it. This works if there is already data on the table. You'd lose the data if you dropped the table. 
 Add Constraint Pk_PersonContact primary key (PersonContactKey),
 Constraint Fk_personContact foreign key (PersonKey)
	references Person(PersonKey)

Alter table Person
Drop column PersonEmail
									--These two commands allow you to add and remove column. You could lose data if its stored. 
Alter table Person
Add PersonEmail nvarchar(255)

Alter table Person
Add Constraint unique_Email Unique(PersonEmail) --This would require that every email is unique per rec

# Mysql-AddressBook-Service

## UC1 - Create database for addressbook service
```create database address_book_service;```

### Go to the database created
```use address_book_service;```

## UC2 - Create addressbook table with necessary details
```
create table address_book
    -> ( firstName    varchar(150) NOT NULL,
    ->   lastName     varchar(150) NOT NULL,
    ->   Address      varchar(200) NOT NULL,
    ->   City         varchar(200) NOT NULL,
    ->   State        varchar(200) NOT NULL,
    ->   Zip          int(10)      NOT NULL,
    ->   Phone Number int(15)      NOT NULL,
    ->   Email        varchar(300) NOT NULL,
    ->   PRIMARY KEY  (firstName)
    -> );
```

### Viewing the address book table
```DESCRIBE address_book;```

## UC3 - Insert new contacts to address book
```
INSERT INTO address_book(firstName,lastName,Address,City,State,Zip,Phone,Email) VALUES(
    -> 'Deeksha','Sai','Karampakkam','Chennai','TamilNadu',600010,888561875,'saideeksha@gmail.com'),
    -> ('Divya','Sai','Shivajinagar','Hyderabad','Telangana',500019,891967665,'saidivya@gmail.com');
```

### View address book
```SELECT * FROM address_book;```

## UC4 - Ability To Edit Existing Contact with Name

### Editing contact for given name
```UPDATE address_book SET phone=878787777 WHERE firstName='Deeksha';```

### View address book
```SELECT * FROM address_book;```

## UC5 - Ability To Delete Existing Contact with Name
```DELETE FROM address_book WHERE firstName='Deeksha';```

### View address book
```SELECT * FROM address_book;```

## UC6 -Ability to Retrieve Person belonging to a City or State

### Contact of person belonging to particular city
```SELECT * FROM address_book WHERE City='Hyderabad';```

### Contact of person belonging to particular state
```SELECT * FROM address_book WHERE State='Telangana';```

## UC7 - Ability to understand the size of address book by City and State
### Count contacts By city
```
SELECT city,COUNT(city) FROM address_book GROUP BY city;
SELECT COUNT(city) FROM address_book;
```

### Count contacts By state
```
SELECT state,COUNT(state) FROM address_book GROUP BY state;
SELECT COUNT(state) FROM address_book;
```

## UC8 - Ability to retrieve entries sorted alphabetically by Person’s name for a given city
### For a given city ,sort contacts in alphabetical order
```SELECT * FROM address_book WHERE city='Hyderabad' ORDER BY firstName;```

## UC9 - Ability to identify each Address Book with name and Type.
### Altering table
```
ALTER table address_book add AddressBookName varchar(200) AFTER Email;
ALTER table address_book add Type varchar(200) AFTER Email;
UPDATE address_book set type='Family' where firstName='Deeksha';
UPDATE address_book set type='Friends' where firstName='Divya';
UPDATE address_book set type='Professional' where firstName='Uma';
UPDATE address_book set AddressBookName='Personal' where firstName='Uma';
UPDATE address_book set AddressBookName='Casual' where firstName='Deeksha' or firstName='Divya';
```

### View address book
```SELECT * FROM address_book;```

## UC10 - Ability to get number of contact persons(count by type)
```SELECT type,COUNT(type) FROM address_book GROUP BY type;```

## UC11 - Ability to add person to both Friend and Family
```
INSERT INTO address_book(firstName,lastName,Address,City,State,Zip,Phone,Email,Type,AddressBookName) VALUES(
    -> 'Sreenivasulu','Konda','Pragatinagar','Hyderabad','Telangana',500050,949876547,'sreenivasulu@gmail.com','Family','Personal'),
    -> ('Chandan','Reddy','Vasanthnagar','Dilsukhnagar','Bangalore',400097,87008493,'chandanreddy@gmail.com','Friends','Personal');
```

## UC13 - Ensure all retrieve queries done
### Creating table Address_Book_Dictionary
```
create table Address_Book_Dictionary
    -> (
    -> Address_Book_Name VARCHAR(200) NOT NULL PRIMARY KEY,
    -> Address_Book_Type VARCHAR(150) NOT NULL
    -> )ENGINE=INNODB;
```

### Creating table Contacts
```
create table contacts
    -> (
    -> firstName    varchar(150) NOT NULL,
    -> lastName     varchar(150) NOT NULL,
    -> Address_Book_Name VARCHAR(200) NOT NULL,
    -> FOREIGN KEY (Address_Book_Name) REFERENCES Address_Book_Dictionary (Address_Book_Name),
    -> Address      varchar(200) NOT NULL,
    -> City         varchar(200) NOT NULL,
    -> State        varchar(200) NOT NULL,
    -> Zip          int(10)      NOT NULL,
    -> Phone_Number int(15)      NOT NULL,
    -> Email        varchar(300) NOT NULL,
    -> PRIMARY KEY  (firstName,lastName)
    -> );
```

### Inserting into Address_Book_Dictionary table
```
INSERT INTO Address_Book_Dictionary VALUES
    -> ('Personal','Family'),
    -> ('Corporate','Professional'),
    -> ('Casual','Friends');
```

### Inserting into Contacts
```
INSERT INTO contacts VALUES
    -> ('Divya','Sai','Casual','Shivajinagar','Hyderabad','Telangana',500019,891967665,'saidivya@gmail.com'),
    -> ('Sreenivasulu','Konda','Personal','Pragatinagar','Hyderabad','Telangana',500050,949876547,'sreenivasulu@gmail.com'),
    -> ('Deeksha','Sai','Corporate','Karampakkam','Chennai','TamilNadu',600010,888561875,'saideeksha@gmail.com');
```

### Ability to Retrieve Person belonging to a City or State
```
SELECT * FROM contacts WHERE City='Hyderabad';
SELECT * FROM contacts WHERE State='Telangana';
```

### Ability to understand the size of address book by City and State
```
SELECT city,COUNT(city) FROM contacts GROUP BY city;
SELECT state,COUNT(state) FROM contacts GROUP BY state;
```

### Ability to retrieve entries sorted alphabetically by Person’s name for a given city
```
SELECT * FROM contacts WHERE city='Hyderabad' ORDER BY firstName;
```

### Ability to get number of contact persons(count by type)
```
SELECT a.Address_Book_Type,Count(a.Address_Book_Type) FROM Address_Book_Dictionary a left join contacts c on c.Address_Book_Name=a.Address_Book_Name group by a.Address_Book_Type;
```

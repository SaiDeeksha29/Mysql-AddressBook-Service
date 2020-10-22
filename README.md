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

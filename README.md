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


One-to-one:
  Use a foreign key to the referenced table:

student: student_id, first_name, last_name, address_id
address: address_id, address, city, zipcode, student_id # you can have a
                                                        # "link back" if you need
You must also put a unique constraint on the foreign key column (addess.student_id) to prevent multiple rows in the child table (address) from relating to the same row in the referenced table (student).

Example

```sql
CREATE TABLE Gov(
    GID number(6) PRIMARY KEY,
    Name varchar2(25),
    Address varchar2(30),
    TermBegin date,
    TermEnd date
);

CREATE TABLE State(
    SID number(3) PRIMARY KEY,
    StateName varchar2(15),
    Population number(10),
    SGID Number(4) REFERENCES Gov(GID),
    CONSTRAINT GOV_SDID UNIQUE (SGID)
);

INSERT INTO gov(GID, Name, Address, TermBegin)
values(110, 'Bob', '123 Any St', '1-Jan-2009');

INSERT INTO STATE values(111, 'Virginia', 2000000, 110);
```

One-to-many:
  Use a foreign key on the many side of the relationship linking back to the "one" side:

teachers: teacher_id, first_name, last_name # the "one" side
classes:  class_id, class_name, teacher_id  # the "many" side

Example
```sql
CREATE TABLE Vendor(
    VendorNumber number(4) PRIMARY KEY,
    Name varchar2(20),
    Address varchar2(20),
    City varchar2(15),
    Street varchar2(2),
    ZipCode varchar2(10),
    Contact varchar2(16),
    PhoneNumber varchar2(12),
    Status varchar2(8),
    StampDate date
);

CREATE TABLE Inventory(
    Item varchar2(6) PRIMARY KEY,
    Description varchar2(30),
    CurrentQuantity number(4) NOT NULL,
    VendorNumber number(2) REFERENCES Vendor(VendorNumber),
    ReorderQuantity number(3) NOT NULL
);
```

Many-to-many:
  Use a junction table (example):

student: student_id, first_name, last_name
classes: class_id, name, teacher_id
student_classes: class_id, student_id     # the junction table

Example queries:

```sql
 -- Getting all students for a class:

    SELECT s.student_id, last_name
      FROM student_classes sc
INNER JOIN students s ON s.student_id = sc.student_id
     WHERE sc.class_id = X

 -- Getting all classes for a student:

    SELECT c.class_id, name
      FROM student_classes sc
INNER JOIN classes c ON c.class_id = sc.class_id
     WHERE sc.student_id = Y
```

Example

```sql
CREATE TABLE Class(
    ClassID varchar2(10) PRIMARY KEY,
    Title varchar2(30),
    Instructor varchar2(30),
    Day varchar2(15),
    Time varchar2(10)
);

CREATE TABLE Student(
    StudentID varchar2(15) PRIMARY KEY,
    Name varchar2(35),
    Major varchar2(35),
    ClassYear varchar2(10),
    Status varchar2(10)
);

CREATE TABLE ClassStudentRelation(
    StudentID varchar2(15) NOT NULL,
    ClassID varchar2(14) NOT NULL,
    FOREIGN KEY (StudentID) REFERENCES Student(StudentID),
    FOREIGN KEY (ClassID) REFERENCES Class(ClassID),
    UNIQUE (StudentID, ClassID)
);
```


Many to ones
  - https://stackoverflow.com/questions/4601703/difference-between-one-to-many-and-many-to-one-relationship


## Links

- https://vladmihalcea.com/database-table-relationships/

# Programming & SQL Quick Questions

## 1. D in SOLID

    D stands for Dependency Inversion Principle.

    High-level modules should not depend on low-level modules.
    Both should depend on abstractions (interfaces).
    It helps reduce tight coupling in code.

## 2. Difference between INNER JOIN and NATURAL JOIN

    INNER JOIN joins tables using a specified condition.

    NATURAL JOIN automatically joins tables based on columns
    with the same name in both tables.

    INNER JOIN is explicit, NATURAL JOIN is automatic.

## 3. How to overload a constructor

    Constructor overloading means creating multiple constructors
    with different parameters in the same class.

    Example:
    class A:
        def __init__(self, x=None):
            self.x = x

## 4. What happens if we add string and integer

    In most languages this causes a type error.

    Example in Python:
    "10" + 5 → TypeError

    We must convert types first:
    int("10") + 5

## 5. 4 Pillars of OOP

    1. Encapsulation – wrapping data and methods together.
    2. Abstraction – hiding implementation details.
    3. Inheritance – reuse properties from another class.
    4. Polymorphism – same method behaves differently.

## 6. What is Self Join

    A self join joins a table with itself.

    It is useful when rows in the same table are related.

    Example:
    employees joined with employees to find manager.

## 7. What is CSS

    CSS stands for Cascading Style Sheets.

    It is used to style and design HTML pages.

    It controls colors, layout, fonts, spacing and responsiveness.

## 8. Types of SQL Commands

    1. DDL – CREATE, ALTER, DROP
    2. DML – INSERT, UPDATE, DELETE
    3. DQL – SELECT
    4. DCL – GRANT, REVOKE
    5. TCL – COMMIT, ROLLBACK

## 9. How to call a constructor

    A constructor is called automatically when an object is created.

    Example:
    obj = MyClass()

    This creates the object and runs the constructor.

## 10. What are DCL commands

    DCL stands for Data Control Language.

    Used to control database permissions.

    Common commands:
    GRANT
    REVOKE

## 11. Use of TRUNCATE

    TRUNCATE removes all rows from a table.

    It is faster than DELETE because it does not log each row.

    Example:
    TRUNCATE TABLE students;

## 12. What is HTML? Is it a programming language?

    HTML stands for HyperText Markup Language.

    It is used to structure web pages.

    It is not a programming language because
    it does not contain logic or conditions.

## 13. What is Candidate Key

    A candidate key is a column or set of columns
    that can uniquely identify a row in a table.

    A table can have multiple candidate keys.
    One of them becomes the primary key.

## 14. Order of Execution of SQL Query

    FROM
    WHERE
    GROUP BY
    HAVING
    SELECT
    ORDER BY

## 15. Compiler vs Interpreter

    Compiler converts the whole program to machine code at once.

    Interpreter executes code line by line.

    Compiler → faster execution.
    Interpreter → easier debugging.

## 16. Composite Key

    A composite key is a primary key made from
    two or more columns.

    Example:
    (student_id, course_id)

    Both together uniquely identify a record.

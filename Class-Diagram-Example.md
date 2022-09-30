# Mermaid Class Diagram Examples

## Class diagram overview

> "In software engineering, a class diagram in the Unified Modeling Language (UML) is a type of static structure diagram that describes the structure of a system by showing the system's classes, their attributes, operations (or methods), and the relationships among objects." -- Wikipedia

The class diagram is the main building block of object-oriented modeling. It is used for general conceptual modeling of the structure of the application, and for detailed modeling to translate the models into programming code. Class diagrams can also be used for data modeling. The classes in a class diagram represent both the main elements, interactions in the application, and the classes to be programmed.

Example:

```mermaid
  classDiagram
    Animal <|-- Duck
    Animal <|-- Fish
    Animal <|-- Zebra

    Animal : +int age
    Animal : +String gender
    Animal : +isMammal()
    Animal : +mate()

    class Duck {
      +String beakColor
      +swim()
      +quack()
    }

    class Fish {
      -int sizeInFeet
      -canEat()
    }

    class Zebra {
      +bool is_wild
      +run()
    }
```

-----

## Syntax

UML provides mechanisms to represent class members, such as attributes and methods, and additional information about them. A single instance of a class in the diagram contains three compartments:

1. The top compartment contains the name of the class. It is printed in bold and centered, and the first letter is capitalized. It may also contain optional annotation text describing the nature of the class.

2. The middle compartment contains the attributes of the class. They are left-aligned and the first letter is lowercase.

3. The bottom compartment contains the operations the class can execute. They are also left-aligned and the first letter is lowercase.

```mermaid
  classDiagram
    class BankAcccount

    BankAcccount : +String owner
    BankAcccount : +BigDecimal balance
    BankAcccount : +deposit(amount)
    BankAcccount : +withdrawal(amount)
```

-----

## Define a class

UML provides mechanisms to represent class members such as attributes and methods, as well as additional information about them.

Mermaid distinguishes between attributes and functions/methods based on if the **parenthesis**  ```()``` are present or not. The ones with () are treated as functions/methods, and all others as attributes.

There are two ways to define the members of a class, and regardless of whichever syntax is used to define the members, the output will still be same. The two different ways are:

1. Associate a member of a class using : (colon) followed by member name, useful to define one member at a time. For example:

```mermaid
  classDiagram
    class BankAcccount

    BankAcccount : +String owner
    BankAcccount : +BigDecimal balance
    BankAcccount : +deposit(amount)
    BankAcccount : +withdrawal(amount)
```

2. Associate members of a class using {} brackets, where members are grouped within curly brackets. Suitable for defining multiple members at once. For example:

```mermaid
  classDiagram
    class BankAccount {
        +String owner
        +BigDecimal balance
        +deposit(amount)
        +withdrawal(amount)
    }
```

### Return type

Optionally you can end a method/function definition with the data type that will be returned (note: there must be a space between the final ```)``` and the return type. An example:

```mermaid
  classDiagram
    class BankAccount {
        +String owner
        +BigDecimal balance
        +deposit(amount) bool
        +withdrawal(amount) int
    }
```

### Generic types

Members can be defined using generic types, such as ```List<int>```, for fields, parameters, and return types by enclosing the type within ```~``` **(tilde)**. Note: **nested** type declarations such as ```List<List<int>>``` are not currently supported.

Generics can be represented as part of a class definition and also in the parameters or the return value of a method/function:

```mermaid
  classDiagram
    class Square~Shape~ {
        int id
        List~int~ position
        setPoints(List~int~ points)
        getPoints() List~int~


    }

    Square : -List~string~ messages
    Square : +setMessages(List~string~ messages)
    Square : +getMessages() List~string~
```

### Visibility

To describe the visibility (or encapsulation) of an attribute or method/function that is a part of a class (i.e. a class member), optional notation may be placed before that members' name:

- ```+``` Public
- ```-``` Private
- ```#``` Protected
- ```~``` Package/Internal

***Note.*** You can  include additional ***classifiers*** to a method definition by adding the following notation to the ***end*** of the method, i.e., after the ```()```:

- ```*``` Abstract e.g.: ```someAbstractMethod()*```
- ```$``` Static e.g.: ```someStaticMethod()$```

***Note.*** You can include additoinal ***classifiers*** to a feild definition by adding the following notation to the end of its name:

- ```$``` Static e.g.: ```String someField$```

-----

## Defining relationship
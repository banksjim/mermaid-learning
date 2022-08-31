
> Exercises for YouTube introductory video: "Mermaid JS: Finally There's A Great UML & Diagram Drawing Tool"; https://youtu.be/JiQmpA474BY

# Mermaid tutorial

## Flowchart Diagram Example

```mermaid
flowchart LR
    Start-Login --> A(Enter your email address);
    A --> B{Existing user?};
    B --> |Yes| C[Start login];
    B --> |No| D(Enter name);
    D --> E{Accept conditions?};
    E --> C;
    E --> |No| A;
```

<hr>

## Sequence Diagram Example

```mermaid
sequenceDiagram
   participant Client;
   participant OAuthProvider;
   participant Server;

   autonumber

   Client ->> OAuthProvider: Request access token;
   activate OAuthProvider;
   OAuthProvider ->> Client: Send access token;
   deactivate OAuthProvider;
   Client ->> Server: Request resource;
   activate Server;
   Server ->> OAuthProvider: Validate token;
   activate OAuthProvider;
   OAuthProvider ->> Server: Token valid
   deactivate OAuthProvider;
   Server ->> Client: Return resource;
   deactivate Server;
```

<hr>

## Class Diagram Example

> '-' = private interface;
> '+' = public interface;
> '#' = protected interface;

> <|-- = inheritance relationship (e.g. class and a sub-class)

> o-- = aggregation relationship (another special case of an association relationship -> the object of the class relationship can exist independently of the associated class object) (e.g. Customer can be associated with an Order object, but if you delete the Order then you'd still want to keep the Customer object)

> *-- = composition relationship (a special case of an association relationship -> the object of the class relationship is composed of and doesn't exist independently of its associated class object) (e.g. A Student object can be connected to a Schedule object, but if you remove the Student object it would also make sense to remove the associated Schedule object for that student)

```mermaid
classDiagram

   class Order {
    +OrderStatus = status
   }

   class OrderStatus {
    
    <<enumeration>>
    
    FAILED
    PENDING
    PAID
   }
   Order o-- Customer


   class PaymentProcessor {
    
    <<interface>>
    
    -String apiKey
    
    #connect(String url, JSON header)

    +processPayment(Order order) OrderStatus
   }
   PaymentProcessor <|-- StripePaymentProcessor
   PaymentProcessor <|-- PayPalPaymentProcessor


   class Customer {
    +String name
   }
   Customer <|-- PrivateCustomer
   Customer <|-- BusinessCustomer

   Car *-- Engine
```

<hr>
## Entity-Relationship Diagram Example

> A good diagram for entity domain modeling

> |o or o| = Zero or one
> || or || = Exactly one
> }o or o{ = Zero or more (no upper limit)
> }| or |{ = One or more (no upper limit)

```mermaid
   erDiagram 
     Customer ||--o{ Order : Places
     Order ||--|{ LineItem : Contains

     Customer {
        String id
        String name
     }

     Order {
        String id
        OrderStatus status
     }

     LineItem {
        String code
        String description
        int quantity
        int price
     }
```

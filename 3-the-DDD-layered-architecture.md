# Modern Software Architecture

## <span style="color: #3C5DD8"> The DDD Layered Architecture </span>

### Key Points

- Layers and tiers (Segmentation of a software system)
- Domain layer (Patterns for organizing the business logic)
- Other layers (From presentation to persistence)

#### Spaghetti-code vs. Lasagna-code

Spaghetti-code is a messy tangle of instructions leading nowhere near to any flicker of solid software. <br/>
Lasagna-code is a layered block of modules easy to cut vertically and/or horizontally and easy to deploy.

#### Classic 3-tier layers

- Presentation
- Business
- Data

#### DDD layers

- Presentation (UX)
- Application (Use-cases)
- Domain (Business)
    - Model
    - Services
- Infrastructure (Persistence)
    - IoC
    - Cache
    - Repositories --> db

Business concerns can be resolved by peaking one of these these design patterns:
- TX Script
- Table Module
- Domain Model
- CQRS
- EventSourcing

Persistence concerns can be resolved by peaking one of these format for storing data:
- Relational
- NoSQL
- Memory

### Presentation Layer

It is responsible for providing some user interface to accomplish any tasks. <br/>
Today the presentation is the most critical part of the application. <br/>
Presentation has always been a part of the system that is directly exposed to the users. <br/>

This layer is responsible for:
- Providing the **user interface** to accomplish any required tasks.
- Providing a effective, smooth and pleasant **user experience**.

Attributes of presentation layer:
- Task-based
- Device-friendly
- User-friendly
- Faithful to real-world processes

### Application Layer

This layer is just where you orchestrate to implementation of your application use-cases.

Where does code that formats data for presentation purposes really belong? <br/>
It's Clearly a presentation concern.<br/>
It sounds more like a business logic aspect.<br/>
Data is data and the database returns the data.<br/>

What does this layer do?
- Reports to the presentation
    - Serves ready-to-use data in the required form
- Orchestrates tasks triggered by presentation elements
    - Use-cases of the application frontend
- Doubly-linked with presentation
    - Possibly extended or duplicated when a new frontend is added

The link between presentation layer and application layer should be established right when you design the user interface.

``` c#
public class InputModel
{
    string Id { get; set; }
}

public class CustomerService
{
    ViewModel Search(InputModel m);
}

public class ViewModel
{
    string Name { get; set; }
    string Address { get; set; }
    string City { get; set; }
    IList<OrderDto> Orders { get; set; }
}
```

In the design of a software system you go through 3 key phases:
1. Crunch knowledge about the business domain
2. Split the business domain in bounded contexts
3. Learn the language of the business domain

#### What is the next step?

It's all about implementing all business rules and organizing the business logic.

### Business Logic - An Abstract Definition

- Application logic (depends on use-cases)
    - Application entities
    - Application workflow components
- Domain logic (invariant to use-cases)
    - Business entities
    - Business workflow components

These two logics are made of entities to hold data and workflows to orchestrate behavior.

### Business Logic - DDD Definition

- Application logic (depends on use-cases)
    - Data transfer objects
    - Application services
- Domain logic (invariant to use-cases)
    - Domain model
    - Domain services

In DDD the application logic is implemented in application layer.<br/>
Domain logic is all about banking business rules into the code.<br/>
A **Business Rule** is any statements that explains in detail the implementation of a business process or describe a business policy to be taken into account.

### Common Patterns

Common patterns for organizing the business logic are:
- TX Script
- Table Module
- Domain Model

#### Transaction Script **Pattern**

This pattern is probably the simplest possible pattern for business logic.

1. System actions
     - Each procedure handles a single task
2. Logical transaction
     -  end-to-end from presentation to data
3. Common subtasks
     - split bounded sub-procedures for reuse

Transaction script pattern leads to a design in which actionable UI elements in the presentation layer invoke application layer's endpoints and these endpoints run transaction script for just each task.

#### Table Module **Pattern**

This pattern has more database centric way of organizing the business logic. The core idea here is that the logic of a system is closely related to persistence and databases.

1. One module per table in the database
2. Module contains all methods that will process the data
     - Both queries and commands
3. May limit modules to "significant" tables
     - Tables with only outbound foreign-key relationships

#### Domain Model **Pattern**

This pattern refers to having a software model for the domain.
It is usually used in DDD, but is not the strict part of it.

1. Aggregated objects
     - Data and behavior 
2. Persistence agnostic
3. Paired with domain services

### Domain Layer

In this layer the architect places all the logic that is invariant to use-cases. This means a software model for the business domain, just the domain model, and related set of domain services.

The domain model is not necessarily an implementation of the **Domain Model** pattern. <br/>
The primary responsibility of domain services is persistence.

#### Domain Model

- Models for the business domain
  - Object-oriented entity model
  - Functional model (tasks are expressed as functions)
- Guidelines for classes in an entity model
  - DDD conventions (factories, value types, private setters)
  - Data and behavior
- Anemic model
  - Plain data containers (Behavior and rules moved to domain services)

#### Domain Services

- Contains pieces of domain logic that don't fit into any of the existing entities
- Classes that group logically related behaviors
  - Typically operating on multiple domain entities
- Implementation of processes that
  - Require access to the persistence later for reads and writes
  - Requires access to external services

### Infrastructure Layer

Infrastructure (software) is set of the fundamental facilities needed for the operation of a software system.

#### Fundamental Facilities of Software System

- Persistence (like database)
- Security
- Logging & Tracing
- Inversion of Control
- Caching
- Networks

Infrastructure layer is place down where technologies belong.<br/>
Infrastructure layer is where you start dealing with configuration details; things like ConnectionStrings, file paths, TCP addresses or URLs.<br/>
To keep the application decoupled from specific products, you sometimes want to introduce facades to hide technology details while keeping the system 
resilient enough to be able to replaced technologies at any time in the future with limited effort and cost.

## Source of content:

[Modern Software Architecture: Domain Models, CQRS, and Event Sourcing](https://www.pluralsight.com/courses/modern-software-architecture-domain-models-cqrs-event-sourcing)

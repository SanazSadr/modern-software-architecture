# Modern Software Architecture

## <span style="color: #3C5DD8"> The "Domain Model" Supporting Architecture </span>

### Key Points

- The foundation of Object-oriented Model for creating business domain
- Domain Services
- Events, Processes and more...

### Domain Model Supporting Architecture

In a domain model architecture the domain layer is made of two main components:
1. Domain Model
   - Aggregates
   - Entities
   - Value types
   - Factories
2. Domain Services
   - Cross-aggregate behavior
   - Repositories
   - External services

#### Key **DDD** Misconceptions

- Perceived simply as having an **object model** with some special characteristics
- **Database** is merely part of the infrastructure and can be neglected
- Ubiquitous Language is a guide to naming classes in the object model

#### Clearing Misconceptions

- Just an object model
  - Context mapping is paramount
  - Modeling the domain through objects is just one of the possible options
- Database agnostic
  - The object model must be easy to persist
  - Persistence, though, should not be the primary concern
  - Primary concern is making sense of the business domain
- Ubiquitous Language
  - Understand the language to understand the business
  - Keep language of business in sync with code

The domain layer is the API of the business domain, and you should make sure that no wrong call to the API is possible that can break the integrity of the domain.<br/>
You should be clear that in order to stay continuously consistent with the business, you should focus your design on behavior much more than on data.<br/>
To Make Domain Driven Design a success you must understand how the business domain works, and render it with software. That's why it's all about **behavior**.

### Aspects of a Domain Model

If a developer <span style="color: yellow">**can**</span> use an API the wrong way, <span style="color: yellow">**he will**</span>.<br/>
How to avoid that? With Proper design.

The real direction we're moving today, is more and more about correctly identifying and rendering Business Processes with all of their related data and events.<br/>

### Database-centric Domain Models

#### Domain Layer

1. Domain Model
   1. Module(s)
      1. Entities
      2. Values
2. Domain Services
   1. Repositories (have access to storage)
   2. Proxies (external web services)

A value object is fully described by its attributes. The attributes of a value object never change once the instance has been created.<br/>
All objects have attributes but not all objects are fully identified by the collection of their attributes.<br/>
When attributes are not enough to guarantee uniqueness, and when uniqueness is important to specific object that you just have domain driven design entities.

In a domain model the aggregation of multiple entities under a single container is called an **aggregate**.

To indicate a value object in .net you use a value type. The most relevant aspect of value type is that it is a collection of individual values.<br/>
The type therefor is fully identified by its collection of attributes, and the instance of the type is immutable.<br/>
In other words, the attributes of a value object never change once the instance has been created.<br/>
Value types are used in primitive types such as `int`, `string` and etc. because they're more precisely and accurately rendered values and quantities found in the business domain.

#### Value Type

``` c#
public int OutsideTemperature { get; set; }

public Temperature OutsideTemperature { get; set; }
```

In the second line where we have `Temperature` model we can have:
- Constructor(s)
- Min and Max constants
- Ad hoc setters with built-in validation and compensation logic
- Ad hoc getter
- Ad hoc comparison
- Additional properties

#### DDD Entities

Not all objects are identified by their collection of attributes. Sometimes you need an object to have an identity attribute.<br/>
When uniqueness is important to the specific object, then you have just entities. But in other way, if the object needs an Id attribute to track it 
uniquely throughout a context for entire application life cycle, then the object has an identity and it said to be an entity.<br/>
An Entity is a class with properties and methods when it comes to behavior it's important to distinguish domain logic from persistance logic.
Domain logic goes into the domain layer, model or services. Persistence goes in the infrastructure layer, managed by domain services.

#### DDD Aggregate

An aggregate is a collection of logically related entities and value types. More than a flat collection, an aggregate is a cluster of associated objects 
including then relationships that you find easier to treat as a single entity for a purpose of queries and commands.
In cluster there is a root object that is the public endpoint that the outside world uses to query or command. Access to other members of the aggregate is always
mediated by the aggregate root. Two aggregates are separated by a sort of a consistency boundary that suggests how to group entities together.
The design of aggregated is closely inspired by the business transactions required by the system. Consistency here means transactional consistency objects in the aggregate expose an overall behavior that is fully consistent with the business purposes.

### That Crazy Little Thing Called Behavior

#### Persistence vs. Domain Model

- Persistence Model (The model you use to persist data)
  - Object-oriented model 1:1 with underlying relational data
  - Reliable and familiar to most developers
  - Doesn't include business logic (except perhaps validation)
- Domain Model (The main focus is behavior)
  - Object-oriented model for business logic
  - Persistable model
  - No persistance logic inside

### Domain Model as a Domain API

#### What's behavior?

The way in which one acts or conducts oneself, specially towards others.

Behavior is:
- Methods that validate the state of the object
- Methods that invoke business actions to perform on the object
- Methods that express **business process** involving the object

### Domain Services

#### Facts on an Aggregate

Work with fewer objects and coarse grained and with fewer relationships.

- Protect as much as possible the graph of entities from outside access
- Ensure the state of child entities is always consistent
  - If the business has a rule that requires that no detail of the order can be updated once it has shipped, the aggregate must offer a public API that makes this update impossible to achieved in code.
- Actual boundaries of aggregates are determined by business rules 

For example a customer has an address. Customer and address are two entity classes.
If the address is an entity that exists only to be an attribute for the customer, they forme as an aggregate; otherwise they are distinct aggregates that work together.

#### Common Responsibilities (Associated with an Aggregate Root)

An aggregate root object is the root of the cluster of associated objects that form the aggregate. An aggregate root has global visibility throwout the domain model and can be referenced directly, is the only part of the aggregate that can be referenced directly, and it has a few Responsibilities too.

In particular it has to:
- Ensure encapsulated objects are always in a consistent state
- Take care of persistence for all encapsulated objects
- Cascade updates and deletion through the encapsulated objects
- Access to encapsulated objects must always happen by navigation

**<span style="color: red">One Repository per aggregate</span>**

### Events in the Business Domain

#### Domain Service

- Domain services are classes which method's implement the domain logic that doesn't belong to a particular aggregate and most likely span over multiple entities.
- Domain services coordinate the activity of aggregates and repositories with the purpose of implementing a business action.
- Domain services may consume services from the infrastructure, such as when sending an email or a text message is necessary.

Actions in domain services come from <span style="color: yellow">**requirements**</span> and are approved by <span style="color: yellow">**domain experts**</span>. <br/>
Names used in domain services are strictly part of the ubiquitous language.

#### Domain Service **Example**

##### Determine whether a given customer reached the status of "gold" customer

A customer earns the status of "**gold**" after she exceeds a given threshold of orders on a selected range of products.

This leads to a number of distinct actions and aspects:

1. Need to query **Orders** and **Products** determine
2. Not the **right** job for an aggregate (data access!)
3. Value set on any newly created instance of **Customer**
4. Cross-aggregate **domain** logic
5. Strictly **business-oriented**

##### Booking a meeting room

Booking requires **verifying** availability of the room and **processing** payment.

We have two options here:

1. **Booking** domain service
   1. Read the member credit status
   2. Check the room availability
2. **Booking** aggregate
   1. Room and Member child objects
   2. Aggregate repository does the job

##### Repository

In DDD, a repository is just the class that handles <span style="color: yellow">**persistance**</span> on behalf of entities and ideally aggregate roots.

- Most popular type of domain service
- Take care of persisting aggregates
- One repository per aggregate root
- Any assembly with repositories has a direct dependency on data stores
- A repository is where you deal with connection strings and use SQL commands

``` c#
public interface IRepository<T> where T:IAggregateRoot
{
    T Find (object id);
    bool Save (T item);
    bool Delete (T item);
}
```

### Anemic Models

#### Why should you consider events in a domain layer?

Events are optional, but they are just a more effective and resilient way to express the intricacy of some real-world business domain.

In an online store application an order is placed and is processed successfully by the system. Which means that the payment is ok, delivery order was passed and received by the shipping company, and the order was generated and inserted in the system.

Let's suppose that business requirements wants you to do some special task(s) to perform upon creation of the order.

Where would you implement such task(s)?

##### Option #1

``` c#
/*Add any tasks to the method that processed the order*/
void Checkout(ShoppingCart cart)
{
    // Proceed though the necessary steps
    ...
    if (success)
    {
        // Execute task(s)
        ...
    }
}
```

**Facts**:
- Not very expressive
  - Monolithic code
  - Future changes require to touch the service
  - Risk of turning into rather complicated code
- Violations of ubiquitous language?
  - The adverb "when" in requirements indicates what to do when a given "event" is observed

##### Option #2

Raise an event for domain-relevant facts.

- No need to have all handling code in one place.
- Raise of the event distinct from handling the event.
- Can handle the same event in multiple places.

**event**
``` c#
public class GoldMemberStatusReached : IDomainEvent
{
    public GoldMemberStatusReached(Customer customer)
    {
        Customer = customer;
    }

    public Customer Customer { get; set; }
}
```

**raise**
``` c#
void Checkout(ShoppingCart cart)
{
    // Proceed though the necessary steps
    ...
    if (success)
    {
        // Execute task(s)
        Bus.RaiseEvent(new GoldMemberStatusReached(customer));
    }
}
```

**Facts**:
- Bus as an "external" element
  - Part of the infrastructure
  - Notify listeners

### Beyond Single All-encompassing Domain Models

#### Anemic Models

Anti-pattern because "**it takes behavior away from domain objects**".

In an anemic domain model, all objects may still match conventions of the ubiquitous language and some of the DDD guideline for object modeling like value types over primitive types and relationships between object. <br/>
The inspiring principle of the anemic domain model is that you have no behavior in entities, just properties; <br/>
and all the required logic places in service components that all together contain the domain logic. <br/>
These services orchestrate the application logic that use-cases and consume the domain model and accessed storage.

Is this **really** an anti-pattern today?

### Entity Framework and Code First

- Define a model of classes. Is it representing the domain model?
  - No, it's mostly representing the persistence model.
- Add behavior to a persistence model
  - May or may not keep the resulting model fluent enough to express the ubiquitous language and be friendly enough to be persisted via EF.
- Database is infrastructure, but also a constraint
  - Domain model
  - persistence model
  - Adapters

The model you end up with when using **Code first** and **Entity Framework** is hardly a domain model, it is a lot more anemic than you may think.

## Source of content:

[Modern Software Architecture: Domain Models, CQRS, and Event Sourcing](https://www.pluralsight.com/courses/modern-software-architecture-domain-models-cqrs-event-sourcing)

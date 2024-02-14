# Modern Software Architecture

## <span style="color: #3C5DD8"> DDD at a Glance </span>

### Key points

- Repositioning: Domain-driven Design
- Exploring Supporting Architectures
- UX-first Design Methodology

### Where does complexity come from?

1. Make sense of requirements
2. Build a (relational) data model
3. Identify relevant tasks and data tables
4. Build a user interface
5. Close to what users wanted but...

#### Big Ball of Mud (BBM)

A system that's largely unstructured, padded with hidden dependencies between parts, with a lot of data and code duplication and an unclear identification of layers and concerns-a spaghetti code jungle.

### Why is DDD so intriguing?

- **Captured** known elements of design process
- **Organized** them into a set of principles
- Made **domain modeling** the focus of development
- **Different** approach to building business logic

### DDD is **still** about business logic

It just suggests you follow a different approach. More focused on domain which is data and **behavior** instead of just mostly data.

1. Crunch knowledge about the domain. Learn as much as possible about the domain, not simply a flat list of rules, not simply a bunch of entity names, but try to capture the essence of the domain and how things go.
2. Recognize subdomains. You should not be afraid to split big thins into smaller and more manageable pieces.
3. Design a rich domain model. For each recognized subdomain you can design a rich object model that describes how our entities behave and our actions by users.
4. Code by telling objects in the domain model what do to. 

### The secret dream of any developer

An all-encompassing object model describing the entire domain.

#### Supreme Goal

Tackling **Complexity** in the heart of software.

However you want to frame it, DDD represents a significant landmark in software development.

- Took root in Java space
- Blissfully ignored in .NET until recently

DDD is another way to organize business logic

Why should I spend days around the design of a class when I can find a **non-classy** way out far more quickly?

### DDD was not cheating

- DDD was the right hammer **bundled** with the wrong set of nails
- DDD is more about analysis than about actual coding strategies

In 2009, five years later, the main focus of DDD has shifted.
**Discovering** the domain architecture more than **organizing** the business logic.
**Domain model** remains a valid pattern to organize the business logic but other patterns can be used as well.

### Common summary of DDD

 - Build an object model for the business domain
 - Consume the model in a layered architecture

 #### DDD == Domain-driven Design

 **You** **Design** the system **Driven** by your knowledge of the **domain**

 DDD has **two** distinct parts.
 You always **need one** but can happily **ignore** the other.

 1. Analytical (Valuable for everybody and every project)
 2. Strategic (One of many possible supporting architecture)


## Source of content:

[Modern Software Architecture: Domain Models, CQRS, and Event Sourcing](https://www.pluralsight.com/courses/modern-software-architecture-domain-models-cqrs-event-sourcing)

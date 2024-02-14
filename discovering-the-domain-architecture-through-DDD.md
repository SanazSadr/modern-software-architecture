# Modern Software Architecture

## <span style="color: #3C5DD8"> Discovering the Domain Architecture through DDD </span>

### Key points

- Ubiquitous Language, definition and discovery
- Bounded Context, definition and discovery
- Context Map, design of top-level architecture

### Ubiquitous Language

It is the part of DDD that aims at building a common and business oriented language. The primary goal of the language is avoiding misunderstanding and avoiding assumptions.

#### What is Ubiquitous Language?

- Vocabulary of domain-specific terms
    - Nouns, verbs, adj, idiomatic expressions and even adverbs
- Shared by all parties involved in the project
    - Primary goal of avoiding misunderstandings
- Used in all forms of spoken and written communication
    - Universal language of the business as done in the organization

Discovering Ubiquitous language starts from User Requirements.

Ubiquitous language is made of words and verbs that truly reflect the semantic of the business domain.

In our definitions we shouldn't have ambiguity or synonyms. <br/>
**Different** concepts should be named **differently**. <br/>
**Matching** concepts should be named **equally**. <br/>

#### How much is technical?

It is neither the language of the business, nor the language of the development. They both are involved in the language. It is a combination of the business and technical.

### Tips from the trenches

- Avoid using acronyms if it is possible, because they are domain-specific and hard to remember.
- The language of the glossary can be English or the language of the customer. A word to word table can be created for translating from customer language to English in order to reduce ambiguity.
- Software developers are responsible for keeping the language and the code in sync.

### UL in code

-  Naming conventions
    - Classes
    - Members
    - Namespaces
- Extension Methods
- Tools
    - Code assistants
    - Refactoring tools
- Agnostic
    - No mandated technology
    - No mandated paradigm

### What is the Bounded Context?

The UL changes as the project grows, but it shouldn't change indefinitely.

**Bounded Context** is the delimited space where an element has a well-defined meaning. <br/>
It is beyond the boundaries of the context, the language changes. Every bounded context has its own UL. <br/>
The business domain split in a web of interconnected contexts. Each context has its own architecture and implementation.

Sometimes you find out that the same term has different meanings when used by different people. When this happens, you should know that the business domain has been splitted in many related bounded contexts.

| Problem Space | Solution Space  |
| ------------- | --------------- |
| Domain        | Domain Model    |
| Subdomain     | Bounded Context |

- A Bounded Context has its own
    - Ubiquitous Language
    - Independent implementation (e.g., CQRS)
    - External interface (to other contexts)

Imagine there are two development team working on a big project and there are lot of domain models, and each team work on their own area of influence. A word like *account* is used in both teams but with different meanings. When two or more models overlap, they can be merged into a more flexible model.

We usually have one bounded context for each business department in the company.

### Event Storming

It's primary purpose is exploring a business domain from observable domain events.

#### How it works

1. Identify relevant domain events
2. Find what causes the event
3. Look at the modeling surface as a timeline

## Source of content:

[Modern Software Architecture: Domain Models, CQRS, and Event Sourcing](https://www.pluralsight.com/courses/modern-software-architecture-domain-models-cqrs-event-sourcing)
# Readme


1. JAVA
   - Core
     - Abstract class vs Interfaces, why and when to use? Abstract class vs Interfaces where better to use?
     - loose coupling & high cohesion
     - Equals & HashCode, hashCode & equals contract? busket 1, 2, hashcode collision, if two objects equal then hashcode should be the same, [[link](https://medium.com/coding-corpus/java-important-methods-equals-hashcode-and-compareto-6adcdf2814c3)]
     - Lambda, Anonymous classes
     - anonymous function, lambda, functional interface, default methods, do you know any functional methods?
     - Immutable class? class final, private final members, initialise everything in constructor, deep copy, no setters! 
     - JVM inside, class loaders, rt.jar, bootstrap. https://medium.com/geekculture/java-backend-developer-interview-questions-pt-1-10-1c74c76442bd
     - Funtional interfaces java, purpose, examples? single abstract method, to avoid boilerplate using anonymous classes, Consumer, Predicate, Function, Supplier.
     - Garbage collector, Memory management, memory allocate. heap=objects, permgen(metaspace):classes, static, string pool. stack: primitive objects, references. [[link](https://diptendud.medium.com/java-memory-management-interview-questions-and-answers-204d7a249019)]
     - class Objects.
   - Streams
     - aggregation functions [[link text itself](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)]
     - repeat Streams, map, multiply, reduce, groupby, summarise, max, min, Function interfaces? [[link](https://www.youtube.com/watch?v=o1H6kMlCQ74&ab_channel=Bobocode)], [[link] (https://medium.com/swlh/java-collectors-and-its-20-methods-2fc422920f18)]
   - Threads
     - Singleton class
     - Thread safe, DeadLock?
     - volatile
     - Lock interface, locking, synchronize block
     - Executors
     - Race condition. Occurs in programming when two or more execution threads modify a shared resource.
   - Collections
     - LinkedList vs ArrayList, pros & cons? LinkedList vs ArrayList (size capacity 10 by default).
       Linked list fast for add and remove O(1), slow access O(n).
       ArrayList fast random access O(1), but slow add and delete!
     - public interface Collection<E> extends Iterable<E>
     - thread safe Collections?
     - fast fail, fail safe
     - implement Comparable, or anonymous class Comparator
     - Iterator used for change mutable objects like created by List.of
   - Java 11 vs 17, Text blocks """text""", Records, S.toList() instead of S.collect(Collectors.toList())
   - DDD
   - GoF patterns
     - Remember most usage patterns: Strategy(lambda!), Observer, Decorator, Iterator, Builder.
     - BandOf4 patterns? what you use? Observer, Proxy, Iterator vs Iterable? Adapter, Decorator, Facade.
     - Decorator pattern(structural), decor. https://medium.com/analytics-vidhya/simplify-strategy-using-lambda-expression-40195d1445ea
   - SOLID
     - Liskov = The principle defines that objects of a superclass shall be replaceable with objects of its subclasses without breaking the application.
     - Dependency inversion = High level modules should not depend upon low level. Everything should be dependent on abstraction.
     - Interface sagregation = “Clients should not be forced to depend upon interfaces that they do not use.” By following this principle, you prevent bloated interfaces that define methods for multiple responsibilities. Split one interface to more with specific responsibilities.
   - etc

3. SPRING
   - Spring vs SpringBoot
   - Dependency injection?
   - SpringBoot
       - Spring bean lifecyrcle, initialization, scopes
       - inject by constructor or setter, factory method, what is the best option?
       - Stereotypes?
       - @Transactional, Proxy?
       - Spring Actuator - production ready features (health check, metrics)
4. DATABASE
   - NoSql vs RDBMs, NoSQL(high velocity-speed, high handle volume data). https://www.geeksforgeeks.org/difference-between-relational-database-and-nosql/
   - ACID, transaction, isolation levels, anomalies, indexes?
   - what is connection pool? purpose
   - SQL queries [[link](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)]
   - sql joins, group by, avg() >, departments & employees salary [[link1](https://sqlbolt.com/)] [[link2](https://www.youtube.com/watch?v=d-SJmsgoUrw&ab_channel=CrackConcepts)]
   - SQL update script, ALTER TABLE table_name ADD column_name datatype;
   - Answer for question: How to change DB tables in the running environment? (manually without Liquibase)
   - Isolation levels from lowest to highest are Read Uncommitted, Read Committed, Repeatable Read, and Serializable. [[link] (https://jetherrodrigues.dev.br/transaction-management-in-the-spring-framework-996d700f1f27)]
4. ORM
   - JPA vs Hibernate, more then one difference?
   - Lazy loading JPA/Hibernate
   - Optimistic Lock @Version
   - How to One to One mapping?
   - Jpa entity states: New, Managed, Detached(when Session closed), Removed.
   - Cache L1, L2, query cache in JPA
   - N + 1 problem?
   - JPA relationship 1-n, n-1, @Entity, other annotation links tables? department-employee. [[link](https://medium.com/thefreshwrites/manytoone-onetomany-mapping-in-jpa-32581d3c0f8a)], [[link] (https://www.baeldung.com/jpa-one-to-one)], [[link] (https://www.tutorialspoint.com/jpa/jpa_entity_relationships.htm)]
   - Opimistic lock? jpa, hibernate, entity stages, detached? Transient(Created), Managed, Detached, Removed
   - Liquibase vs Flyway, changelogs. Flyway uses SQL-based migration scripts, whereas. Liquibase uses XML, YAML, or JSON to define the database changes. https://www.linkedin.com/pulse/database-migration-flyway-vs-liquibase-rafael-porto-rodrigues#:~:text=Configuration%3A%20Flyway%20follows%20a%20convention,to%20define%20the%20database%20changes.
   - Hibernate audited, @Audited - generate table with suffix table_aud
5. REST
   - Rest vs Soap
   - idempotent, [[link](https://restfulapi.net/idempotent-rest-apis/)]
   - Rest header, body, query parameters
   - 
6. Microservices
   - Event driven communication vs REST, when to use?
   - how did you specify the boundaries of your microservices. [[link](https://blog.bitsrc.io/how-to-choose-microservices-boundaries-5c68b0b1af24)], [[link](https://nathanpeck.com/making-microservice-boundaries-that-you-wont-regret/)], [[link](https://codeburst.io/microservice-boundaries-five-characteristics-to-guide-your-design-89312b65cc27)] , [[link](https://www.linkedin.com/advice/0/how-do-you-identify-boundaries-microservices-from)], [[link](https://www.linkedin.com/advice/3/how-do-you-set-microservice-boundaries-skills-software-design#:~:text=One%20of%20the%20first%20steps,inventory%20management%2C%20or%20payment%20processing.)] , [[link](https://www.oreilly.com/library/view/microservices-up-and/9781492075448/ch04.html)] , [[link](https://www.lokajittikayatray.com/post/how-to-define-your-microservices-correctly)]
   - fault tolerant approach, Bulkhead pattern, Circuit Breaker. https://www.codecentric.de/wissens-hub/blog/resilience-design-patterns-retry-fallback-timeout-circuit-breaker, https://www.youtube.com/watch?v=ADHcBxEXvFA&ab_channel=DefogTech, https://quickbooks-engineering.intuit.com/resiliency-two-alternatives-for-fault-tolerance-to-deprecated-hystrix-de58870a8c3f, 
   - 
7. Docker
   - What is docker container itself?
   - Docker networking?, Docker swarm, compose? how to expose or open service connection outside?
8. K8s
   - K8s question: if your service in K8s is down what is your step to do? service describe, readiness probe.
    Read Troubleshooting applications kubernetes.io , startup, liveness, readness probe, describe pod, [[link](https://stackoverflow.com/questions/65858309/why-do-i-need-3-different-kind-of-probes-in-kubernetes-startupprobe-readinessp)]
   - etc
9. Clean Code and Uncle Bob, Craftmanship
   - code refactoring how to? Better organization, Less code duplication, Easier maintenance, understandable, readable, structured, documented
   - code challenge -thinking simply not complex. Rest apis> dont use Feign! use WebClient!
   - time complexity Big On, https://aaronice.gitbook.io/lintcode/linked_list. [[link](https://flexiple.com/algorithms/big-o-notation-cheat-sheet/)]
   - https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html
   - TDD
   - Naming unit test. [UnitOfWork_StateUnderTest_ExpectedBehavior], Sum_NegativeNumberAs1stParam_ExceptionThrown().
   - UML, [[link](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-aggregation-vs-composition/#:~:text=Aggregation%20implies%20a%20relationship%20where,exist%20independent%20of%20the%20parent)].
10. CI/CD
    - feature toggle, how to manage if one main branch
    - git flow? what is trunk base? main branch etc.
    - CI/CD how it? ArgoCD, Octopus deploy, GitLab
11. Linux
    - how to remote connect in Linux/Unix, SSH command? most common list commands
    - 
12. Agile
    - How are you start working on task? Jira, Task, Epic, User story, Scram, Kanban.
    - what was your last task you working on?
    - Scrum pocker
13. Code challenges
    - etc
14. etc
15. etc


    



Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

- [x] #739
- [ ] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:
s



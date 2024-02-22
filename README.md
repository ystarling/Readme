# Readme


1. JAVA
   - Core
     - Abstract class vs Interfaces, why and when to use? Abstract class vs Interfaces where better to use?
     - loose coupling & high cohesion
     - Equals & HashCode, hashCode & equals contract? busket 1, 2, hashcode collision.
       `if two objects equal then hashcode should be the same`, [[link](https://medium.com/coding-corpus/java-important-methods-equals-hashcode-and-compareto-6adcdf2814c3)]
     - Lambda expression, Anonymous classes
     - anonymous function, lambda, functional interface, default methods, do you know any functional methods?
     - Immutable class? class final, private final members, initialise everything in constructor, deep copy, no setters! 
     - JVM inside, class loaders, rt.jar, bootstrap. [[link](https://medium.com/geekculture/java-backend-developer-interview-questions-pt-1-10-1c74c76442bd)]
     - Funtional interfaces java, purpose, examples? single abstract method, to avoid boilerplate using anonymous classes, Consumer, Predicate, Function, Supplier. Runnable, Callable, Comparable, 
     - Garbage collector, Memory management, memory allocate. tuning GC1.
       `heap=objects.`
       `permgen(metaspace):classes, static, string pool.`
       `stack: primitive objects, references.`
       `eden space, new generation, old generation. heap max size`
       [[link](https://diptendud.medium.com/java-memory-management-interview-questions-and-answers-204d7a249019)]
     - class Objects.
   - Streams
     - Sequence of operations on objects, 
         input->intermediate operations ..filter, mapping, reducing, sorting, etc->terminal operation->output
     - aggregation functions [[link text itself](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)]
     - repeat Streams, map, multiply, reduce, groupby, summarise, max, min, Function interfaces? [[link](https://www.youtube.com/watch?v=o1H6kMlCQ74&ab_channel=Bobocode)], [[link](https://medium.com/swlh/java-collectors-and-its-20-methods-2fc422920f18)]
   - Threads
     - Singleton class
     - Thread safe, DeadLock?
     - volatile, use fast cash in memory
     - Lock interface, locking, synchronize block
     - Executors
     - Race condition. Occurs in programming when two or more execution threads modify a shared resource.
     - https://rjlfinn.medium.com/asynchronous-programming-in-java-d6410d53df4d
     - etc
   - Collections
     - LinkedList vs ArrayList, pros & cons? LinkedList vs ArrayList (size capacity 10 by default).
       - LinkedList `fast for add and remove O(1), slow access O(n).`
       - ArrayList `fast random access O(1), but slow add and delete!`
     - public interface Collection<E> extends Iterable<E>
     - thread safe Collections?
     - fast fail, fail safe
     - implement Comparable, or anonymous class Comparator
     - Iterator used for change mutable objects like created by List.of
   - Java 11 vs 17, var keyword without specifing type, Text blocks """text""", Records, S.toList() instead of S.collect(Collectors.toList())
   - GoF patterns
     - Remember most usage patterns: Strategy(lambda!), Observer, Decorator, Iterator, Builder.
     - BandOf4 patterns? what you use? Observer, Proxy, Iterator vs Iterable? Adapter, Decorator, Facade.
     - Decorator pattern(structural), decor. [[link](https://medium.com/analytics-vidhya/simplify-strategy-using-lambda-expression-40195d1445ea)]
     - https://refactoring.guru/
   - SOLID
     - Liskov = The principle defines that objects of a superclass shall be replaceable with objects of its subclasses without breaking the application. Do you know how to broke this principal in diff languages? [[link](https://softwareengineering.stackexchange.com/questions/436420/what-are-the-examples-of-breaking-liskov-substitution-principle)]
     - Dependency inversion = High level modules should not depend upon low level. Everything should be dependent on abstraction.
     - Interface sagregation = “Clients should not be forced to depend upon interfaces that they do not use.” By following this principle, you prevent bloated interfaces that define methods for multiple responsibilities. Split one interface to more with specific responsibilities.
     - why SOLID?  maintainable, understandable, and flexible, as our applications grow in size, we can reduce their complexity. Smaller, well-organized classes.
     - https://medium.com/@furkanalniak/understanding-solid-principles-in-java-code-examples-and-best-practices-f6451bb5198e
   - IntelijIDEA shortcuts repeat!
   - etc
   - Kotlin vs Java, syntax, null safety, functional programming

3. SPRING
   - Spring vs SpringBoot
   - Dependency injection?
   - SpringBoot
       - Spring bean lifecyrcle, initialization, scopes
       - inject by constructor or setter, factory method, what is the best option?
       - Stereotypes?
       - @Transactional, Proxy?
       - Spring Actuator - production ready features (health check, metrics)
       - ReflectionUtils
       - Paging, Sorting
       - @Patch, [[link](https://www.youtube.com/watch?v=UB71ARdhS78&ab_channel=AlmightyJava)]
   - Security oAuth2, basic what is it how it works internally?
   - SecurityFilterChain, Resource server, bearer tokens: jwt, opaque token. Bearer Token, basic authentication, SecurityContextHolder, 
   - etc
4. DATABASE
   - NoSql vs RDBMs, NoSQL(high velocity-speed, high handle volume data). [[link](https://www.geeksforgeeks.org/difference-between-relational-database-and-nosql/)]
   - ACID, transaction, isolation levels, anomalies, indexes?
   - what is connection pool? purpose
   - SQL queries [[link](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)]
   - sql joins, group by, avg() >, departments & employees salary [[link1](https://sqlbolt.com/)] [[link2](https://www.youtube.com/watch?v=d-SJmsgoUrw&ab_channel=CrackConcepts)]
   - SQL update script, ALTER TABLE table_name ADD column_name datatype;
   - Answer for question: How to change DB tables in the running environment? (manually without Liquibase), rolling updates
      - rolling update that doesn’t cause any downtime. [[link](https://thorben-janssen.com/update-database-schema-without-downtime/)]
      - The removal of the constraint itself is a backward-compatible operation.
      - https://habr.com/ru/articles/664028/
   - Isolation levels from lowest to highest are Read Uncommitted, Read Committed, Repeatable Read, and Serializable. [[link](https://jetherrodrigues.dev.br/transaction-management-in-the-spring-framework-996d700f1f27)], [[docker](https://youtu.be/tNk8uXLOxA8?t=499)], [[docker](https://youtu.be/4EajrPgJAk0?t=252)]
     - Read Committed = Only see data written by committed transactional.
   - Postgres default isolation level. Explain what this isolation means?
   - NoSQL learn https://www.youtube.com/watch?v=c2M-rlkkT5o&ab_channel=BroCode
4. ORM
   - JPA vs Hibernate, more then one difference?
   - Lazy loading JPA/Hibernate
   - Optimistic Lock @Version
   - How to One to One mapping?
   - Jpa entity states: New, Managed, Detached(when Session closed), Removed.
   - Cache L1, L2, query cache in JPA
   - N + 1 problem?
   - JPA relationship 1-n, n-1, @Entity, other annotation links tables? department-employee. [[link](https://medium.com/thefreshwrites/manytoone-onetomany-mapping-in-jpa-32581d3c0f8a)], [[link](https://www.baeldung.com/jpa-one-to-one)], [[link](https://www.tutorialspoint.com/jpa/jpa_entity_relationships.htm)]
   - Opimistic lock? jpa, hibernate, entity stages, detached? Transient(Created), Managed, Detached, Removed
   - Liquibase vs Flyway, changelogs. Flyway uses SQL-based migration scripts, whereas. Liquibase uses XML, YAML, or JSON to define the database changes. [[link](https://www.linkedin.com/pulse/database-migration-flyway-vs-liquibase-rafael-porto-rodrigues#:~:text=Configuration%3A%20Flyway%20follows%20a%20convention,to%20define%20the%20database%20changes.)]
   - Hibernate audited, @Audited - generate table with suffix table_aud
   - Transactional manager in Hibernate
5. REST
   - Rest vs Soap
   - Idempotent, [[link](https://restfulapi.net/idempotent-rest-apis/)]
   - Rest header, body, query parameters, content-type?
   - backward compatibility, versioning, https://www.linkedin.com/advice/0/how-do-you-design-restful-api-supports#:~:text=Backward%20compatibility%20is%20the%20ability,new%20version%20of%20the%20API.
   - client server architecture based on requests - responses, various response format, flexible, stateless (means all info that needs already in request).
   - Async Rest example [[link](https://sanketdaru.com/blog/polling-model-async-rest-spring-boot/)], [[link](https://github.com/sanketdaru/async-jobs-over-restful-api)], [[link2](https://medium.com/@bubu.tripathy/a-beginners-guide-to-async-processing-in-a-spring-boot-application-a4c785a992f2)], [[link2](https://jackynote.medium.com/optimizing-spring-boot-asynchronous-processing-a-comprehensive-guide-f9437ce3d14d)]
6. Microservices
   - Event driven communication vs REST, when to use?
      - Event-garantie that message deliveried to consumer, no downtime, no need to wait for message.
      - Rest-has address which service you
      - Asynchronous and nonblocking
      - what usually can happen with messages, can some messages not reach, or duplicate, if so how to deal with it?
      - Rest - client-server communication,
      - ED - has more consumers, no single point of failure
   - Monolithic - all functionalities tightly coupled in single application, simplicity, easy deployment, but lack of scalability and fault tolerance. It may become complex and difficult to maintain as the system grow.
   - Microservices - breaking down the system into independent and loosely coupled services, each responsible for specific function. It offers scalability, fault tolerance, flexibility in technology choices. Hovewer is introduces complexity in inter-service communication and deployment. 
   - how did you specify the boundaries of your microservices. [[link](https://blog.bitsrc.io/how-to-choose-microservices-boundaries-5c68b0b1af24)], [[link](https://nathanpeck.com/making-microservice-boundaries-that-you-wont-regret/)], [[link](https://codeburst.io/microservice-boundaries-five-characteristics-to-guide-your-design-89312b65cc27)], [[link](https://www.linkedin.com/advice/0/how-do-you-identify-boundaries-microservices-from)], [[link](https://www.linkedin.com/advice/3/how-do-you-set-microservice-boundaries-skills-software-design#:~:text=One%20of%20the%20first%20steps,inventory%20management%2C%20or%20payment%20processing.)], [[link](https://www.oreilly.com/library/view/microservices-up-and/9781492075448/ch04.html)], [[link](https://www.lokajittikayatray.com/post/how-to-define-your-microservices-correctly)]
   - fault tolerant approach, Bulkhead pattern, Circuit Breaker. [[link](https://www.codecentric.de/wissens-hub/blog/resilience-design-patterns-retry-fallback-timeout-circuit-breaker)], [[link](https://www.youtube.com/watch?v=ADHcBxEXvFA&ab_channel=DefogTech)], [[link](https://quickbooks-engineering.intuit.com/resiliency-two-alternatives-for-fault-tolerance-to-deprecated-hystrix-de58870a8c3f)]
   - Resilience design patterns: retry, fallback, timeout, circuit breaker.
   - https://www.codecentric.de/wissens-hub/blog/resilience-design-patterns-retry-fallback-timeout-circuit-breaker
   - Service discovery is a mechanism by which services discover each other dynamically without the need for hard coding IP addresses or endpoint configuration.
   - https://blog.bitsrc.io/how-to-choose-microservices-boundaries-5c68b0b1af24
   - [kafka](https://medium.com/@shubhamkumbhar787/example-of-implementing-kafka-in-a-java-spring-boot-application-e271740df5ca)
   - Api gateway? - An API gateway is a component of the app-delivery infrastructure that sits between clients and services and provides centralized handling of API communication between them. It also delivers security, policy enforcement, and monitoring and visibility across on-premises, multi-cloud, and hybrid environments.
   - Service dicovery(ex. Load Balancer) - automatically detecting devices and services on a computer network.
7. Docker
   - What is docker container itself? [[link](https://www.docker.com/resources/what-container/#:~:text=A%20Docker%20container%20image%20is,tools%2C%20system%20libraries%20and%20settings.)]
      - A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
   - Docker networking?, Docker swarm, compose? how to expose or open service connection outside?
      - https://docs.docker.com/get-started/08_using_compose/
      - https://youtu.be/tNk8uXLOxA8?t=499
      - [[crazy](https://www.youtube.com/watch?v=bKFMS5C4CG0&ab_channel=NetworkChuck)]
   - https://docs.docker.com/engine/swarm/
   - https://www.youtube.com/watch?v=i7ABlHngi1Q&ab_channel=TravisMedia
   - https://medium.com/@bharathy.poovalingam/spring-boot-with-docker-d4129a353f87
   - 
8. K8s
   - K8s question: if your service in K8s is down what is your step to do? service describe, readiness probe.
    Read Troubleshooting applications kubernetes.io , startup, liveness, readness probe, describe pod, [[link](https://stackoverflow.com/questions/65858309/why-do-i-need-3-different-kind-of-probes-in-kubernetes-startupprobe-readinessp)]
   - deployment kind, services, Deploy the node-based Agent
   - kubectl, kebelet, manifest, agent deployment, cluster, node, pod, container
   - A pod typically includes several containers, which together form a functional unit. A Pod is is the smallest unit that can be deployed and managed by Kubernetes.
   - kubernetes monitoring tools: Grafana, ELK, Datadog, New Relic, K8s Dashboards,
   - Kubernetes has progressively rolled out support for auto-scaling with metrics besides CPU utilization, such as memory consumption. Kubernetes uses labels to identify which pods belong to a particular service, you can use these labels to aggregate data from individual pods and containers to get continuous visibility into services and other Kubernetes objects.
   - Kubernetes is an open-source container orchestration system for automating deployment, scaling, and management of containerized applications. Kubernetes monitoring refers to the practice of monitoring the health and performance of a Kubernetes cluster or deployment. Kubernetes monitoring typically involves collecting metrics and logs from various components of the Kubernetes cluster, including nodes, pods, and services, and analyzing them to gain insights into the cluster’s behavior. Some of the key metrics that are commonly monitored in a Kubernetes cluster include CPU usage, memory usage, network traffic, and disk usage.
   - Historical data can be used to identify trends and patterns and to perform retrospective analysis to understand and diagnose issues that occurred in the past. It can also be used to provide context and benchmarking information for future planning and decision-making.
It is important to establish a data retention policy that defines how long data should be kept, where it should be stored, and how it should be managed. This policy should consider factors such as data volume, access requirements, and compliance regulations, and should be aligned with the overall data management strategy for the organization. The data should be organized and indexed to enable easy searching and retrieval.
   - One of the main objectives of monitoring Kubernetes is to ensure that applications are performing optimally and meeting user expectations.
   - https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-monitoring/
   - delete minikube https://gist.github.com/rahulkumar-aws/65e6fbe16cc71012cef997957a1530a3
   - etc
9. Clean Code and Uncle Bob, Craftmanship
   - code refactoring how to? Better organization, Less code duplication, Easier maintenance, understandable, readable, structured, documented
   - code challenge -thinking simply not complex. Rest apis> dont use Feign! use WebClient!
   - time complexity Big On, [[link](https://aaronice.gitbook.io/lintcode/linked_list)], [[link](https://flexiple.com/algorithms/big-o-notation-cheat-sheet/)]
   - https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html
   - TDD
   - Naming unit test. [UnitOfWork_StateUnderTest_ExpectedBehavior], Sum_NegativeNumberAs1stParam_ExceptionThrown().
   - UML, [[link](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-aggregation-vs-composition/#:~:text=Aggregation%20implies%20a%20relationship%20where,exist%20independent%20of%20the%20parent)].
      - Composition =has-a relationship between objects. relationship where the child cannot exist independent of the parent.
      - Aggregation= relationship where the child can exist independently of the parent.
   - DDD [[link](https://medium.com/microtica/the-concept-of-domain-driven-design-explained-3184c0fd7c3f)]
      - The primary focus of the project is the core domain and domain logic. A domain consists of several subdomains that refer to different parts of the business logic. For example, an online retail store could have a product catalog, inventory, and delivery as its subdomains. Bounded contexts actually represent boundaries in which a certain subdomain is defined and applicable. specific bounded context, configuration, and dependencies.
      - Domain-driven design is a software engineering approach to solving a specific domain model. The solution circles around the business model by connecting execution to the key business principles.
Common terminology between the domain experts and the development team includes domain logic, subdomains, bounded contexts, context maps, domain models, and ubiquitous language as a way of collaborating and improving the application model and solving any domain-related challenges.
      - Microservices offer some serious advantages over traditional architectures, providing scalability, accessibility, and flexibility. Moreover, this approach keeps developers focused as each microservice is a loosely coupled service with a single idea of accountability.
      - subject, 
10. Design
    - Spotify, music streaming [[link](https://www.youtube.com/watch?v=_K-eupuDVEc&ab_channel=IGotAnOffer%3AEngineering)]
    - Amazon System Design Interview: Design Parking Garage, [[link](https://www.youtube.com/watch?v=NtMvNh0WFVM&ab_channel=Exponent)]
    - Design Url Shortening Service, [[link](https://youtu.be/eCLqmPBIEYs?t=709)], [[link](https://www.designgurus.io/blog/url-shortening)], [[link](https://www.geeksforgeeks.org/system-design-url-shortening-service/)], [[link](https://medium.com/@sandeep4.verma/system-design-scalable-url-shortener-service-like-tinyurl-106f30f23a82)], [[link](https://www.youtube.com/watch?v=CihfMVePlcQ&ab_channel=CachedInsights)]
    - etc
    - https://www.designgurus.io/blog/step-by-step-guide
11. CI/CD
    - feature toggle, how to manage if one main branch
    - merge vs rebase
    - git flow? what is trunk base? main branch etc.
    - what is trunc base strategy?
    - CI/CD how it? ArgoCD, Octopus deploy, GitLab
    - Github Actions, [[link](https://docs.github.com/en/actions/quickstart)], [[link](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)], [[youtube](https://www.youtube.com/watch?v=3mzQRJY1GVE&ab_channel=TECHSCHOOL)], [[listen!](https://www.youtube.com/watch?v=R8_veQiYBjI&ab_channel=TechWorldwithNana)]
12. Linux
    - how to remote connect in Linux/Unix, SSH command? most common list commands
    - 
13. Agile
    - How are you start working on task? Jira, Task, Epic, User story, Scram, Kanban. Retrospective, Backlog, Sprint planning, short iteration.
    - what was your last task you working on?
    - Scrum pocker
    - Squads, [[link](https://engineering.atspotify.com/2014/03/spotify-engineering-culture-part-1/)], [[link](https://vimeo.com/85490944)]
14. Code challenges
    - https://www.linkedin.com/pulse/coding-challenges-struggle-real-solutions-here-owoseni-boluwatife-ss0jf/
    - https://leanylabs.com/blog/senior-vs-middle-vs-junior-developers/
    - etc
15. Domains
    - EV Charging, OCPP & OCPI
    - [[link](https://www.linkedin.com/pulse/3-tricks-implement-smart-charging-ocpp-16-joachim-lohse/)], [[link](https://www.linkedin.com/pulse/seamless-ev-charging-roaming-exploring-ocpi-protocol-fedotov/)], [[link](https://medium.com/@yocharge2022/open-charge-point-protocol-ocpp-a-complete-guide-cfcfb57c4108)]
    - Through OCPP, the Central System can monitor and manage charging sessions, collect data on energy consumption, and handle billing information. 
    - Sending commands to CPO
    - etc
    - etc
16. Questions & Answers
    - Can you tell me more about the team?
    - What would a typical day for me in this role look like?
    - What are the biggest challenges that I might face in this position?
    - We appreciate any tools that increase our productivity.
    - As we have 8 separate teams always dedicated always PO, 
    - Our daily work is driven by Agile values, be focus, committed,
    - Each team works transparently making sure that all progress and knowledge shared.
    - 
18. etc

    



Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

- [x] #739
- [ ] https://github.com/octo-org/octo-repo/issues/740
- [ ] Add delight to the experience when all tasks are complete :tada:
s



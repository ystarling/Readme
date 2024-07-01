# Readme


1. JAVA
   - Core
     - Abstract class vs Interfaces, why and when to use? Abstract class vs Interfaces where better to use?
       - As a general rule, you should use an abstract class when creating a base class that needs to be inherited by other classes in a class hierarchy. If you need to define a behavior that can be implemented by multiple unrelated classes, you should use an interface.
       - Abstract classes are particularly useful when you need to define a hierarchy of classes that share common attributes and behaviors.
       - For example, interfaces are an excellent choice when a class needs to inherit behavior from multiple sources.
     - Loose coupling & high cohesion, tight coupling
     - Equals & HashCode, hashCode & equals contract? bucket 1, 2, hashcode collision.
       `if two objects equal then hashcode should be the same`, [[link](https://medium.com/coding-corpus/java-important-methods-equals-hashcode-and-compareto-6adcdf2814c3)]
     - Lambda expression, Anonymous classes  
     - anonymous function, lambda, functional interface, default methods, do you know any functional methods?  
     - Funtional interfaces java, purpose, examples? single abstract method, to avoid boilerplate using anonymous classes, Consumer, Predicate, Function, Supplier. Runnable, Callable, Comparable,  
     - Immutable class? class final, private final members, initialise everything in constructor, deep copy, no setters! [[link](https://systemweakness.com/immutable-objects-in-java-using-builder-pattern-with-functional-interface-fa8885771cda)], [[records, withers, builders](https://www.sonarsource.com/blog/builders-withers-and-records-java-s-path-to-immutability/)], by reflection
     - JVM inside, class loaders, rt.jar, bootstrap. [[link](https://medium.com/geekculture/java-backend-developer-interview-questions-pt-1-10-1c74c76442bd)],
       [[gc](https://stackify.com/what-is-java-garbage-collection/)]
     - JVM parameters  
       ```
          -XX:MaxPermSize =java.lang.OutOfMemoryError
          -Xms, Xmx
          -Xss =java.lang.StackOverFlowError
       ``` 
     - Garbage collector, Memory management, memory allocate. tuning GC1.  
       `heap=objects.`  
       `permgen(metaspace):classes, methods, static, string pool, metadata`  
       `stack: primitive objects, references.`  
       `eden space, new generation, old generation. heap max size`  
       [[link](https://diptendud.medium.com/java-memory-management-interview-questions-and-answers-204d7a249019)]  
       arguments: -XX:+PrintGCDetails. -XX:+UseSerialGC -Xms1024m -Xmx1024m -verbose:gc [[verbose](https://www.baeldung.com/java-verbose-gc)]  
       tuning JVM: visualVM, jmap -histo:live 7544, jConsole, Profiling tools intellij-idea-profiler/
       [[dzone](https://dzone.com/articles/java-memory-management)]  
       finalize(), gc()
     - The Java garbage collection process uses a mark-and-sweep algorithm. The Java garbage collection process uses a mark-and-sweep algorithm. Here’s how that works:
    There are two phases in this algorithm: mark followed by sweep.
    When a Java object is created in the heap, it has a mark bit that is set to 0 (false).
    During the mark phase, the garbage collector traverses object trees starting at their roots. When an object is reachable from the root, the mark bit is set to 1 (true). Meanwhile, the mark bits for unreachable objects is unchanged.
    During the sweep phase, the garbage collector traverses the heap, reclaiming memory from all items with a mark bit of 0 (false).
     - Short-lived objects tend to be collected more frequently in the young generation (newly created objects), while long-lived objects are managed in the old generation.  
     - What is it memory leak, how to detect?  https://www.javamadesoeasy.com/2017/03/top-30-jvmjava-virtual-machine.html?m=1
     - class Objects.
     - weak, strong, soft, phantom references: [[link](https://www.baeldung.com/java-reference-types)]  
       strong reference -sitting all time.  
       weak reference -sitting on demand gc, once need memory.  
   - Streams
     - Sequence of operations on objects, 
         input->intermediate operations ..filter, mapping, reducing, sorting, etc->terminal operation->output
     - aggregation functions [[link text itself](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)]
     - repeat Streams, map, multiply, reduce, groupby, summarise, max, min, Function interfaces? [[link](https://www.youtube.com/watch?v=o1H6kMlCQ74&ab_channel=Bobocode)], [[link](https://medium.com/swlh/java-collectors-and-its-20-methods-2fc422920f18)], [[github](https://github.com/bobocode-projects/java-core-exercises/tree/exercise/completed)], [[CrazyStreams.java](https://github.com/bobocode-projects/java-core-exercises/blob/exercise/completed/crazy-streams/src/main/java/com.bobocode/CrazyStreams.java)]  
     - examples
       ```
          Map<String, Long> groupByGender = employees.stream()
             .collect(Collectors.groupingBy(Emloyee::getGender, Collectors.counting()));
       ```
     - https://4comprehension.com/the-ultimate-guide-to-the-java-stream-api-groupingby-collector/
     - groupingBy, https://medium.com/@dudkamv/java-streams-and-collectors-a-comprehensive-guide-3ce4cd1b311f
       ```
          List<Employee> employees = // Assume a list of employees
          Map<Department, Double> averageSalaryByDepartment = employees.stream()
             .collect(Collectors.groupingBy(Employee::getDepartment,
                                   Collectors.averagingDouble(Employee::getSalary)));
       ```
   - Threads
     - Singleton class, [[thread safety singleton](https://www.initgrep.com/posts/design-patterns/thread-safety-in-java-singleton-pattern)]
       using Enum, Nested class, Double-Checked Locking,
       ```
         public class DoubleCheckedLockingSingleton {
             private static volatile DoubleCheckedLockingSingleton instance;
         
             private DoubleCheckedLockingSingleton() { }
         
             public static DoubleCheckedLockingSingleton getInstance() {
                 if (instance == null) {
                     synchronized (DoubleCheckedLockingSingleton.class) {
                         if (instance == null) {
                             instance = new DoubleCheckedLockingSingleton();
                         }
                     }
                 }
                 return instance;
             }
         }
       ```
     - Thread safe, DeadLock?
     - volatile, use fast main memory, shared and visible for threads
     - Lock interface, locking, synchronize block
     - Executors
       The java.util.concurrent.Executors provide factory methods that are being used to create ThreadPools of worker threads. Threads get free, they pick up the next task from this Queue.  
       ```
         SingleThreadExecutor
         FixedThreadPool(n)+
         CachedThreadPool
         ScheduledExecutor
         
         ExecutorService executor = Executors.newSingleThreadExecutor();
         ExecutorService fixedPool = Executors.newFixedThreadPool(2);
         ExecutorService executorService = Executors.newCachedThreadPool();
         ScheduledExecutorService scheduledExecService = Executors.newScheduledThreadPool(1);
         
         class Task implements Callable<String>
         Future<String> result = executorService.submit(callableTask);
       ```
     - Race condition. Occurs in programming when two or more execution threads modify a shared resource.
     - https://rjlfinn.medium.com/asynchronous-programming-in-java-d6410d53df4d
     - ThreadLocal, ConcurrentHashMap, BlockingQueue, Collections.synchronizedCollection(new ArrayList<>()); Collections.synchronizedList(), atomic wrappers AtomicInteger.  
       Atomic classes allow us to perform atomic operations, which are thread-safe, without using synchronization.  
     - Concurrent Random Numbers, java.util.concurrent.ThreadLocalRandom , Math.random(),
        ```
        int[] array = {1, 2, 3, 4, 5, 6};
        CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();
        IntStream.of(array).parallel().forEach(list::add);
        ```  
   - Collections
     - LinkedList vs ArrayList, pros & cons? LinkedList vs ArrayList (size capacity 10 by default).
       - LinkedList `fast for add and remove O(1), slow access O(n).`
       - ArrayList `fast random access O(1), but slow add and delete!`
       - Linked lists, a versatile data structure, consist of nodes, each holding data and a reference to the next node in the sequence.
     - public interface Collection<E> extends Iterable<E>
     - thread safe Collections?
     - fast fail, fail safe
     - implement Comparable, or anonymous class Comparator.
       Comparable is meant for objects with natural ordering which means the object itself must know how it is to be ordered. If any class implements Comparable interface in Java then collection of that object either List or Array can be sorted automatically by using Collections.sort() or Arrays.sort() method and objects will be sorted based on there natural order defined by CompareTo method.
       ```
          class Movie implements Comparable<Movie> {
             private int year;
             public int compareTo(Movie m)
             {
                 return this.year - m.year;
             }
          }
          
          class NameCompare implements Comparator<Movie> {
             public int compare(Movie m1, Movie m2)
             {
                 return m1.getName().compareTo(m2.getName());
             }
          }
      
          NameCompare nameCompare = new NameCompare();
          Collections.sort(list, nameCompare);
       ```
     - Iterator used for change mutable objects like created by List.of
     - HashSet vs TreeSet, [[link](https://www.javatpoint.com/hashset-vs-treeset-java)]
     - HashMap uses the array of Nodes, capacity=16, loadfactor=0.75.
       HashMap offers O(1) insertion and retrieval time.  
       ```
          transient Node<K,V>[] table; 
          class Node<K,V> {
             final int hash;
             final K key;
             V value;
             Node<K,V> next;
             // Some utility methods
         }
       ```  
       [[link](https://www.interviewcake.com/concept/java/hash-map)]
      - TreeMap offers O(log N) insertion and retrieval time. TreeMap implements Red-Black Tree. TreeMap sorts all its entries according to their natural ordering. For an integer, this would mean ascending order and for strings, alphabetical order.
      - Binary Search and Limitations
        Binary search, a more efficient algorithm, only works on sorted lists.  
        Binary Search is divide and conquer approach to search an element from the list of sorted element. In Linked List we can do binary search but it has time complexity O(n) that is same as what we have for linear search which makes Binary Search inefficient to use in Linked List.  
      - 
   - enum,
     ```
     public static Month findByValue(String value) {
        return Arrays.stream(values()).filter(month -> month.getValue().equalsIgnoreCase(value)).findFirst()
                       .orElseThrow(IllegalArgumentException::new);
     }
     ``` 
   - Java 11 vs 17, var keyword without specifing type, Text blocks """text""", Records, S.toList() instead of S.collect(Collectors.toList())
   - GoF patterns
     - Remember most usage patterns: Observer, Decorator, Iterator, Builder, Strategy(lambda!)
     - BandOf4 patterns? what you use? Observer, Proxy, Iterator vs Iterable? Adapter, Decorator, Facade.
     - Decorator pattern(structural), decor. [[link](https://medium.com/analytics-vidhya/simplify-strategy-using-lambda-expression-40195d1445ea)]
     - https://refactoring.guru/
     - Why Singleton is anti-pattern? [[link](https://medium.com/aia-sg-techblog/why-singleton-pattern-is-considered-as-anti-design-pattern-c81dd8b7e757)]
Violating Single Responsibility Principle :
Single Responsibility Principle states that every class should have a single task to do.
In case of Singleton class it will have two responsibility one to create an instance and other to do the actual task.
       Breaks the Open Closed Principle :
Open Closed Principle can be explained in a single statement “Open for Extension closed for Modification”.
Singleton class always returns its own instance and is never open for extension.
Dependency Inversion Violation: Dependency Inversion Principle ensures that change in low level details should not impact the high level abstraction.
Any low level changes in singleton pattern system we need to do change the Singleton class.
Difficult to Test. Tight Coupling.
     - [[strategy pattern](https://www.devdiaries.net/blog/Java-Strategy-Design-Pattern-By-Examples/)]
     - etc
   - SOLID
     - Liskov = The principle defines that objects of a superclass shall be replaceable with objects of its subclasses without breaking the application. Do you know how to broke this principal in diff languages? [[link](https://softwareengineering.stackexchange.com/questions/436420/what-are-the-examples-of-breaking-liskov-substitution-principle)]
     - Dependency inversion = High level modules should not depend upon low level. Everything should be dependent on abstraction.
     - Interface sagregation = “Clients should not be forced to depend upon interfaces that they do not use.” By following this principle, you prevent bloated interfaces that define methods for multiple responsibilities. Split one interface to more with specific responsibilities.
     - why SOLID?  maintainable, understandable, and flexible, as our applications grow in size, we can reduce their complexity. Smaller, well-organized classes.
     - https://medium.com/@furkanalniak/understanding-solid-principles-in-java-code-examples-and-best-practices-f6451bb5198e
     - [[github](https://github.com/Java-Techie-jt/solid-principles-example/tree/main)], [[link](https://www.youtube.com/watch?v=BM_lSZPMClo&ab_channel=JavaTechie)], [[link](https://www.youtube.com/watch?v=HoA6aZPR5K0&ab_channel=Geekific)], [[link](https://www.youtube.com/watch?v=_jDNAf3CzeY&ab_channel=Amigoscode)]
     - etc
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
   - Authentication is a process for verifying identity. It answers the question “Is this person who they claim to be?‚ (username/password). Authentication verifies who the user is. Authentication works through passwords, one-time pins, biometric information, and other information provided or entered by the user.
   - Authorization gives the user permission to access specific resources. It answers the question “What is this authenticated person allowed to do?‚(Roles)
Authorization determines what resources a user can access.
   - RestTemplate [[link](https://hellokoding.com/spring-resttemplate-timeout/)]
   - etc
4. DATABASE
   - NoSql vs RDBMs, NoSQL(high velocity-speed, high handle volume data). [[link](https://www.geeksforgeeks.org/difference-between-relational-database-and-nosql/)]
   - ACID, transaction, isolation levels, anomalies, indexes?
   - what is connection pool? purpose
   - SQL queries [[link](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)], [[sqlbolt](https://sqlbolt.com/lesson/select_queries_with_aggregates)]  
     ```
        For each role, find the average number of years employed by employees in that role
         select role, AVG(Years_employed) FROM Employees GROUP BY role;
         
        Find the total number of employee years worked in each building ✓
         select building, sum(Years_employed) from employees group by building;
         
        Find the number of Employees of each role in the studio 
         SELECT role, count() as count FROM employees group by role;
         
        Find the total number of years employed by all Engineers ✓
         SELECT sum(Years_employed) FROM employees where role='Engineer';
         
        Find the number of movies each director has directed ✓
         SELECT director, COUNT(id) as Num_movies_directed
         FROM movies
         GROUP BY director;
         
        Find the total domestic and international sales that can be attributed to each director ✓
         SELECT Movies.director, sum(Domestic_sales +International_sales)
         FROM Boxoffice
          JOIN Movies
            ON Movies.Id = Boxoffice.Movie_id
          GROUP BY Director;
         
         /////
         SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
         FROM mytable
          JOIN another_table
            ON mytable.column = another_table.column
          WHERE constraint_expression
          GROUP BY column
          HAVING constraint_expression
          ORDER BY column ASC/DESC
          LIMIT count OFFSET COUNT;
         //
   
        SELECT Director, AVG(Boxoffice.Rating) as rating FROM movies 
         LEFT JOIN Boxoffice ON movies.id=Boxoffice.Movie_id GROUP BY movies.Director 
            HAVING rating > 8 ORDER BY rating DESC;
   
         //
        Find Second Highest Salary in SQL:
           SELECT DISTINCT salary 
           FROM employee 
           ORDER BY salary DESC LIMIT 1,1;
      
           SELECT MAX(SALARY) FROM employees 
           WHERE SALARY < (SELECT MAX(SALARY) FROM employees);
     ```  
   - sql joins, group by, avg() >, departments & employees salary [[link1](https://sqlbolt.com/)] [[link2](https://www.youtube.com/watch?v=d-SJmsgoUrw&ab_channel=CrackConcepts)]
     ```
     Tables: [Student] -> [student_course] <- [course]
      SELECT
        student.first_name,
        student.last_name,
        course.name
      FROM student
      JOIN student_course
        ON student.id = student_course.student_id
      JOIN course
        ON course.id = student_course.course_id;
     ```
   - SQL update script, ALTER TABLE table_name ADD column_name datatype;
     ```
     INSERT INTO boxoffice VALUES (4, 8.7, 340000000, 270000000);
     UPDATE movies SET director = "John Lasseter" WHERE id = 2;
     DELETE FROM movies where year < 2005;
      
     Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
     ALTER TABLE Movies
     ADD COLUMN Aspect_ratio FLOAT DEFAULT 2.39;
      
     DROP TABLE IF EXISTS mytable;
     ```
   - Liquibase uses the DATABASECHANGELOGLOCK (DBCLL) table to ensure only one instance of Liquibase runs at a time. If the table does not exist in the database, Liquibase creates one automatically. When you make a database update, Liquibase reads from the DATABASECHANGELOG table to determine which changesets need to run.    
   - Answer for question: How to change DB tables in the running environment? (manually without Liquibase), rolling updates
      - rolling update that doesn’t cause any downtime. [[link](https://thorben-janssen.com/update-database-schema-without-downtime/)]
      - The removal of the constraint itself is a backward-compatible operation.
      - https://habr.com/ru/articles/664028/
   - Isolation levels from lowest to highest are: Read Uncommitted, Read Committed, Repeatable Read, and Serializable. [[link](https://jetherrodrigues.dev.br/transaction-management-in-the-spring-framework-996d700f1f27)], [[docker](https://youtu.be/tNk8uXLOxA8?t=499)], [[docker](https://youtu.be/4EajrPgJAk0?t=252)]
     - Read Committed = Only see data written by committed transactional.
   - Postgres default isolation level. Read-committed. Explain what this isolation means?
   - NoSQL learn https://www.youtube.com/watch?v=c2M-rlkkT5o&ab_channel=BroCode
4. ORM
   - JPA vs Hibernate, more then one difference?
   - Lazy loading JPA/Hibernate, Cascading
   - Optimistic Lock @Version
   - How to One to One mapping?
   - Jpa entity states: New, Managed, Detached(when Session closed), Removed.
   - Cache L1, L2, query cache in JPA
   - N + 1 problem?
   - JPA relationship 1-n, n-1, @Entity, other annotation links tables? department-employee. [[link](https://medium.com/thefreshwrites/manytoone-onetomany-mapping-in-jpa-32581d3c0f8a)], [[link](https://www.baeldung.com/jpa-one-to-one)], [[link](https://www.tutorialspoint.com/jpa/jpa_entity_relationships.htm)]
   - Opimistic lock? jpa, hibernate, entity stages, detached? Transient(Created), Managed, Detached, Removed
   - Liquibase vs Flyway, changelogs. Flyway uses SQL-based migration scripts, whereas. Liquibase uses XML, YAML, or JSON to define the database changes. [[link](https://www.linkedin.com/pulse/database-migration-flyway-vs-liquibase-rafael-porto-rodrigues#:~:text=Configuration%3A%20Flyway%20follows%20a%20convention,to%20define%20the%20database%20changes.)]
   - Hibernate audited, @Audited - generate table with suffix table_aud
   - Transactional manager in Hibernate, other vendors, @EnableTransactionManagement, PlatformTransactionManager, JpaTransactionManager
   - @Modify, safety update or delete native queries
5. REST
   - Rest vs Soap
   - Idempotent, [[link](https://restfulapi.net/idempotent-rest-apis/)], POST and PATCH are generally non-idempotent.
   - Rest header, body, query parameters, content-type? Map<String, String>
   - backward compatibility, versioning, https://www.linkedin.com/advice/0/how-do-you-design-restful-api-supports#:~:text=Backward%20compatibility%20is%20the%20ability,new%20version%20of%20the%20API.
   - client server architecture based on requests - responses, various response format, flexible, stateless (means all info that needs already in request).
   - Async Rest example [[link](https://sanketdaru.com/blog/polling-model-async-rest-spring-boot/)], [[link](https://github.com/sanketdaru/async-jobs-over-restful-api)], [[link2](https://medium.com/@bubu.tripathy/a-beginners-guide-to-async-processing-in-a-spring-boot-application-a4c785a992f2)], [[responsiveness](https://jackynote.medium.com/optimizing-spring-boot-asynchronous-processing-a-comprehensive-guide-f9437ce3d14d)] [[link](https://www.javacodegeeks.com/2016/06/java-8-completablefuture-vs-parallel-stream.html)]
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
     [[link](https://aws.amazon.com/compare/the-difference-between-monolithic-and-microservices-architecture/)] 
   - how did you specify the boundaries of your microservices. [[link](https://blog.bitsrc.io/how-to-choose-microservices-boundaries-5c68b0b1af24)], [[link](https://nathanpeck.com/making-microservice-boundaries-that-you-wont-regret/)], [[link](https://codeburst.io/microservice-boundaries-five-characteristics-to-guide-your-design-89312b65cc27)], [[link](https://www.linkedin.com/advice/0/how-do-you-identify-boundaries-microservices-from)], [[link](https://www.linkedin.com/advice/3/how-do-you-set-microservice-boundaries-skills-software-design#:~:text=One%20of%20the%20first%20steps,inventory%20management%2C%20or%20payment%20processing.)], [[link](https://www.oreilly.com/library/view/microservices-up-and/9781492075448/ch04.html)], [[link](https://www.lokajittikayatray.com/post/how-to-define-your-microservices-correctly)]
   - fault tolerant approach, Bulkhead pattern, Circuit Breaker. [[link](https://www.codecentric.de/wissens-hub/blog/resilience-design-patterns-retry-fallback-timeout-circuit-breaker)], [[link](https://www.youtube.com/watch?v=ADHcBxEXvFA&ab_channel=DefogTech)], [[link](https://quickbooks-engineering.intuit.com/resiliency-two-alternatives-for-fault-tolerance-to-deprecated-hystrix-de58870a8c3f)]
   - Resilience design patterns: retry, fallback, timeout, circuit breaker. [[link](https://api7.ai/blog/10-common-api-resilience-design-patterns)], [[link](https://www.linkedin.com/pulse/top-15-proven-patterns-resilient-software-design-deepak-gupta-anrnc/)], [[link](https://medium.com/garantibbva-teknoloji/applying-the-five-most-used-resiliency-patterns-using-resilience4j-with-spring-boot-1cc695988d)], [[link](https://quickbooks-engineering.intuit.com/resiliency-two-alternatives-for-fault-tolerance-to-deprecated-hystrix-de58870a8c3f)]
   - https://www.codecentric.de/wissens-hub/blog/resilience-design-patterns-retry-fallback-timeout-circuit-breaker
   - Service discovery is a mechanism by which services discover each other dynamically without the need for hard coding IP addresses or endpoint configuration.
   - https://blog.bitsrc.io/how-to-choose-microservices-boundaries-5c68b0b1af24
   - [kafka](https://medium.com/@shubhamkumbhar787/example-of-implementing-kafka-in-a-java-spring-boot-application-e271740df5ca)
   - API Gateway? - An API gateway is a component of the app-delivery infrastructure that sits between clients and services and provides centralized handling of API communication between them. It also delivers security, policy enforcement, and monitoring and visibility across on-premises, multi-cloud, and hybrid environments.
     The API gateway intercepts all incoming requests and sends them through the API management system, which handles a variety of necessary functions.
Exactly what the API gateway does will vary from one implementation to another. Some common functions include authentication, routing, rate limiting, billing, monitoring, analytics, policies, alerts, and security.  
   - Service dicovery(ex. Load Balancer) - automatically detecting devices and services on a computer network.
   - Load balancer - distribute the workload between different servers or applications, network traffic across a group of backend servers. Load balancers are used to distribute capacity during peak traffic times, and to increase reliability of applications.
   - Distributed antipatterns, [[link](https://blog.bitsrc.io/10-microservice-anti-patterns-278bcb7f385d)]
   - Saga, Choreography: [[link](https://www.youtube.com/watch?v=6O5iJ7PKUhs)]
   - In Onion architecture everything split by layers, core is your model, then repository, service layer . All 3 layers are abstraction or interfaces. Then other layers infrastructure, controllers is concrete realisations. Dependency inversion principle and dependency injection widely use.
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
   - https://docs.docker.com/engine/swarm/raft/
   - 
8. K8s
   - K8s question: if your service in K8s is down what is your step to do? service describe, readiness probe.
    Read Troubleshooting applications kubernetes.io , startup, liveness, readness probe, describe pod, [[link](https://stackoverflow.com/questions/65858309/why-do-i-need-3-different-kind-of-probes-in-kubernetes-startupprobe-readinessp)]
   - deployment kind, services, Deploy the node-based Agent
   - kubectl, kebelet, manifest, agent deployment, cluster, node, pod, container
   - A pod typically includes several containers, which together form a functional unit. A Pod is the smallest unit that can be deployed and managed by Kubernetes.
   - kubernetes monitoring tools: Grafana, ELK, Datadog, New Relic, K8s Dashboards,
   - Kubernetes has progressively rolled out support for auto-scaling with metrics besides CPU utilization, such as memory consumption. Kubernetes uses labels to identify which pods belong to a particular service, you can use these labels to aggregate data from individual pods and containers to get continuous visibility into services and other Kubernetes objects.
   - Kubernetes is an open-source container orchestration system for automating deployment, scaling, and management of containerized applications. Kubernetes monitoring refers to the practice of monitoring the health and performance of a Kubernetes cluster or deployment. Kubernetes monitoring typically involves collecting metrics and logs from various components of the Kubernetes cluster, including nodes, pods, and services, and analyzing them to gain insights into the cluster’s behavior. Some of the key metrics that are commonly monitored in a Kubernetes cluster include CPU usage, memory usage, network traffic, and disk usage.
   - Historical data can be used to identify trends and patterns and to perform retrospective analysis to understand and diagnose issues that occurred in the past. It can also be used to provide context and benchmarking information for future planning and decision-making.
It is important to establish a data retention policy that defines how long data should be kept, where it should be stored, and how it should be managed. This policy should consider factors such as data volume, access requirements, and compliance regulations, and should be aligned with the overall data management strategy for the organization. The data should be organized and indexed to enable easy searching and retrieval.
   - One of the main objectives of monitoring Kubernetes is to ensure that applications are performing optimally and meeting user expectations.
   - https://www.aquasec.com/cloud-native-academy/kubernetes-101/kubernetes-monitoring/
   - delete minikube https://gist.github.com/rahulkumar-aws/65e6fbe16cc71012cef997957a1530a3
   - [[Deployment vs StatefulSet](https://www.youtube.com/watch?v=pPQKAR1pA9U&ab_channel=TechWorldwithNana)], [[Helm](https://www.youtube.com/watch?v=-ykwb1d0DXU&ab_channel=TechWorldwithNana)], [[Pods and Containers](https://www.youtube.com/watch?v=5cNrTU6o3Fw&ab_channel=TechWorldwithNana)], [[Terraform](https://www.youtube.com/watch?v=l5k1ai_GBDE&ab_channel=TechWorldwithNana)], [[Kubernetes Services](https://www.youtube.com/watch?v=T4Z7visMM4E&ab_channel=TechWorldwithNana)], [[Ingress](https://www.youtube.com/watch?v=80Ew_fsV4rM&ab_channel=TechWorldwithNana)], [[Microservices](https://www.youtube.com/watch?v=rv4LlmLmVWk&ab_channel=TechWorldwithNana)], [[Kubernetes components](https://www.youtube.com/watch?v=Krpb44XR0bk&ab_channel=TechWorldwithNana)], [[K8s](https://www.youtube.com/watch?v=VnvRFRk_51k&ab_channel=TechWorldwithNana)], [[K8s Hands On](https://www.youtube.com/watch?v=r2zuL9MW6wc&ab_channel=TravisMedia)], [[Kubectl Basic Commands](https://www.youtube.com/watch?v=azuwXALfyRg&ab_channel=TechWorldwithNana)]
   - etc
9. Clean Code and Uncle Bob, Craftmanship, Refactoring
   - code refactoring how to? Better organization, Less code duplication, Easier maintenance, understandable, readable, structured, documented
   - code challenge -thinking simply not complex. Rest apis> dont use Feign! use WebClient!
   - time complexity Big On, [[link](https://aaronice.gitbook.io/lintcode/linked_list)], [[link](https://flexiple.com/algorithms/big-o-notation-cheat-sheet/)]  
     Following are the key time and space complexities:  
   ```Constant: O(1)
      Linear time: O(n)
      Logarithmic time: O(n log n)
      Quadratic time: O(n^2)
      Exponential time: 2 ^(n)
      Factorial time: O(n!)
   ```  
   - https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html
   - https://www.youtube.com/watch?v=wSDyiEjhp8k
   - TDD
   - Naming unit test. [UnitOfWork_StateUnderTest_ExpectedBehavior], Sum_NegativeNumberAs1stParam_ExceptionThrown().
   - UML, [[link](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-aggregation-vs-composition/#:~:text=Aggregation%20implies%20a%20relationship%20where,exist%20independent%20of%20the%20parent)].
      - Composition =has-a relationship between objects. relationship where the child cannot exist independent of the parent.
      - Aggregation= relationship where the child can exist independently of the parent.
   - DDD [[link](https://medium.com/microtica/the-concept-of-domain-driven-design-explained-3184c0fd7c3f)], [[link](https://medium.com/raa-labs/part-1-domain-driven-design-like-a-pro-f9e78d081f10)], [[link](https://www.youtube.com/watch?v=xFl-QQZJFTA)]
      - The primary focus of the project is the core domain and domain logic. A domain consists of several subdomains that refer to different parts of the business logic. For example, an online retail store could have a product catalog, inventory, and delivery as its subdomains. Bounded contexts actually represent boundaries in which a certain subdomain is defined and applicable. specific bounded context, configuration, and dependencies.
      - Domain-driven design is a software engineering approach to solving a specific domain model. The solution circles around the business model by connecting execution to the key business principles.
Common terminology between the domain experts and the development team includes domain logic, subdomains, bounded contexts, context maps, domain models, and ubiquitous language as a way of collaborating and improving the application model and solving any domain-related challenges.
      - Microservices offer some serious advantages over traditional architectures, providing scalability, accessibility, and flexibility. Moreover, this approach keeps developers focused as each microservice is a loosely coupled service with a single idea of accountability.
      - subject,
   - Refactoring, [[link](https://www.youtube.com/watch?v=T3iTI2uEwkc&ab_channel=PragmaticWays)], [[link](https://www.youtube.com/watch?v=4P9qkbajv4g&ab_channel=Globant)], [[github](https://github.com/Programming-with-Mati/fp-legacy-refactor-camp/tree/solution)]
   - Static and dynamic code analysis
10. System Design
    - Spotify, music streaming [[link](https://www.youtube.com/watch?v=_K-eupuDVEc&ab_channel=IGotAnOffer%3AEngineering)]
    - Amazon System Design Interview: Design Parking Garage, [[link](https://www.youtube.com/watch?v=NtMvNh0WFVM&ab_channel=Exponent)]
    - Design Url Shortening Service, [[link](https://youtu.be/eCLqmPBIEYs?t=709)], [[link](https://www.designgurus.io/blog/url-shortening)], [[link](https://www.geeksforgeeks.org/system-design-url-shortening-service/)], [[link](https://medium.com/@sandeep4.verma/system-design-scalable-url-shortener-service-like-tinyurl-106f30f23a82)], [[link](https://www.youtube.com/watch?v=CihfMVePlcQ&ab_channel=CachedInsights)]
    - https://github.com/ystarling/system-design, https://medium.com/java-content-hub/implementing-event-driven-interfaces-in-java-c620797f63dc
    - https://www.designgurus.io/blog/step-by-step-guide
    - https://www.geeksforgeeks.org/monolithic-vs-microservices-architecture/
11. CI/CD
    - feature toggle, how to manage if one main branch
    - merge vs rebase
    - git flow? what is trunk base? main branch etc.
    - what is trunc base strategy?
    - CI/CD how it? ArgoCD, Octopus deploy, GitLab
    - Github Actions, [[link](https://docs.github.com/en/actions/quickstart)], [[link](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)], [[youtube](https://www.youtube.com/watch?v=3mzQRJY1GVE&ab_channel=TECHSCHOOL)], [[listen!](https://www.youtube.com/watch?v=R8_veQiYBjI&ab_channel=TechWorldwithNana)]
    - When new code is merged into the trunk, automated integration and code coverage tests run to validate the code quality.
    - Trunk-based development, feature flags, When developers finish new work, they must merge the new code into the main branch.
    - Gitflow vs. trunk-based development.
    - Trunk-based development is a version control management practice where developers merge small, frequent updates to a core “trunk” or main branch.
    - https://www.harness.io/blog/trunk-based-vs-feature-based-development
    - Feature flags (FF), also known as toggles, are a powerful tool in modern software development.
    - FeatureAwareFactory
    - etc
12. Linux
    - how to remote connect in Linux/Unix, SSH command? most common list commands
    - Commands: >
      cd, ls, pwd  
      ssh hostname command  
      chmod  
      top, ps, kill  
      ping, ssh, scp, curl  
      chmod u+rwx file.txt ,grants read, write, and execute permissions to the owner of the file.  
      cat file.txt displays the contents of the file “file.txt”.  
      ls -l, To view the permissions for a file  
      q, exit  
13. Agile
    - How are you start working on task? Jira, Task, Epic, User story, Scram, Kanban. Retrospective, Backlog, Sprint planning, short iteration.
    - what was your last task you working on?
    - Scrum pocker
    - Squads, [[link](https://engineering.atspotify.com/2014/03/spotify-engineering-culture-part-1/)], [[link](https://vimeo.com/85490944)]
    - Spotify
14. Code challenges
    - https://www.linkedin.com/pulse/coding-challenges-struggle-real-solutions-here-owoseni-boluwatife-ss0jf/
    - https://leanylabs.com/blog/senior-vs-middle-vs-junior-developers/
    - etc
15. Domains
    - EV Charging, OCPP & OCPI
    - [[link](https://www.linkedin.com/pulse/3-tricks-implement-smart-charging-ocpp-16-joachim-lohse/)], [[link](https://www.linkedin.com/pulse/seamless-ev-charging-roaming-exploring-ocpi-protocol-fedotov/)], [[link](https://medium.com/@yocharge2022/open-charge-point-protocol-ocpp-a-complete-guide-cfcfb57c4108)]
    - Through OCPP, the Central System can monitor and manage charging sessions, collect data on energy consumption, and handle billing information. 
    - Sending commands to CPO
    - Fintech,
Financial broker
Equities -Акции
Corporate/Goverment bonds
Trade
Exchange
Funds
stock market
ETFs(exchange-traded funds) = funds that trade on exchanges (фонды, торгующие на биржах)
Trading calendar
Auction schedule
https://www.xetra.com/xetra-en/trading/trading-models/auctionschedule
https://www.gettex.de/en/etfs/
    - Travel, [[ota](https://zoftify.com/blog/how-an-online-travel-agency-ota-back-office-software-works)], [[ota](https://xml.coverpages.org/OTA-2001B-200202.pdf)]
    - etc

16. Maven
    - mvn dependency:analyze
    - 
17. Git
    - git init
    - git add .
    - git remote add origin https://github.com/ystarling/cdr-service.git
    - commit, push
18. Frontend
    - Angular [[link](https://www.youtube.com/watch?v=pkTAFaR5LRM)], [[git](https://github.com/cornflourblue/angular-master-details-crud-example/tree/master)]
19. txt
    - How to German Freelance [[link](https://www.iamexpat.de/career/entrepreneur-germany/going-freelance)]
    - 
20. Company culture and fit
    - [[unsuccessful man](https://www.newtraderu.com/2024/05/03/12-habits-of-unsuccessful-men-who-never-move-forward-in-life/)]
    - [[germanycoach](https://www.germanycareercoach.com/blog/six-strategies-for-improving-your-job-search-germany?ss_source=sscampaigns&ss_campaign_id=63b42be196e9211651d3eb09&ss_email_id=6633b812c7eb5d42b67988cd&ss_campaign_name=How+to+get+started+with+your+Germany+job+search+%5BPART+2%2F4%5D&ss_campaign_sent_date=2024-05-04T15%3A58%3A00Z)]
21. Questions & Answers
    - Can you tell me more about the team? Can you tell me more about the team I would be working in?
    - What would a typical day for me in this role look like?
    - What are the biggest challenges that I might face in this position?
    - We appreciate any tools that increase our productivity.
    - As we have 8 separate teams always dedicated always PO, 
    - Our daily work is driven by Agile values, be focus, committed,
    - Each team works transparently making sure that all progress and knowledge shared.
    - Tell me about yourself?  
      dd
    - What can we expect from you?  
      You can expect me to behave as a professional engineer, to approach my work assignments thoughtfully, to treat my colleagues and managers respectfully, and to expect the same.
    - What do you expect from our company? What are your expectations from our company? What are your expectations from us? What are your expectations of the next company at which you will be working?  
      grow professionally with the company. I will work for the company’s goals and targets and in return, I expect to grow professionally in my career path with the company.
      You need to start with - That’s a good question. Thank you for asking.
I’m looking for the opportunity to expand my learning, put to use my skills and experience, work in a team that is inclusive and an environment that helps propel my growth beyond the job descriptions.
My expectations for the company would be to provide me healthy work environment, job security, opportunities to grow personally and professionally. I want to work with like minded people who share the same values as me.
Being part of a team where the team matters. Working in a diverse international team, where everyone is eager to learn and share with each other and appreciating the different backgrounds and experiences.
    - Why we have to hire you?
      My educational background and professional experience align closely with the requirements of this role.
      I want to work for this company because I believe I can make a positive contribution to its success. I have the skills and experience necessary to help the company reach its goals, and I am passionate about the company’s mission and values. Additionally, I am excited by the potential for growth and development opportunities that this role offers.  
    - How do you handle conflicts within your team?
    - How do you handle stress and avoid burnout in your work?
    - e
    - e
    - What is your weakness? Here’s how to identify and discuss a weakness that works in your favor.  
      Fear of public speaking, I struggle with public speaking. Nervousness about public speaking; Discomfort taking big risks;  
      [[link](https://www.deel.com/blog/weaknesses-for-job-interview)]  
      Being too detail-oriented. Procrastination. Harsh self-criticism. Difficulty multitasking. 
    - What is your favorite part about working here? How do you typically measure success in this role?  What traits have people that have been successful in the position demonstrated? What are the opportunities for professional development at the company?  
    - what do you know about our company?
why do you think you're a good fit for our company?
why do you want to work for us?  
    - what are your main strengths?
why should we hire you? [[link](https://nationalcareers.service.gov.uk/careers-advice/top-10-interview-questions)]
    - Why you left your last job? Key takeaways
    - Can you tell us about a personal achievement at work?
    - Who Will I Meet With? Is There Anything You Want Me to Prepare? What’s the Format? What’s Your Dress Code? [[link](https://www.linkedin.com/pulse/what-questions-should-i-ask-job-interview-jay-cprw-cpcc-mba/)]
    - What is your timeline for filling the position?  Never ever leave an interview without asking for their timeline. Knowing an employer’s timeline gives you an idea of what to expect next and opens the door for you to send communication to follow up (that is, if you truly want to work there)
    - What would a typical day look like for the role being offered? Why is the position vacant? Can you tell me about the team and manager I’ll be working with?  What are the next steps?  
    - What does a typical day look like?  ```Can you tell me more about the team I would be working in?  ```  
    - e



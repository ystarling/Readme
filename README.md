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
     - https://immutables.github.io/
     - JVM inside, class loaders, rt.jar, bootstrap. [[link](https://medium.com/geekculture/java-backend-developer-interview-questions-pt-1-10-1c74c76442bd)],
       [[gc](https://stackify.com/what-is-java-garbage-collection/)] , [[jvm](https://interviewnoodle.com/jvm-architecture-71fd37e7826e)] , [[jvm](https://www.linkedin.com/pulse/jvm-architecture-detail-suresh-g)] , [[jvm](https://medium.com/java-for-beginners/understanding-java-virtual-machine-jvm-architecture-e68d1c611026)]
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
     - 
   - Streams
     - Sequence of operations on objects, 
         input->intermediate operations ..filter, mapping, reducing, sorting, etc->terminal operation->output
     - aggregation functions [[link text itself](https://docs.google.com/document/d/1WO14-WGX7cPbBIZtQhvawQiXZKeFHCPIrJp_06EvnLA/edit)]
     - repeat Streams, map, multiply, reduce, groupby, summarise, max, min, Function interfaces? [[link](https://www.youtube.com/watch?v=o1H6kMlCQ74&ab_channel=Bobocode)], [[link](https://medium.com/swlh/java-collectors-and-its-20-methods-2fc422920f18)], [[github](https://github.com/bobocode-projects/java-core-exercises/tree/exercise/completed)], [[CrazyStreams.java](https://github.com/bobocode-projects/java-core-exercises/blob/exercise/completed/crazy-streams/src/main/java/com.bobocode/CrazyStreams.java)],  [[mediaum streams](https://medium.com/@code.wizzard01/java-streams-and-collectors-a-practical-guide-and-cheat-sheet-with-real-world-examples-67dcf84156b5)],  [[engineerscodinghub](https://engineerscodinghub.com/top-java-8-stream-api-practice-problems/)], [[Set-sort](https://labex.io/tutorials/java-how-to-sort-a-set-in-java-414138)]
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
     - Thread safe, DeadLock? [[interview questions](https://dev.to/krishna7852/50-interview-questions-on-multithreading-with-answers-2f8n)]
     - volatile, use fast main memory, shared and visible for threads
     - Lock interface, locking, synchronize block
     - How to use Semaphor instead of ReadWriteLock, ReentrantLock
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
     - Race condition. Occurs in programming when two or more execution threads modify a shared resource. https://medium.com/javarevisited/concurrency-in-java-a-practical-guide-fd47f86284bf, https://studyeasy.org/course-articles/java-en-en/s12l12-wait-and-notify-in-java-multithreading/
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
   - Generic, only compile time.
   - Java 11 vs 17, var keyword without specifing type, Text blocks """text""", Records, S.toList() instead of S.collect(Collectors.toList())
     [[java25](https://www.baeldung.com/java-25-features)]
   - GoF patterns
     - Remember most usage patterns: Observer, Decorator, Iterator, Builder, Strategy(lambda!)
     - BandOf4 patterns? what you use? Observer, Proxy, Iterator vs Iterable? Adapter, Decorator, Facade.
     - Decorator pattern(structural), decor. [[link](https://medium.com/analytics-vidhya/simplify-strategy-using-lambda-expression-40195d1445ea)]
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
   - Java new features: 
     - 17
       - Sealed classes, provide control over class or interface extensions
       - Switch Pattern matching. Instead of writing multiple if-else conditions to match different patterns, you can now directly incorporate the patterns within the switch cases.
     - 21
       - Virtual Threads
       - Record patterns
       - Scoped values
       - Sequenced Collection
     - 25
       - Compact source files
       - Instance Main methods
       - Module Import Declarations
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
   - https://medium.com/@Lakshitha_Fernando/spring-boot-unit-testing-for-repositories-controllers-and-services-using-junit-5-and-mockito-def3ff5891be
   - https://github.com/elkamphy/kloudly-tutorials/blob/master/spring-boot/spring-boot-rest/src/main/java/com/kloudly/springbootrest/controllers/ProductController.java
   - etc
   - How to run asynchromous tasks: @Async, CompleatableFuture, ListenerFuture
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
   - Isolation levels from lowest to highest are: Read Uncommitted, Read Committed, Repeatable Read, and Serializable. [[link](https://jetherrodrigues.dev.br/transaction-management-in-the-spring-framework-996d700f1f27)], [[docker](https://youtu.be/tNk8uXLOxA8?t=499)], [[docker](https://youtu.be/4EajrPgJAk0?t=252)], [[repeatable-read](https://www.youtube.com/watch?v=gaXISK1KTYY)], [[linkedin](https://www.linkedin.com/pulse/understanding-database-phenomena-isolation-levels-ali-0zhpf/)]  
     - Read Committed = Only see data written by committed transactional.
   - Postgres default isolation level Read-committed. Explain what this isolation means? [[isolation-levels](https://medium.com/nerd-for-tech/understanding-database-isolation-levels-c4ebcd55c6b9)]
   - NoSQL learn https://www.youtube.com/watch?v=c2M-rlkkT5o&ab_channel=BroCode
   - ElasticSearch:
     [[link](https://www.elastic.co/training/elastic-certified-engineer-exam)], [[link](https://chatgpt.com/s/t_68c7f6ab28f48191bca7bc339d9c3d43)]
   - Postgres [[query plans](https://www.postgresql.org/docs/9.5/using-explain.html)]
   - s
   - s
4. ORM
   - JPA vs Hibernate, more then one difference?
   - Lazy loading JPA/Hibernate, Cascading
   - Optimistic Lock @Version
   - Pessimistic & Optimistic locking [[linkedin](https://www.linkedin.com/pulse/optimistic-pessimistic-locking-spring-boot-hibernate-stefanova-03nwf/)], [[baeldung](https://www.baeldung.com/jpa-optimistic-locking)], [[medium](https://medium.com/jpa-java-persistence-api-guide/optimistic-vs-pessimistic-locking-in-spring-data-69ae32402fe3)], [[medium](https://medium.com/@abhirup.acharya009/managing-concurrent-access-optimistic-locking-vs-pessimistic-locking-0f6a64294db7)], [[medium](https://medium.com/@duhov/optimistic-vs-pessimistic-locking-in-databases-c32a52aeadfe)]
   - https://medium.com/@bubu.tripathy/managing-concurrent-database-updates-eaf2fe161c48
   - How to One to One mapping?
   - Jpa entity states: New, Managed, Detached(when Session closed), Removed.
   - LazyLoadingException occurs during no session. [[link](https://techbypranav.medium.com/troubleshooting-lazy-loading-in-spring-data-jpa-whats-really-going-on-9b8c0b77dece)], [[link](https://hellokoding.com/jpa-and-hibernate-problems/)], [[link](https://medium.com/jpa-java-persistence-api-guide/hibernate-lazyinitializationexception-solutions-7b32bfc0ce98)], @Fetch(FetchMode.SUBSELECT)
   - Cache L1(session level), L2(application), query cache in JPA
   - The first-level cache is associated with a Session and is used to cache data within a single transaction or request.
   - Second-level cache, on the other hand, is shared across Sessions and can cache data across multiple transactions and requests.
Hibernate provides several cache providers, including EHCache, Infinispan, Hazelcast, and Redis.
   - N + 1 problem?
   - JPA relationship 1-n, n-1, @Entity, other annotation links tables? department-employee. [[link](https://medium.com/thefreshwrites/manytoone-onetomany-mapping-in-jpa-32581d3c0f8a)], [[link](https://www.baeldung.com/jpa-one-to-one)], [[link](https://www.tutorialspoint.com/jpa/jpa_entity_relationships.htm)]
   - Opimistic lock? jpa, hibernate, entity stages, detached? Transient(Created), Managed, Detached, Removed
   - Liquibase vs Flyway, changelogs. Flyway uses SQL-based migration scripts, whereas. Liquibase uses XML, YAML, or JSON to define the database changes. [[link](https://www.linkedin.com/pulse/database-migration-flyway-vs-liquibase-rafael-porto-rodrigues#:~:text=Configuration%3A%20Flyway%20follows%20a%20convention,to%20define%20the%20database%20changes.)]
   - Hibernate audited, @Audited - generate table with suffix table_aud
   - Transactional manager in Hibernate, other vendors, @EnableTransactionManagement, PlatformTransactionManager, JpaTransactionManager
   - @Modify, safety update or delete native queries
   - https://medium.com/@aqeelabbas3972/hibernate-jpa-commonly-used-annotations-3771dc0e0e
   - https://medium.com/@bshiramagond/jpa-with-spring-boot-a-comprehensive-guide-with-examples-e07da6f3d385
5. REST
   - Rest vs Soap
   - Idempotent, [[link](https://restfulapi.net/idempotent-rest-apis/)], POST and PATCH are generally non-idempotent.
   - When to use HTTP head?
The HTTP HEAD method requests the headers that would be returned if the HEAD request's URL was instead requested with the HTTP GET method. For example, if a URL might produce a large download, a HEAD request could read its Content-Length header to check the filesize without actually downloading the file.
   - Rest header, body, query parameters, content-type? Map<String, String>
   - backward compatibility, versioning, https://www.linkedin.com/advice/0/how-do-you-design-restful-api-supports#:~:text=Backward%20compatibility%20is%20the%20ability,new%20version%20of%20the%20API.  
     REST API Versioning and Backward Compatibility  
https://harish-bhattbhatt.medium.com/maintain-backward-compatibility-in-apis-7b7c2b8197c5
   - client server architecture based on requests - responses, various response format, flexible, stateless (means all info that needs already in request).
   - Async Rest example [[link](https://sanketdaru.com/blog/polling-model-async-rest-spring-boot/)], [[link](https://github.com/sanketdaru/async-jobs-over-restful-api)], [[link2](https://medium.com/@bubu.tripathy/a-beginners-guide-to-async-processing-in-a-spring-boot-application-a4c785a992f2)], [[responsiveness](https://jackynote.medium.com/optimizing-spring-boot-asynchronous-processing-a-comprehensive-guide-f9437ce3d14d)] [[link](https://www.javacodegeeks.com/2016/06/java-8-completablefuture-vs-parallel-stream.html)]
   - endpoints names example [[link](https://docs.github.com/en/rest/authentication/endpoints-available-for-fine-grained-personal-access-tokens?apiVersion=2022-11-28)]
   - [[characteristics](https://www.linkedin.com/pulse/characteristics-rest-based-apis-baha-abu-shaqra-phd-dti-uottawa--xyycf)],  [[blog](https://www.knowledgehut.com/blog/programming/rest-api)], [[rest-api-design](https://www.getambassador.io/blog/7-rest-api-design-best-practices)],
     [[paging](https://medium.com/@AlexanderObregon/pagination-performance-testing-in-spring-boot-rest-endpoints-8aedd293c1fb)]  
   - Good REST API's:
```
     1. plural nouns, /users, /customers
     2. GET-get, POST-create, PUT-update, PATCH-partial update, (idempotency)
     3. HTTP status code, error handling, responses (never return collection or map directly! always object!)
        [], instead { size=, data: [] }
     4. Versioning, api/v1/users
     5. Paging, Sorting, Filtering (ResponseEntity<Page<User>>)
     6. ResponseEntity<DTO> create(@RequestBody DTO) return object when create resource
     7. Documentation, Swagger, Openapi, Schemas
     8. Validation, forgot to use..
     9. Database migration scripts!
     10. Database indexes, @Transaction when to use when not, update not?
     11. Wildcards * imports, unused improrts!
     12. must have Tests: junit, integration, what else?
     13. Logic should not be in Controller! even mapping!?
     14. Keep Entities inside the domain, never expose them directly in APIs.
         Do not map in controllers — delegate to service or dedicated mapper.
         Use MapStruct for large projects → generates efficient mapping code automatically.
     15. 
```

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
     Microservices are a software architecture style where a large application is broken down into a collection of small, independent, and loosely coupled services. Each service is built around a specific business capability and can be developed, deployed, and scaled independently. They communicate with each other over a network, often using well-defined APIs. This approach allows teams to work more efficiently, update individual services quickly without affecting the whole system, and scale parts of the application as needed.  
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
   - 2PC, two phase commit
   - In Onion architecture everything split by layers, core is your model, then repository, service layer . All 3 layers are abstraction or interfaces. Then other layers infrastructure, controllers is concrete realisations. Dependency inversion principle and dependency injection widely use.
   - https://www.marcobehler.com/guides/java-microservices-a-practical-guide
   - https://www.linkedin.com/pulse/microservices-world-insurance-monoliths-rais-ahmed
   - https://lumigo.io/microservices-monitoring/microservices-observability/
   - etc
7. Docker
   - What is docker container itself? [[link](https://www.docker.com/resources/what-container/#:~:text=A%20Docker%20container%20image%20is,tools%2C%20system%20libraries%20and%20settings.)]
      - A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings. Self isolated environment,.
   - Docker networking?, Docker swarm, compose? how to expose or open service connection outside?
      - https://docs.docker.com/get-started/08_using_compose/
      - https://youtu.be/tNk8uXLOxA8?t=499
      - [[crazy](https://www.youtube.com/watch?v=bKFMS5C4CG0&ab_channel=NetworkChuck)]
   - https://docs.docker.com/engine/swarm/
   - https://www.youtube.com/watch?v=i7ABlHngi1Q&ab_channel=TravisMedia
   - https://medium.com/@bharathy.poovalingam/spring-boot-with-docker-d4129a353f87
   - https://docs.docker.com/engine/swarm/raft/
   - https://www.docker.com/blog/9-tips-for-containerizing-your-spring-boot-code/
   - [[Docker Networking with spring microservices] (https://github.com/SayedBaladoh/Deploying-and-Running-Multiple-Spring-Boot-Microservices-with-MySql-using-Docker-Compose/tree/master)]
   - Docker swarm, [[Raft consensus](https://thesecretlivesofdata.com/raft/)]
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
   - K8s; deploying, managing, automating, scaling containerise applications [[link vodeo](https://www.youtube.com/watch?v=r2zuL9MW6wc)]
   - etc
9. Clean Code and Uncle Bob, Craftmanship, Refactoring
   - code refactoring how to? Better organization, Less code duplication, Easier maintenance, understandable, readable, structured, documented
   - https://refactoring.guru/
   - code challenge -thinking simply not complex.
   - Code review: [[clean code](https://www.youtube.com/watch?v=wSDyiEjhp8k)]
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
   - TDD, [[unit testing](https://ishansoninitj.medium.com/introduction-to-unit-testing-in-java-f26cdb9d387c)]  
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
   - Types of Testing I Know (and Actively Use)
      1. Unit Testing
         Tests a single class or method in isolation
         Uses JUnit 5, Mockito, AssertJ
         Fast, deterministic, no external dependencies
         Focus on business logic
      2. Integration Testing
         Tests Spring components working together
         Uses Spring Boot Test, Testcontainers, MockMvc or full HTTP calls
         Tests interaction with DB, Kafka, REST endpoints, etc.
      3. API / End-to-End Tests
         Validate REST APIs from the outside
         Use RestAssured, Karate, or Postman/Newman
         Covers the whole request → controller → service → DB flow
      4. Contract Testing
         Ensures microservices agree on API formats
         Uses Pact or Spring Cloud Contract
         Prevents breaking changes in distributed systems
      5. Integration Testing with Messaging (Kafka)
         Using Testcontainers Kafka
         Testing:
            producing messages
            consuming messages
            handling offsets & data consistency
      6. Performance & Load Testing
         Uses Gatling, JMeter, or k6
         Checks:
            throughput
            latency
            scalability
            bottlenecks
     7. Security Testing
         Tests authentication, authorization, and vulnerabilities
         Tools: OWASP ZAP, security scans
            Ensures endpoints are protected
      8. Smoke Testing / Sanity Checks
         Quick tests after deployment
         Ensures core functionality works
      9. Regression Testing
         Automated test suite to ensure new changes don’t break existing functionality
      10. Functional Testing
         Validates feature requirements from user perspective
      11. Database Testing
         Using:
            Testcontainers (PostgreSQL, MySQL)
            @DataJpaTest
            Verifies:
            entity mappings
            cascade rules
            transactions
      12. UI Testing (if applicable)
         Using Selenium, Cypress, or Playwright
         For frontend flows
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
    - 
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
    - Rate limit , [[link](https://www.innoq.com/en/blog/2024/02/rate-limiting-with-spring-boot/)], [[link](https://medium.com/@anil.goyal0057/fixed-window-rate-limiting-implementation-in-java-dc4abc07090e)], [[link](https://restfulapi.net/rest-api-rate-limit-guidelines/)]
    - etc

16. Maven
    - mvn dependency:analyze
    - 
17. Git
    - git init
    - git add .
    - git remote add origin https://github.com/ystarling/cdr-service.git
    - commit, push
    - How to write commit message, [[link](https://github.com/joelparkerhenderson/git-commit-message)]
18. Frontend
    - Angular [[link](https://www.youtube.com/watch?v=pkTAFaR5LRM)], [[git](https://github.com/cornflourblue/angular-master-details-crud-example/tree/master)]
19. Security
    - How to German Freelance [[link](https://www.iamexpat.de/career/entrepreneur-germany/going-freelance)]
    - https://portswigger.net/web-security/csrf
    - Cross forgery, Xss? How to prevent?
    - Symmetryc and Assymetryc key how and when?
    - RSA
    - [[https](https://medium.com/@mohithmarisetti_58912/https-made-easy-df1b88dc2a0e)]
    - etc
20. Company culture and fit
    - [[unsuccessful man](https://www.newtraderu.com/2024/05/03/12-habits-of-unsuccessful-men-who-never-move-forward-in-life/)]
    - [[germanycoach](https://www.germanycareercoach.com/blog/six-strategies-for-improving-your-job-search-germany?ss_source=sscampaigns&ss_campaign_id=63b42be196e9211651d3eb09&ss_email_id=6633b812c7eb5d42b67988cd&ss_campaign_name=How+to+get+started+with+your+Germany+job+search+%5BPART+2%2F4%5D&ss_campaign_sent_date=2024-05-04T15%3A58%3A00Z)]
    - https://roadmap.alexhyett.com/backend-developer-roadmap/
    - etc
    - 

21. Kotlin
    - video links [[link1](https://www.youtube.com/watch?v=i-kyPp1qFBA)], [[link2](https://www.youtube.com/watch?v=iYrgWO2oibY)], [[link3](https://www.youtube.com/watch?v=renRJnDtfxc)], [[inline](https://www.youtube.com/watch?v=T9sAlxqYFYc)]
    - Kotlin vs Java, syntax, null safety, functional programming
    - e
      
22. Kafka
    - To scale Kafka, use horizontal scaling by adding brokers to the cluster and adjust the number of partitions to match your consumer needs. Additionally, optimize performance by batching messages, enabling compression, and proactively monitoring the cluster for bottlenecks.  
    - Kafka message batching is a process where a producer groups multiple messages together into a single request to the broker, improving throughput by reducing network and I/O overhead. It can be configured by a maximum batch size (e.g., in bytes) or a maximum wait time (e.g., in milliseconds), which determines when a batch is sent even if it isn't full. This process can also be combined with compression for further efficiency.
    - d
    - 
23. Code challange
    - recursive list
    ```
         /**
          * Definition for singly-linked list.
          * public class ListNode {
          *     int val;
          *     ListNode next;
          *     ListNode() {}
          *     ListNode(int val) { this.val = val; }
          *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
          * }
          */
         class Solution {
             public ListNode reverseList(ListNode head) {
                 
                 if(head == null) return null;
                 
                 ListNode prev = null;
                 ListNode curr = head;
                 
                 while(curr != null) {
                     ListNode next = curr.next;
                     
                     //swap?
                     curr.next = prev;
                     prev = curr;
                     curr = next;
                 }
                 
                 return prev;
             }
         }
      ```  
    - s
    - s
    - s
    - s
    - 
24. Code refactoring
    - Question 1:  
      You have in a method too much If-Statements. What can you do, to make it more readable/extendable?
      [[link](https://blog.beyondthecloud.dev/blog/beyond-if-statements-ways-to-avoid-ifs)]
      Use Polymorphism / Strategy Pattern, Use a Map of Functions / Command Pattern, Use Enum With Behavior  
    - Question 2:  
      You have a constructor with a big parameterlist what can you do to make it more readable? Builder
    - s
    - Null checks with Optional
      - Traditional
        ```
            if (user != null && user.getEmail() != null){
               String email = user.getEmail().toLowerCase() ;
               System.out.println(email);
            }
        ```
      - Optional approach
        ```
            Optional.ofNullable(user)
              .map(User::getEmail)
              .map(String::toLowerCase)
              .ifPresent (System.out::println);
        ```
      - 

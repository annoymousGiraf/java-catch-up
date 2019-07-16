# Java 9 
### Welcome to Java9
First part of Starting to catch up from Java8

1. Most Significant Features in Java 9
    * Changes to the JVM
    * Changes in the Language
2. Drill Down
3. Code Examples
4. Use cases/ Study Cases
5. Deprecation 

## 1. Most Significant Features in Java 9
#### Project Jigsaw
TBD - Might be a thing of it's on as this is one of the major features of *Java 9*

#### Language Features
1. [Enhancements to the Streams API.](#stream-api)
2. Code cache can be divided in Java 9
3. HTTP/2 client API comes to Java 9 (Beta)
4. DTLS security API is added to Java 9
5. Process API
6. Variable Handles
7. Publish-Subscribe Framework
8. Unified JVM Logging
9. New APIs
10. Try With Resources Improvement

## Drill Down

#### 1.  [Streams API](#stream-api)
	
  1. takeWhile/DropWhile
		
		**takeWhile** - predicate functional interface will take all the values until the predicate
	    `Stream.of("a","b","c","").takeWhile(str -> !str.isEmpty())`


		**dropWhile** - will drop all values who does not answer the predicate
		`Stream.of("a","b","c","").dropWhile(str -> str.isEmpty())`

#### Comments
1. `_` is a reserved keyword since Java 9
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NzYwMTQ5NjcsLTk0MDIwOTMxOSwtNT
c5NjE3ODAyLC04ODQzODM0MjAsLTk4OTkyOTgyXX0=
-->
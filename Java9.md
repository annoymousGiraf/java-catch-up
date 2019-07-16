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
	   
	    `Stream.of("a","b","c","","e").takeWhile(str -> !str.isEmpty())`
		the stream will be `abc` in the case the stream will take values until the the predicate will not be true anymore.

		**dropWhile** - will drop all values until  the predicate is not met
		
		`Stream.of("a","b","c","","e").dropWhile(str -> !str.isEmpty())`
		output will be `e` in that case it will not take any value until the condition will be true
2. Iterate

	**iterate**  - now takes 3 parameters `seed` where to start, which value? second `predicate` hasNext? stop condition. `next` what to do with the next value
	
	example: 	`IntStream.iterate(1, x-> x < 10 , x-> x+1)`
3. ofNullable

	**ofNullable** - the intention is to have an option of having Optionals in the stream and avoid NPE, this will reduce the boiler plate code of having null checks on each streamline function as we did up until now on Java 8 then we can safely execute the following snippet. 

	`Employee emp = getEmployee(empId);
	
	Stream.ofNullable(emp).flatMap(Employee::roles)`

#### Comments
1. `_` is a reserved keyword since Java 9
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTczNDU1MjY2OCwtMTY2MDM4NzE5MiwtMT
I3MDcxMDgzMiwtNzY4MTUwMzg3LC05NDAyMDkzMTksLTU3OTYx
NzgwMiwtODg0MzgzNDIwLC05ODk5Mjk4Ml19
-->
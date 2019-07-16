# Java 9 
### Welcome to Java9
First part of Starting to catch up from Java8

1. [Most Significant Features in Java 9](#1-most-significant-features-in-java-9)
    * Changes to the JVM
    * [Changes in the Language](#language-features)
2. Drill Down
3. Code Examples
4. Use cases/ Study Cases
5. Deprecation 

## 1. Most Significant Features in Java 9
#### Project Jigsaw
TBD - Might be a thing of it's on as this is one of the major features of *Java 9*

#### Language Features
1. [Enhancements to the Streams API.](#1--streams-api)
2. [Factory Methods for Collections.](#2-factory-methods-for-collections)
3. [HTTP/2 client API comes to Java 9 (Beta)](#3-http2-client-api-comes-to-java-9-beta)
4. [DTLS security API is added to Java 9](#4-dtls-security-api--with-java-9)
5. Process API
6. Variable Handles
7. Publish-Subscribe Framework
8. Unified JVM Logging
9. New APIs
10. Try With Resources Improvement


## Drill Down

#### 1.  Streams API
	
  1. takeWhile/DropWhile
		
		* we need to bare in mind that an unordered stream will change the desired outcome of this functions.

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

	```java
	Employee emp = getEmployee(empId);  
	Stream.ofNullable(emp).flatMap(Employee::roles)
	 ```

#### 2. Factory Methods for Collections.

  Java 9 comes with a set of static methods to initialize collection in easier way, rather than creating the desired collection and then adding elements to it we now have a static method in each one of them for an instance `Set.of("a","b","c")` it was implemented in with overloading function up until 10 from 0 for the sake of performance, but also have a varargs version to support arbitrary amount of variables.

 
 #### 3. HTTP/2 client API comes to Java 9 (Beta)

In Java 9 Oracle started supporting HTTP/2 Protocol as well as WebSocket features. while the current protocol supported Websocket only on blocking mode. 
##### What is HTTP/2 ?

HTTP/2 can send multiple requests for data in parallel over a single TCP connection. it allows to download web files via Async mode from one server, Most of the modern browsers limit TCP connection to one server.  while in HTTP/1 you needed 3 different  connections to download 3 files. it is using header compression to reduce overhead hence less bandwidth.  it allows servers to push responses proactively to the clients instead of waiting for a new request for each resource. 

**Bare in mind that it is still incubating in Java 9** 

Some code examples on the new API 

```java
HttpClient httpClient  =  HttpClient.newHttpClient();  //Create a HttpClient

HttpRequest httpRequest  =  HttpRequest.newBuilder()
.uri(new  URI("http://localhost:3000"))
.GET().build();
```
Handle async calls.
```java
HttpClient httpClient  =  HttpClient.newHttpClient();  //Create a HttpClient
HttpRequest httpRequest = HttpRequest.newBuilder()
	.uri(new URI("http://www.localhost:3000"))
	.GET().build();

System.out.println("Calling...");

CompletableFuture<HttpResponse<String>> httpResponse =  httpClient
	.sendAsync(httpRequest,HttpResponse.BodyHandler)
	.asString(); //Send the request asynchronously
System.out.println("Performing Other Task");

if(httpResponse.isDone()) {
System.out.println("Status Code:"+httpResponse.get().statusCode());
} 
else {
	httpResponse.cancel(true);
}
```
the request running in the background allowing the code to continue with the other tasks and then handles the response with a `completableFuture`.

#### 4. DTLS security API  with Java 9

TLS support provided with Java secure socket extension API. DTLS provides is essentially TLS over UDP so that you can encrypt communication established by unreliable protocols running over UDP. 
```java

SSLContext sslContext = SSLContext.getInstance("DTLS");  
sslContext.init(…)  
SSLEngine engine = sslContext.createSSLEngine();  
engine.setUseClientMode(…);

```
in Java 9 you need to enable it though:

`-Djdk.tls.client.enableStatusRequestExtension=true ` 

`-Dcom.sun.net.ssl.checkRevocation=true`

and (on the TLS server)

`-Djdk.tls.server.enableStatusRequestExtension=true`

#### 5. Process API
Java 9 adds several new methods to the abstract  `Process`  class that let you identify direct child or descendent processes, obtain this  `Process`'s PID, return a snapshot of information about this  `Process`, obtain a completable future to receive asynchronous notification when this  `Process`  exits, and more:

-   Stream<ProcessHandle> children()
-   Stream<ProcessHandle> descendants()
-   long getPid()
-   ProcessHandle.Info info()
-   CompletableFuture<Process> onExit()
-   boolean supportsNormalTermination()
-   ProcessHandle toHandle()

```java
//Java 9
Process p = new ProcessBuilder("notepad.exe").start();

//Before Java 9
Runtime.getRuntime().exec().ProcessBuilder....

```

The process API gives us a better control on spinning process on the OS level with more fine grain detail support and a way to handle the process. with additional features such as Info.

*the main process might not have a permission to open a new process*

#### Comments
1. `_` is a reserved keyword since Java 9
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc1NTk5OTIxNCwtNDEzMzczMjEzLDE1Nz
Q1OTU1OCwtMTYxMzc5NjYxMywyNjAyNjMyMjIsLTc0MjA1NDQy
LDg1Njg2MDM4MCwtMTMxMjY1MzgzOCwtMTI5MTgyNjQ1MCwtNT
E4ODkwNzA4LC0xNjYwMzg3MTkyLC0xMjcwNzEwODMyLC03Njgx
NTAzODcsLTk0MDIwOTMxOSwtNTc5NjE3ODAyLC04ODQzODM0Mj
AsLTk4OTkyOTgyXX0=
-->
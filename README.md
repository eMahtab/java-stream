# Java Stream

A simple definition is that streams are wrappers for collections and arrays. They wrap an existing collection (or another data source) to support operations expressed with lambdas, so you specify what you want to do, not how to do it.

# Creating Streams
A stream is represented by the java.util.stream.Stream<T> interface. This works with objects only.

There are also specializations to work with primitive types, such as **IntStream, LongStream, and DoubleStream**. Also, there are many ways to create a stream. Let's see the three most popular.

The first one is creating a stream from a java.util.Collection implementation using the stream() method:
```java
List<String> words = Arrays.asList(new String[]{"hello", "hola", "hallo", "ciao"});
Stream<String> stream = words.stream();
```
  
The second one is creating a stream from individual values:
```java
Stream<String> stream = Stream.of("hello","hola", "hallo", "ciao");
```
  
The third one is creating a stream from an array:
```java
String[] words = {"hello", "hola", "hallo", "ciao"};
Stream<String> stream = Stream.of(words);
```

  
```java
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    Stream<String> stream = Stream.of("t", "k", "c", "m")
    .sorted()
    .limit(3);
    
    // Print the stream
    stream.forEach(s -> System.out.println(s));
  }
}
```
  
## Output:
```
c
k
m
```  
  
## Java 8 streams can't be reused  
After the terminal operation is performed, the stream pipeline is consumed and can't be used anymore.
  
```java
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    int[] digits = {0, 1, 2, 3, 4 , 5, 6, 7, 8, 9};
    IntStream s = IntStream.of(digits);
    long n = s.count();
    System.out.println(s.findFirst()); // An exception will be thrown
  }
}
  
```  
## Output :
```
Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed
    at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)
    at java.base/java.util.stream.IntPipeline.findFirst(IntPipeline.java:528)
    at Main.main(Main.java:8)  
  
```

```java
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    int[] digits = {20, 1, 2, 3, 4 , 5, 6, 7, 8, 9};
    long n = IntStream.of(digits).count();
    System.out.println("Count : " + n);
    System.out.println(IntStream.of(digits).findFirst().getAsInt());
  }
} 
```  

## Output :
```
Count : 10
20  
```
# sum() :  
  
```java
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    System.out.println(IntStream.of(28,4,91,30).sum()); // 153
  }
}  
```  
# average() :  
  
```java
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    System.out.println(IntStream.of(28,4,91,30).average().getAsDouble()); // 38.25
  }
}
  
```
# min() , max()
```java
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    System.out.println(IntStream.of(28,4,91,30).min().getAsInt()); // 4
    System.out.println(IntStream.of(28,4,91,30).max().getAsInt()); // 91
  }
}
  
```  

### Passing Comparator :  
```java
import java.util.*;
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    List<String> strings = Arrays.asList("Stream","Operations","on","Collections");
    strings.stream().min(Comparator.comparing(
                        (String s) -> s.length())
    ).ifPresent(System.out::println); // on
  }
}
  
``` 
  
# range() , rangeClosed()
	
The ```range(int startInclusive, int endExclusive)``` method creates an ordered stream from the first parameter to the second parameter. It increments the value of subsequent elements with the step equal to 1. The result doesn't include the last parameter, it is just an upper bound of the sequence.

The ```rangeClosed(int startInclusive, int endInclusive)``` method does the same thing with only one difference, the second element is included.	
	
```java
import java.util.stream.IntStream;
import java.util.stream.LongStream;

public class App {
	public static void main(String[] args) {
		
		IntStream intStream = IntStream.range(1,5);
		intStream.forEach((item) -> System.out.print(item + " ")); // 1 2 3 4 
		System.out.println();
		LongStream longStream = LongStream.rangeClosed(1,5);
		longStream.forEach((item) -> System.out.print(item + " ")); // 1 2 3 4 5 
	}
}  
```
	
# map()
```java
import java.util.*;
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    List<Integer> list = Arrays.asList(3, 6, 9, 12, 15);
    list.stream().map(number -> number * 3)
    .forEach((n) -> System.out.print(n + " ")); // 9 18 27 36 45 
  }
}	
```	
	
```java
import java.util.*;
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    List<String> list = Arrays.asList("java", "Stream");
    List<String> answer = list.stream().map(String::toUpperCase).
                          collect(Collectors.toList());
    // displaying the new stream of UpperCase Strings
    System.out.println(answer);  // [JAVA, STREAM]
  }
}	  
```
	
```java
import java.util.*;
import java.util.stream.*;

public class Main{
  public static void main(String[] args) {
    List<String> list = Arrays.asList("java", "Stream");
    list.stream().map(str -> str.length())
    .forEach(System.out::println);
  }
}
```

### Output :
```
4
6	
```	
	
	
# References :
https://app.pluralsight.com/guides/java-8-stream-api-part-1  

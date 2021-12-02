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


## Lambda Expression

- Bring benefits of functional programming in Java.
- 3 tokens ( ) - > { }

<a href="url"><img src="https://github.com/user-attachments/assets/3cd4d1ac-45ae-4027-9f84-1d69788ce7fb" align="left" height="400" width="400" ></a>
| - |
## Functional Interface
- Only one abstract method
- Can have any number of default and static methods
```
import java.util.*;

public class Main {
    public static void main(String[] args) {
    /*Instead of implementing a class
    and all stuff we can directly write
    lambda expression
    for functional interface.*/
    Bank sbi = ()->System.out.println("SBI Bank");
    
    sbi.minBalance();
    // can use it or overide it
    sbi.work();
    //can be called with object but class is convention
    Bank.rules();
    
  }
}
interface Bank{
  
  public void minBalance();
  
  public default void  work(){
    System.out.println("Banking");
  }
  
  // static  depedent on class
  public static void rules(){
     System.out.println("RBI standards");
  }
}
```
## Internal SAM

```
//without functional interface
class Main{
    public static void main(String[] args) {
     
     Runnable runnable1 = new MyRunnable();
     Thread thread1 = new Thread(runnable1);
     thread1.start();
     
  }
}

class MyRunnable implements Runnable{
  
  public void run(){
    System.out.print("Thread Started");
  }
}
```
```
//with function interface
public class Main {
    public static void main(String[] args) {
     // implementation for run method
     Runnable runnable1 = ()->System.out.print("Thread Started");
     Thread thread1 = new Thread(runnable1);
     thread1.start();
     
  }
}
```
## Steps to create Functional Interface and work with it
- Create a interface(Red) with only one abstract method(color).
- With that interface(Red) as variable provide implementation using lambda expression.
- Call that variable with tha abstract method(color).

## Method References

- Compact and easy form of lambda expression
- Using method reference for existing implementation instead of lambda expression implementation.
```
import java.util.*;

public class Main {
    
    static int square(int x){
      return x*x;
     }
     
    public static void main(String[] args) {
  
  //instead lambda expression - refering a method
    Math sq = Main::square;
    int val = sq.square(2);
    System.out.print(val);
   }
}

interface Math{
  int square(int x);
}

```
<a href="url"><img src="https://github.com/user-attachments/assets/92eb93e3-b1b3-4215-99bc-f3b6d33a9958" align="left" height="400" width="900" ></a>
| - |

## Type 3 Example
```
public class Main {
  
    public static void main(String[] args) {
    
      List<String> names = Arrays.asList("John", "Alexander", "Chris", "Mike");
    // This refers to an instance method of the String class, applied to each element of the stream
      List<String> upperCase = names.stream().map(String::toLowerCase).toList();
      System.out.print(upperCase);
      
   }
}

```
### Inbuilt Functional Interfaces for daily use
we no need to create interface for our simple usecase, Java provides variety of it.
![image](https://github.com/user-attachments/assets/b122c541-685b-4c80-aec2-62a518e083c3)
  
![image](https://github.com/user-attachments/assets/6d32a28a-205d-45a4-83b7-f2b850e49368)

  ```
  public class Main {
  
    public static void main(String[] args) {
    
    Predicate<Integer> divide = x->x%2==0;
    System.out.println("Predicate "+divide.test(2));
    
    Function<Integer,Integer> mul = x->x*x;
    System.out.println("Function "+mul.apply(2));
    
    Supplier<String> strSup = ()-> new String();
    System.out.println("Supplier "+strSup.get());
    
    Consumer<String> cons = s->System.out.println(s);
    cons.accept("hello");
    
      
   }
}
```
## Java Streams

## Quick ways to create a stream

```java
// From parameters
Stream<String> s = Stream.of("a", "b");

// From arrays
Arrays.stream(myArray)

// From collections
myCollections.stream()

// you also have specialized streams like IntStream, LongStream, DoubleStream, some example below:
IntStream ints = IntStream.range(0, 10_000);
IntStream rdInts = new Random().ints(1000);
```

## Most common methods

* ```filter()```
* ```mapToInt```, ```mapToObj```
* ```map()```
* ```collect()```
* ```findAny()```, ```findFirst()```, ```noneMatch()```
* ```forEach()```
* ```distinct()```
* ```sorted()``` ```sorted(Comparator<? super T>)```

## Differences map() and flatmap()

These functions can be applied to 
* Optional
* Stream

### map()

```map()``` returns a stream consisting of the results of applying the parameter function to the elements of the stream. This can potentially leads to producing output of type ```Stream<Stream<R>>```, which are hard to work with. In such cases, ```flatmap()``` can be used (see below).

### flatMap()

```flatMap()```, as it names indicates, _flattens_ the result. Unlike ```map()``` which is only performing a transformation on each element of the stream, ```flatMap()``` also perform flattening of the inner streams in the stream resulting from the transformation.

Example:
```java
String[] arr = { "map", "flatmap" }; 
Arrays.stream(arr).flatMap(word -> word.chars().mapToObj(o -> (char) o)).forEach(System.out::println);
```
This prints:
```
m
a
p
f
l
a
m
a
p
```

## From stream to collection

Example, use: ```mystream.collect(Collectors.toList())```, ```mystream.collect(Collectors.toCollection(ArrayList::new)```

## From stream to array

Example, use: ```mystream.toArray(String[]::new)```

## Reduction operations

* ```reduce(identity, BinaryOperator<T> accumulator)```

Example: 
```java
String[] myArray = { "Where", "is", "my", "stream", "?" };
String result = Arrays.stream(myArray)
                .reduce("", (a,b) -> a + " " + b);
assert result.equals(" Where is my stream ?");               
```

Others...

* ```sum()```
* ```average()```
* ```count()```

## Parallelization

The motivation behind the stream API was mostly to enable easy parallelization

Use these methods:

* ``myStream.parallel()``
* ``myCollection.parallelStream()``







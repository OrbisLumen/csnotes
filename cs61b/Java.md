# Java

## Basic

1. In java, all code must be part of a `class`
2. Classes are difined with

    ```java
    public class CLASSNAME
    ```
3. Using `{}` to delineate the beginning and ending of things
4. End lines with a semicolon  `;` 
5. The code we want to run must be inside 

    ```java
    public static void main(String[] args)
    ```
6. **Java is `statically` typed** 

### Compilation and Interpretation

1. The compiler checks that all the types in your program are compatible **before the program ever runs**

2. Compilation and Interpretation
   
    ```text
    Hello.java 
        ↓ javac (compiler)
    Hello.class 
        ↓ java (interpreter)
    Program execution
    ```

### Change file structure

    Ctrl + Shift + P
    >Java: Clean Java Language Server Workspace

- to clean Java language server cache (vscode)

###  Comments

1. single line
   
   ```java
   // The single line
   ```

2. mutiple line
   
   ```java
   /* 
   the first line
   the second line
   */
   ```

3. Doc comments
   
    ```java
    /** 
     * The first line
     * The second line
     */
    ```

##  Classes in Java

**Everything in java is a sub class of object** 

1. Constructors

    ```java
    public class Car{
        String model;
        int gas;

        public Car(String m, int n){
            this.model = m;
            this.gas = n;
        }
    }
    ```

2. Create new object

    ```java
    Car c1 = new Car("Toyato Supra", 98)
    ```

3. Seperate codes

    ```
    cs61b/
    └── lec/
        └── lec2/
            └── lec2_intro2/
                    ├── Dog.java
                    └── DogLauncher.java
    ```
    write this in the .java at the beginning

    ```java
    package lec2_intro2;
    ```
    run this in the terminal
    
    ```bash
    PS C:\...\cs61b\lec\lec2> javac lec2_intro2/*.java
    PS C:\...\cs61b\lec\lec2> java lec2_intro2.DogLuancher
    ```

4. Terminology [Click here to see Examples](./Blocks/Terminology.md)

    `Non-static method`, a.k.a `Instance method`. 
    
    (If the method is going to be invoked by an instance of the class, then it should be non-static)

    `Declaration`, `Instantiation` and `Assignment` can be combined like this 

    ```java
    Dog hugeDog = new Dog(150);
    ```

### Static vs. Non-Static
- Static methods are invoked using the class name

    ```java
    Dog.makeNoise();
    ```

- Instance methods are invoked using an instance name

    ```java
    Dog maya = new Dog(100);
    maya.makeNoise();
    ```

### Public vs. Private

- Use the **private** keyword to prevent code in other classes from using members (or constructors) of a class.
  
### Nested classes

- Allowing nested class definition.
- There are two types:
  - **Non-static inner class**: (can access outer instance fields)
  - **Static nested class**: (does not depend on the outer class) 

### Instanceof
```java
o instanceof Dog aDog
```
- Checks to see if o's dynamic type is Dog (or one of its subtypes).
- If no, returns false.
- If yes, returns true and casts o into a variable of static type Dog called aDog.
- Works correctly, even if o is null.



## Types

1. 8 primitive types in Java :

    `byte`, `short`, `int`, `long`, `float`, `double`, `boolean`, `char`

2. Everything else is a reference type
    
   - When we declare a variable of any reference type :

       - Java allocates exactly a box of size 64 bits, no matter what type of object.
       - These bits can be either set to : 
         - Null (all zeros)
         - The 64 bit "address" of a specific instance of that class (returned by new)

3. The Golden Rule of Equals (GRoE)
    
    y = x **copies** all the bits from x into y.

    (If x and y are reference types, the "address"" is copied)

4. Passing parameters obeys the same rule : 
   
    Simply **copy the bits** (also called pass by value) to the new scope.

### Constants

In Java, constants are written using:
```java
static final TYPE NAME = value;
```


### Generics

- Generics let classes, interfaces, and methods work with different data types while keeping type safety.
- A generic type uses a placeholder like `T` for the actual type.

    ```java
    public class Box<T> {
        private T item;

        public Box(T i) {
            item = i;
        }

        public T get() {
            return item;
        }
    }
    ```
- For arrays
    ```java
    Generic[] a = (Generic[]) new Object[size];
    ```

## Loop Structure

### while

```java
while (condition) {
    statement(s);
}
```

### do-while

```java
do {
    statement(s);
} while (condition);
```

### for
1. basic for loop :
    ```java
    for (initialization; termination; increment) {
        statement(s)
    }
    ```
2. enhanced for loop :
    ```java
    for (Type var : arrayOrCollection) {
        statement(s);
    }
    ```

### continue and break

#### break
- Immediately exits the loop
#### continue
- Skips current iteration
- Moves to next loop cycle


## Input in Java

### Command Line Input（命令行参数）

1. Java receives command line input via:

    ```java
    public static void main(String[] args)
    ```

- args is an array of String

2. Example :
   
    ```java
    public class Demo {
        public static void main(String[] args) {
            double T = Double.parseDouble(args[0]);
            double dt = Double.parseDouble(args[1]);
            String filename = args[2];

            System.out.println(T);
            System.out.println(dt);
            System.out.println(filename);
        }
    }
    ```
3. Run in terminal :
   
    ```bash
    java Demo 100.0 0.5 data.txt
    ```

### Standard Input（标准输入 / 键盘输入）

1. Use Scanner to read input from keyboard

2. Example :
    ```java
    import java.util.Scanner;

    public class Demo {
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);

            int x = sc.nextInt();       // read int
            double y = sc.nextDouble(); // read double
            String s = sc.next();       // read one word
            String line = sc.nextLine();// read entire line

            System.out.println(x);
            System.out.println(y);
            System.out.println(s);
            System.out.println(line);

            sc.close();
        }
    }
    ```


## Testing

**Google's Truth assertions library**

### Truth Assertions

1. A truth assertion takes the following format:
```java
assertThat(actual).isEqualTo(expected);
```
2. To add a message to the assertion, we can instead use:
```java
assertWithMessage("actual is not expected")
    .that(actual)
    .isEqualTo(expected);
```
3. We can use things other than isEqualTo, depending on the type of actual. For example, if actual is a List, we could do the following to check its contents without constructing a new List:
```java
assertThat(actualList)
    .containsExactly(0, 1, 2, 3)
    .inOrder();
```
4. If we had a List or other reference object, we could use:
```java
assertThat(actualList)
    .containsExactlyElementsIn(expected)  // `expected` is a List
    .inOrder();
```
5. Truth has many assertions, including isNull and isNotNull; and isTrue and isFalse for booleans.


## Inheritance

### Interface Inheritance

[List example here](./Blocks/List.md)

- A specification of what, not how.
- Interface: The list of all method signatures.

### Inpelmentation Inheritance

```java
default public TYPE NAME() {
    ...
}
```
- A specification of what and how.
- By using interface to complete this.

### Implements

```java
public class AList<Item> implements List<Item> {
    ...
}

public class SLList<Item> implements List<Item> {
    ...
}
```
- List is a hypernym of AList and SLList.
- AList and SLList are hyponyms.
- Subclasses must override all of the methods mentioned in interface.

### Extends
    
```java
public class RotatingSSList<Item> extends SLList<Item> {
    ...
}
```
- `implements` for hypernym is an interface
- `extends` for hypernym is a class

### Overriding vs. Overloading

1. override :
    - A `subclass` has a method with the exact same signature as in the `superclass`, we say the subclass overrides the method.
  
2. overload :
    - Methods with the same name but different signatures are overlodaded.

3. `@Override`: to remind it is a overriden method.

### Static Type vs. Dynamic Type

1. Static Type (Compile-Time Type) :
    - specified at declaration
    - never changes

2. Dynamic Type (Run-Time Type) :
    - specified at instantiation 
    - equal to the type of the object being pointed at

3. Compiler allows method calls based on compile-time type of variable and also allows assignments based on compile-time types.

#### Casting

```java
Poodle frank = new Poodle("Frank", 5);
Poodle frankJr = new Poodle("FrankJr", 15);

Dog largerDog = maxDog(frank, frankJr);
Poodle largerPoodle = (Poodle) maxDog(frank, frankJr);
```
### Super

```java
super.method()
```
- to call superclass's method in subclass
- When a subclass constructor is called, Java will first call a constructor of the superclass.(If there is no none-argument constructor in superclass, you must call super(x))

### Encapsulation

A module is said to be encapsulated if its implementation is completely hidden and it can be accessed only through a documented interface.

### *Implementation Inheritance Defect

Users do not now superclass's impletation and could code new method to break encapsulation

## Comparables vs. Comparators

### Comparable (内部比较规则）

1. Definition
```java
public interface Comparable<T> {
    int compareTo(T other);
}
```
- Defines natural ordering
- Implemented inside the class 

2. Example 
```java 
public class Dog implements Comparable<Dog> {
    int size;

    public int compareTo(Dog other) {
        return this.size - other.size;
    }
}
```

3. Key Points 
    - comparison logic is part of the class
    - Only `one` natural order
    - Type-safe (no casting)
  
### Comparator (外部比较规则)

1. Definition
```java
public interface Comparator<T> {
    int compare(T a, T b);
}   
```
- Defines custom ordering 
- Implemented outside the class

2. Example 
```java
public class DogSizeComparator implements Comparator<Dog> {
    public int compare(Dog a, Dog b) {
        return a.size - b.size;
    }
}
```

3. Usage
```java
ComparatorName.compare(o1, o2);
```
- Return negative integer when o1 < o2
- Return zero when o1 = o2
- Return positive integer when o1 > o2

4. Key Points 
    - Comparison logic is separate from class
    - Can define multiple orderings
    - More flexible

## Iterators

### Iterable (可迭代对象)

1. Definition  
```java
public interface Iterable<T> {
    Iterator<T> iterator();
}
```
- Represents a collection that can be iterated.
- Provides a way to get an iterator.

2. Example
```java 
public class AList<T> implements Iterable<T> {
    public Iterator<T> iterator() {
        return new AListIterator();
    }
}
```

3. Usage (for-each loop)
```java
for (int x : mylist) {
    System.out.printIn(x);
}
```

- Compiler translates to:
```java
Iterator<Integer> it = myList.iterator();
while(it.hasNext()) {
    int x = it.next();
}
```

4. Key Points
    - Enables for-each loop
    - Only requirement: implement iterator()

### Iterator (迭代器)

1. Definition 
```java
public interface Iterator<T> {
    boolean hasNext();
    T next();
}
```
- Represents the actual traversal logic
- Moves through elements one by one

2. Example

```java
private class AListIterator implements Iterator<T> {
    private int index;

    public boolean hasNext() {
        return index < size;
    }

    public T next() {
        T returnItem = items[index];
        index++;
        return returnItem;
    }
}
```

3. Key Points
- hasNext() -> is there more?
- next() -> get next item
- Maintains iteration state

## Object Methods

**Since all the things in java implements object and the methods below are object's, you can directly override them in your class**

### toString() 

1. The toString() method provides a string representation of an object.
    - System.out.printIn(Object x) calls x.toString()


### equals()
1. Definition 
```java
public class Object {
    ...

    public boolean equals(Object obj) {
        return (this == obj);
    }
}
``` 
```java
public class Dog {

    public int weightInPounds;                  /** Instance variable */

    public Dog(int startingWeight) {            /** Constructor */
        weightInPounds = startingWeight;
    }

    public void makeNoise() {                   /** Non-static method */
        if (weightInPounds < 10) {
            System.out.println("yipyip!");
        } else if (weightInPounds < 30) {
            System.out.println("bark!");
        } else {
            System.out.println("arooooooo!");
        }
    }
}
```

 ```java
public class DogLuancher {

    public static void main(String[] args) {
        Dog smallDog;               /** Declaration */
        new Dog(20);                /** Instantiation */
        smallDog = new Dog(5);      /** Instantiation and Assignment */
        smallDog.makeNoise();       /** Dot -> using a method */        
    }
}
```
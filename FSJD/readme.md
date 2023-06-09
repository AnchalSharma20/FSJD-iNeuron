# ← Java →

Q1. Write a Java program that uses polymorphism by defining an interface called Shape with methods to calculate the area and perimeter of a shape. Then create classes that implement the Shape interface for different types of shapes, such as circles and triangles.

**Solution :**

```Java
interface Shape {
    double calculateArea();
    double calculatePerimeter();
}

class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

class Triangle implements Shape {
    private double sideA;
    private double sideB;
    private double sideC;

    public Triangle(double sideA, double sideB, double sideC) {
        this.sideA = sideA;
        this.sideB = sideB;
        this.sideC = sideC;
    }

    @Override
    public double calculateArea() {
        // Using Heron's formula to calculate the area of a triangle
        double s = (sideA + sideB + sideC) / 2;
        return Math.sqrt(s * (s - sideA) * (s - sideB) * (s - sideC));
    }

    @Override
    public double calculatePerimeter() {
        return sideA + sideB + sideC;
    }
}

public class Main {
    public static void main(String[] args) {
        Shape circle = new Circle(5);
        System.out.println("Circle - Area: " + circle.calculateArea());
        System.out.println("Circle - Perimeter: " + circle.calculatePerimeter());

        Shape triangle = new Triangle(3, 4, 5);
        System.out.println("Triangle - Area: " + triangle.calculateArea());
        System.out.println("Triangle - Perimeter: " + triangle.calculatePerimeter());
    }
}
```


Q2. Write a Java program to invoke parent class constructor from a child class. Create Child class object and parent class constructor must be invoked. Demonstrate by writing a program. Also explain key points about Constructor.


**Solution :**

```Java
class Parent {
    public Parent() {
        System.out.println("Parent class constructor invoked");
    }
}

class Child extends Parent {
    public Child() {
        super(); // Invoking parent class constructor
        System.out.println("Child class constructor invoked");
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child(); // Creating Child class object
    }
}
```

### Key points about constructors:
```
- A constructor is a special method in a class that is used to initialize objects of that class. It has the same name as the class and doesn't have a return type, not even void.
- If a class doesn't define any constructors, a default constructor (with no arguments) is automatically provided by the Java compiler.
- Constructors can be overloaded, meaning a class can have multiple constructors with different parameters.
- Constructors can invoke the constructor of the superclass using the super keyword as shown in the example. This is used to initialize the inherited members of the object.
- If a constructor doesn't explicitly invoke the parent class constructor using super(), the compiler automatically inserts a call to the default constructor of the parent class.
- If the parent class doesn't have a default constructor (constructor with no arguments) and the child class doesn't invoke any other constructor of the parent class using super(), then the compiler will show an error.
- The order of execution in the above example is such that the parent class constructor is invoked first, followed by the child class constructor.
- Constructors can have access modifiers (public, private, protected), which control the visibility of the constructor.
- Constructors can also have other modifiers like static, final, and abstract, but they are rarely used in combination with constructors.
```

Q3. Write a Java programme that takes an integer from the user and throws an exception if it is negative.Demonstrate Exception handling of same program as solution.

**Solution :**

```Java
import java.util.Scanner;

class NegativeNumberException extends Exception {
    public NegativeNumberException(String message) {
        super(message);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            System.out.print("Enter an integer: ");
            int number = scanner.nextInt();

            if (number < 0) {
                throw new NegativeNumberException("Negative numbers are not allowed.");
            }

            System.out.println("You entered: " + number);
        } catch (NegativeNumberException e) {
            System.out.println("Exception: " + e.getMessage());
        }
    }
}
```

Q4. Create a Java program that simulates a bank account. The program should allow users to deposit and withdraw money, check their balance.

**Solution :**

```Java
import java.util.Scanner;

class BankAccount {
    private double balance;

    public BankAccount() {
        balance = 0.0;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit successful. Current balance: " + balance);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawal successful. Current balance: " + balance);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient funds.");
        }
    }

    public double getBalance() {
        return balance;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        BankAccount account = new BankAccount();

        boolean exit = false;

        while (!exit) {
            System.out.println("Bank Account Menu");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Check Balance");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter deposit amount: ");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    break;
                case 2:
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawalAmount = scanner.nextDouble();
                    account.withdraw(withdrawalAmount);
                    break;
                case 3:
                    System.out.println("Current balance: " + account.getBalance());
                    break;
                case 4:
                    exit = true;
                    System.out.println("Exiting the program. Thank You!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }

            System.out.println();
        }
    }
}
```

Q5. Demonstrate the difference between abstract class and interface by writing programs as well as in keypoints.

**Solution :**

#### Example 1: Using an Abstract Class

```java
abstract class Animal {
    public abstract void makeSound();

    public void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
    public void makeSound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.makeSound();
        dog.eat();
    }
}
```
#### Example 2: Using an Interface

```Java
interface Animal {
    void makeSound();
    void eat();
}

class Dog implements Animal {
    public void makeSound() {
        System.out.println("Dog barks");
    }

    public void eat() {
        System.out.println("Dog is eating");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.makeSound();
        dog.eat();
    }
}
```

### Key points about abstract classes:
```
- An abstract class is a class that cannot be instantiated but can be subclassed.
- It may contain both abstract and non-abstract methods.
- Abstract methods are declared without a body and must be implemented in the subclass.
- Abstract classes can have constructors, instance variables, and concrete methods.
- Subclasses of an abstract class must provide an implementation for all abstract methods.
- An abstract class can provide a common implementation for the methods, which can be inherited by its subclasses.
```
### Key points about interfaces:
```
- An interface is a blueprint of a class and represents a contract.
- It cannot be instantiated directly; instead, a class implements an interface.
- It contains only method signatures without any implementation.
- All methods in an interface are implicitly public and abstract.
- Interfaces can also contain constant fields (implicitly static and final).
- A class can implement multiple interfaces.
- An interface provides a way to achieve multiple inheritance in Java.
- When a class implements an interface, it must provide an implementation for all the methods defined in the interface
```

Q6. Write a Java program that uses stream api to perform operations on a large data set, such as sorting or filtering the data.

**Solution :**

```Java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        // Sample data set
        List<Integer> numbers = Arrays.asList(5, 2, 9, 1, 7, 3, 8, 4, 6);

        // Sorting the numbers in ascending order
        System.out.println("Sorted numbers in ascending order:");
        numbers.stream()
                .sorted()
                .forEach(System.out::println);

        // Sorting the numbers in descending order
        System.out.println("\nSorted numbers in descending order:");
        numbers.stream()
                .sorted((a, b) -> b.compareTo(a))
                .forEach(System.out::println);
                
                
      List<String> names = Arrays.asList("John", "Mary", "David", "Alice", "Michael", "Sara");

        // Filtering names with more than 4 characters
        System.out.println("Names with more than 4 characters:");
        names.stream()
                .filter(name -> name.length() > 4)
                .forEach(System.out::println);

        // Filtering names starting with 'M'
        System.out.println("\nNames starting with 'M':");
        names.stream()
                .filter(name -> name.startsWith("M"))
                .forEach(System.out::println);
    }
}
```


Q7. Create a Java program that implements a binary search algorithm. The program should accept user input for the target value and search for it in a sorted array. The program should return the index of the target value if found or a message if not found.

**Solution :**

```Java
import java.util.Arrays;
import java.util.Scanner;

public class BinarySearchExample {
    public static int binarySearch(int[] array, int target) {
        int left = 0;
        int right = array.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (array[mid] == target) {
                return mid; // Target found at index mid
            } else if (array[mid] < target) {
                left = mid + 1; // Target is in the right half
            } else {
                right = mid - 1; // Target is in the left half
            }
        }

        return -1; // Target not found
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Sorted array
        int[] array = { 2, 5, 8, 12, 16, 23, 38, 56, 72, 91 };

        System.out.print("Enter the target value: ");
        int target = scanner.nextInt();

        int index = binarySearch(array, target);

        if (index != -1) {
            System.out.println("Target found at index: " + index);
        } else {
            System.out.println("Target not found in the array.");
        }
    }
}
```

Q8. Write a Java program that creates two threads. The first thread should print even numbers between 1 and 10, and the second thread should print odd numbers between 1 and 10.

**Solution :**

```Java
public class EvenOddThreadExample {
    public static void main(String[] args) {
        // Create two threads
        Thread evenThread = new Thread(new EvenRunnable());
        Thread oddThread = new Thread(new OddRunnable());
        // Start the threads
        evenThread.start();
        oddThread.start();
    }
}

class EvenRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 2; i <= 10; i += 2) {
            System.out.println("Even Thread: " + i);
            try {
                Thread.sleep(500); // Add a delay for better visibility
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class OddRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 10; i += 2) {
            System.out.println("Odd Thread: " + i);
            try {
                Thread.sleep(500); // Add a delay for better visibility
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

Q9. Write a Java program that implements a producer-consumer model using multithreading. The program should have a producer thread that generates random numbers and adds them to a queue, and a consumer thread that reads numbers from the queue and calculates their sum. The program should use synchronization to ensure that the queue is accessed by only one thread at a time.

**Solution :**

```Java
import java.util.Queue;
import java.util.LinkedList;

public class ProducerConsumerExample {
    private static final int QUEUE_CAPACITY = 10;
    private static final int NUM_VALUES_TO_PRODUCE = 20;

    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();

        Thread producerThread = new Thread(() -> {
            for (int i = 0; i < NUM_VALUES_TO_PRODUCE; i++) {
                synchronized (queue) {
                    while (queue.size() == QUEUE_CAPACITY) {
                        try {
                            queue.wait(); // Wait if the queue is full
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                    int value = (int) (Math.random() * 100);
                    queue.offer(value);
                    System.out.println("Produced: " + value);
                    queue.notifyAll(); // Notify the consumer that a value is produced
                }
            }
        });

        Thread consumerThread = new Thread(() -> {
            int sum = 0;
            for (int i = 0; i < NUM_VALUES_TO_PRODUCE; i++) {
                synchronized (queue) {
                    while (queue.isEmpty()) {
                        try {
                            queue.wait(); // Wait if the queue is empty
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                    int value = queue.poll();
                    sum += value;
                    System.out.println("Consumed: " + value);
                    queue.notifyAll(); // Notify the producer that a value is consumed
                }
            }
            System.out.println("Sum of consumed values: " + sum);
        });

        producerThread.start();
        consumerThread.start();
    }
}
```

Q10. Write a Java program that reads a set of integers from the user and stores them in a List. The program should then find the second largest and second smallest elements in the List.

**Solution :**

```Java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class SecondLargestSmallestExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        List<Integer> numbers = new ArrayList<>();

        System.out.print("Enter the number of integers: ");
        int count = scanner.nextInt();

        System.out.println("Enter the integers:");
        for (int i = 0; i < count; i++) {
            int num = scanner.nextInt();
            numbers.add(num);
        }

        if (numbers.size() < 2) {
            System.out.println("At least 2 integers are required.");
            return;
        }

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;
        int smallest = Integer.MAX_VALUE;
        int secondSmallest = Integer.MAX_VALUE;

        for (int num : numbers) {
            if (num > largest) {
                secondLargest = largest;
                largest = num;
            } else if (num > secondLargest && num != largest) {
                secondLargest = num;
            }

            if (num < smallest) {
                secondSmallest = smallest;
                smallest = num;
            } else if (num < secondSmallest && num != smallest) {
                secondSmallest = num;
            }
        }

        System.out.println("Second largest element: " + secondLargest);
        System.out.println("Second smallest element: " + secondSmallest);
    }
}
```

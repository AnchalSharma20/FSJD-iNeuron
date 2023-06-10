# ← Java →

`Q1. Write a Java program that uses polymorphism by defining an interface called Shape with methods to calculate the area and perimeter of a shape. Then create classes that implement the Shape interface for different types of shapes, such as circles and triangles.`

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
- A constructor is a special method in a class that is used to initialize objects of that class. It has the same name as the class and doesn't have a return type, not even void.
- If a class doesn't define any constructors, a default constructor (with no arguments) is automatically provided by the Java compiler.
- Constructors can be overloaded, meaning a class can have multiple constructors with different parameters.
- Constructors can invoke the constructor of the superclass using the super keyword as shown in the example. This is used to initialize the inherited members of the object.
- If a constructor doesn't explicitly invoke the parent class constructor using super(), the compiler automatically inserts a call to the default constructor of the parent class.
- If the parent class doesn't have a default constructor (constructor with no arguments) and the child class doesn't invoke any other constructor of the parent class using super(), then the compiler will show an error.
- The order of execution in the above example is such that the parent class constructor is invoked first, followed by the child class constructor.
- Constructors can have access modifiers (public, private, protected), which control the visibility of the constructor.
- Constructors can also have other modifiers like static, final, and abstract, but they are rarely used in combination with constructors.


`Q3. Write a Java programme that takes an integer from the user and throws an exception if it is negative.Demonstrate Exception handling of same program as solution.`

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

`Q5. Demonstrate the difference between abstract class and interface by writing programs as well as in keypoints.`

**Solution :**

Here's an example that demonstrates the difference between an abstract class and an interface in Java:

Example 1: Using an Abstract Class

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
Example 2: Using an Interface

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
- An abstract class is a class that cannot be instantiated but can be subclassed.
- It may contain both abstract and non-abstract methods.
- Abstract methods are declared without a body and must be implemented in the subclass.
- Abstract classes can have constructors, instance variables, and concrete methods.
- Subclasses of an abstract class must provide an implementation for all abstract methods.
- An abstract class can provide a common implementation for the methods, which can be inherited by its subclasses.

### Key points about interfaces:
- An interface is a blueprint of a class and represents a contract.
- It cannot be instantiated directly; instead, a class implements an interface.
- It contains only method signatures without any implementation.
- All methods in an interface are implicitly public and abstract.
- Interfaces can also contain constant fields (implicitly static and final).
- A class can implement multiple interfaces.
- An interface provides a way to achieve multiple inheritance in Java.
- When a class implements an interface, it must provide an implementation for all the methods defined in the interface


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


`Q7. Create a Java program that implements a binary search algorithm. The program should accept user input for the target value and search for it in a sorted array. The program should return the index of the target value if found or a message if not found.`

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

`Q9. Write a Java program that implements a producer-consumer model using multithreading. The program should have a producer thread that generates random numbers and adds them to a queue, and a consumer thread that reads numbers from the queue and calculates their sum. The program should use synchronization to ensure that the queue is accessed by only one thread at a time.`

Q10. Write a Java program that reads a set of integers from the user and stores them in a List. The program should then find the second largest and second smallest elements in the List.

# ← JDBC →

`Q11. Write a Java program that connects to a MySQL database using JDBC. The program should read data from a table and display the results in the console.`

Q12. Write a Java program that uses JDBC to implement a simple CRUD (create, read, update, delete) application. The program should allow users to add, view, update, and delete records in a MySQL database table.

`Q13. Create a Java program that connects to a PostgreSQL database and executes a batch update. The program should read the input data from a file and insert it into the database using JDBC batch updates.`

Q14. Create a Java servlet that reads the name of the user from a form and displays a welcome message on the web page. The servlet should use the GET method to read the input data from the user.

`Q15. Write a Java servlet that reads the data from a MySQL database table and displays it in an HTML table on the web page. The servlet should use JDBC to connect to the database and retrieve the data.`

# ← Servlet →

Q16. Create a Java servlet that uses session management to maintain the state of the user across multiple requests. The servlet should store the user's name in a session object and display it on multiple pages of the web application.

`Q17. Create a web application that lets users create and view blog posts. The web application should use the MVC pattern, with servlets as controllers, JSPs as views, and a database as the model. Users should be able to create new blog posts by filling out a form that includes a title, description, and content. The web application should use a servlet to store the blog post data in the database. Users should also be able to view all the blog posts on a separate page, and the web application should use a servlet to retrieve the blog post data from the database and display it in a formatted way.`

# ← Hibernate →

Q18. Create a Java program that uses Hibernate to connect to a MySQL database and retrieve data from a table. The program should use Hibernate to map the table to a Java object and then display the data on the console.

`Q19. Create a Java program that uses Hibernate to insert data into a MySQL database table. The program should use Hibernate to map the table to a Java object and then insert the data into the table. After inserting the data, the program should retrieve it from the database and display it on the console.`

Q20. The program should use Hibernate to map the table to a Java object and then update the data in the table. After updating the data, the program should retrieve it from the database and display it on the console.

# ← Spring Boot →

`Q21. Create a Spring Boot application that inserts data into a MySQL database table using JPA and Hibernate. The application should use Spring Data JPA to map the table to a Java object and then insert the data into the table.`

Q22. Create a Spring Boot application that uses Spring Data JPA to retrieve data from a database. The application should have entities for users and orders, and should allow for querying orders by user.

`Q23. Create a Spring MVC application that allows users to register and login. The application should have a registration form that accepts user details and a login form that authenticates users.`

Q24. Create a Spring Boot application that uses Spring MVC to create a REST API. The API should accept a JSON request with data and insert it into a MySQL database table using JPA and Hibernate. The application should use Spring Data JPA to map the table to a Java object and then insert the data into the table.

`Q25. Create a Spring Boot application that uses Spring AOP to log method calls. The application should have a service class with methods that perform operations. The application should use Spring AOP to log the method calls with input and output parameters to the console.`

Q26. Create a Spring Boot application that exposes a REST API for managing a list of products. The API should allow for creating, updating, deleting, and retrieving products.

`Q27. Create a Spring Boot application that uses Spring Cloud to register a service with Eureka Server. The application should expose a REST API for retrieving data from a database and the API should be discovered by Eureka Server.`

Q28. Create a Spring Boot application that uses Spring Cloud Config Server to externalise configuration. The application should have a property file that defines properties for database connection and other application settings.

`Q29. Create a Spring Boot application that uses Spring Data JPA to retrieve data from a database and expose it as a REST API. The API should allow for filtering, sorting, and paging.`

Q30. Create a Spring Boot application that uses Spring Cloud Circuit Breaker to handle failures in a REST API. The API should use a circuit breaker pattern to handle timeouts and other errors.





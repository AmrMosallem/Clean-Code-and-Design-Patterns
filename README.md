# **Clean Code and Design Patterns Guide**

## Introduction
This repository serves as a detailed resource for understanding and applying key principles of clean coding, code refactoring, and software design patterns. It is structured to provide a step-by-step approach to improving code readability, maintainability, and scalability.

The contents are divided into the following sections:  

- **Clean Code:** Explains best practices for naming, functions, formatting, and comments to write clear and consistent code.  
- **Code Refactoring:** Introduces the concept of refactoring and provides specific techniques like simplifying conditional expressions to optimize existing code.  
- **SOLID Principles:** Covers the five fundamental principles of object-oriented design—Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion.  
- **Design Patterns:** Explores common software design patterns, categorized into Creational, Structural, and Behavioral patterns, with examples like Singleton, Factory, Adapter, and Observer patterns.  

Each section includes practice questions and examples to reinforce learning, making this repository a practical reference for both beginners and experienced developers.

### Table of Contents:

1. [Clean Code](#clean-code)
   - [Clean Code for Naming](#clean-code-naming)
   - [Clean Code for Functions](#clean-code-functions)
   - [Clean Code for Formatting](#clean-code-formatting)
   - [Clean Code for Comments](#clean-code-comments)
   - [Practice Questions](#clean-code-questions)
2. [Code Refactoring](#code-refactor)
   - [Introduction to Code Refactoring](#code-refactor-intro)
   - [Refactoring Technique: Simplifying Conditional Expression](#code-refactor-technique)
3. [SOLID Principles](#solid-principles)
   - [Introduction to SOLID Principles](#solid-intro)
   - [Single Responsibility Principle (SRP)](#solid-srp)
   - [Open Closed Principle (OCP)](#solid-ocp)
   - [Liskov Substitution Principle (LSP)](#solid-lsp)
   - [Interface Segregation Principle (ISP)](#solid-isp)
   - [Dependency Inversion Principle (DIP)](#solid-dip)
   - [Practice Questions](#solid-questions)
4. [Design Patterns](#dp)
   - [Introduction to Design Patterns](#dp-intro)
   - [Creational Design Patterns](#dp-creational)
     - [Singleton Design Pattern](#dp-singleton)
     - [Factory Design Pattern](#dp-factory)
     - [Builder Design Pattern](#dp-builder)
   - [Structural Design Patterns](#dp-structural)
     - [Adapter Design Pattern](#dp-adapter)
     - [Composite Design Pattern](#dp-composite)
     - [Facade Design Pattern](#dp-facade)
   - [Behavioral Design Patterns](#dp-behavioral)
     - [Strategy Design Pattern](#dp-strategy)
     - [Observer Design Pattern](#dp-observer)

---

<div id='clean-code'/>

# Clean Code

## What is Clean Code?

Clean code is code that is easy to read, understand, and modify. It adheres to best practices and avoids unnecessary complexity, making it:

- **Readable**: Easy for others (and your future self) to understand.
- **Maintainable**: Simple to debug and update.
- **Scalable**: Flexible to accommodate future growth.
<div id='clean-code-naming'/>

## **Clean Code for Naming**

Good naming conventions make code easier to read, understand, and maintain.

### **1. Use Intention-Revealing Names**

Names should clearly describe the purpose or function of a variable, method, or class.

#### **Example 1:**

```java
// Bad Practice
int d; // What does "d" represent?

// Good Practice
int elapsedTimeInDays; // Clearly indicates what the variable stores.
```

#### **Example 2 (Minesweeper):**

**Bad Practice:**

```java
    public List<int[]> getThem() {
        List<int[]> list1 = new ArrayList<>();
        for (int[] x : theList) {
            if (x[0] == 4)
                list1.add(x);
        }
        return list1;
    }
```

**Good Practice:**

```java
    public List<Cell> getFlaggedCells() {
        List<Cell> flaggedCells = new ArrayList<Cell>();
        for (Cell cell : gamesBoard) {
            if (cell.isFlagged())
            flaggedCells.add(cell);
        }
        return flaggedCells;
    }
```

---

### **2. Avoid Disinformation**

Names should not imply incorrect behavior or create confusion. Avoid misleading terms.

#### **Example 1:**

```java
// Bad
List<String> accountsList = new HashSet<>(); // "List" in the name implies it's a list, but it's actually a Set.

// Good
Set<String> uniqueAccounts = new HashSet<>(); // Correct naming avoids confusion.
```

#### **Example 2:**

```java
// Bad
class Car {
    int speed; // Speed could mean anything: current speed, max speed, or average speed.
}

// Good
class Car {
    int currentSpeed; // Specifically refers to the car's current speed.
}

```

---

### **3. Make Meaningful Distinctions**

Avoid meaningless distinctions like `a`, `b`, `foo`, and `bar`. Names should add meaningful context.

#### **Example:**

```java
// Bad
String data1, data2; // Unclear how data1 and data2 differ.

// Good
String userInput, processedData; // Names clarify their roles.
```

---

### **4. Use Pronounceable Names**

Names should be easy to pronounce to improve communication between developers.

#### **Example:**

```java
// Bad
String dtRng; // Hard to pronounce and understand.
String usrNm; // Difficult to read and say aloud.

// Good
String dateRange; // Clear and easy to pronounce.
String userName; // Clear and readable.
```

---

### **5. Use Searchable Names**

Names should be easily searchable within the codebase, especially for constants and other key variables.

#### **Example 1:**

```java
// Bad
int max = 42; // Hard to search for "42".

// Good
static final int MAX_RETRIES = 42; // MAX_RETRIES is searchable.
```

#### **Example 2:**

```java
// Bad
public void processGrades() {
    int s = 0;
    int m = 0;

    for (int i = 0; i < 10; i++) {
        s += i * 10; // What is 's'?
        m = s / (i + 1); // What is 'm'?
    }

    System.out.println("Final Result: " + m); // What is the result here?
}

// Good
public void calculateAverageGrade() {
    int totalGrades = 0; // Represents the sum of grades.
    int averageGrade = 0; // Represents the average grade.

    for (int studentIndex = 0; studentIndex < 10; studentIndex++) {
        totalGrades += studentIndex * 10; // Adds the grade for the current student.
        averageGrade = totalGrades / (studentIndex + 1); // Calculates the running average.
    }

    System.out.println("Final Average Grade: " + averageGrade);
}
```

---

### **6. Member Prefixes (Avoid Encodings)**

Avoid prefixes like `m_` for members or `f_` for fields. Modern IDEs make this unnecessary.

#### **Example:**

```java
// Bad
private int m_age;

// Good
private int age; // IDEs highlight members and methods distinctly.
```

---

### **7. Hungarian Notation (Avoid Encodings)**

Avoid including type information in variable names, e.g., `strName` or `iCount`. The code should rely on the type system.

#### **Example:**

```java
// Bad
int iCount;
String strName;

// Good
int count;
String name; // Type is evident from the declaration.
```

---

### **8. Avoid Mental Mapping**

Avoid using single-character variable names or abbreviations that require the reader to remember their purpose.

#### **Example:**

```java
// Bad
int d; // Requires mental effort to remember "d" is days.

// Good
int days; // No mental mapping is needed.
```

---

### **9. Class Names**

Class names should be nouns or noun phrases that describe what the class represents. Avoid verbs.

#### **Example:**

```java
// Bad
class ManageUser; // "Manage" is a verb, not suitable for a class name.

// Good
class UserManager; // Describes the purpose of the class.
```

---

### **10. Method Names**

Method names should be verbs or verb phrases describing what the method does.

#### **Example:**

```java
// Bad
void data(); // Unclear what this method does.

// Good
void fetchData(); // Action-oriented and descriptive.
```

---

### **11. Pick One Word per Concept**

Use consistent terminology across the codebase to avoid confusion.

#### **Example:**

```java
// Bad
void fetchData();
void retrieveData(); // Two words for the same concept.

// Good
void fetchData(); // Consistent terminology.
```

---

### **12. Don’t Pun**

Avoid using the same word for multiple meanings, as it causes confusion.

#### **Example:**

```java
// Bad
class User {
    void add(); // Does "add" mean adding a user or adding data to a user?
}

// Good
class UserManager {
    void addUser(); // No ambiguity.
}
```

---

By following these practices, your code will be cleaner, more readable, and easier to maintain. Clean code is a sign of professional, thoughtful development that prioritizes collaboration and long-term usability.

---

<div id="clean-code-functions"/>

## **Clean Code for Functions**

### **1. Small**

Functions should be short and concise, ideally **<=150 characters per line** and **<20 lines** in length. Long functions are harder to read, understand, and maintain.

#### **Example of a Problematic Function (Too Long)** 

```java
public void processOrder(Order order) {
    if (order == null) {
        System.out.println("Invalid order");
        return;
    }
    if (order.getItems().isEmpty()) {
        System.out.println("Order has no items");
        return;
    }
    double total = 0;
    for (Item item : order.getItems()) {
        total += item.getPrice();
    }
    order.setTotal(total);
    System.out.println("Order processed successfully");
}
```

This function does too much at once and is difficult to read.

#### ✅ **Refactored (Small Functions)** 

```java
public void processOrder(Order order) {
    if (!validateOrder(order)) return;
    calculateTotal(order);
    printSuccessMessage();
}

private boolean validateOrder(Order order) {
    if (order == null || order.getItems().isEmpty()) {
        System.out.println("Invalid order or no items");
        return false;
    }
    return true;
}

private void calculateTotal(Order order) {
    double total = 0;
    for (Item item : order.getItems()) {
        total += item.getPrice();
    }
    order.setTotal(total);
}

private void printSuccessMessage() {
    System.out.println("Order processed successfully");
}
```

Each function does one thing, making it easier to understand and modify.

---

### **2. Do One Thing**

Functions should focus on a single responsibility. A function that does too much is harder to test and maintain.

#### **Bad Example (Does Multiple Things)**

```java
public void processUser(User user) {
    System.out.println("Validating user...");
    if (user.getAge() < 18) {
        System.out.println("User is underage.");
        return;
    }
    System.out.println("Saving user to database...");
    saveToDatabase(user);
    System.out.println("User saved successfully.");
}
```

#### ✅ **Refactored (Does One Thing per Function)**
```java
public void processUser(User user) {
    if (!validateUser(user)) return;
    saveUser(user);
}

private boolean validateUser(User user) {
    if (user.getAge() < 18) {
        System.out.println("User is underage.");
        return false;
    }
    return true;
}

private void saveUser(User user) {
    saveToDatabase(user);
    System.out.println("User saved successfully.");
}
```

Each function does a single task, making it simpler to test and modify.

---

### **3. One Level of Abstraction per Function**

Think of the "what", not the "how". Each function should operate at a single level of abstraction. Mixing high-level and low-level details makes the code harder to follow.

#### **Bad Example (Mixing What and How)**

```java
public void sendEmail(User user) {
    System.out.println("Preparing email...");
    String recipient = user.getEmail();
    String subject = "Welcome!";
    String body = "Hello " + user.getName() + ", thank you for joining.";
    System.out.println("Sending email to " + recipient);
    System.out.println("Subject: " + subject);
    System.out.println("Body: " + body);
}
```

#### ✅ **Refactored (One Level of Abstraction)**

```java
// High Level Function
public void sendEmail(User user) {
    Email email = prepareEmail(user);
    send(email);
}

// Low Level Functions (Helper Functions)
private Email prepareEmail(User user) {
    Email email = new Email();
    email.setRecipient(user.getEmail());
    email.setSubject("Welcome!");
    email.setBody("Hello " + user.getName() + ", thank you for joining.");
    return email;
}

private void send(Email email) {
    System.out.println("Sending email to " + email.getRecipient());
    System.out.println("Subject: " + email.getSubject());
    System.out.println("Body: " + email.getBody());
}
```

The high-level (main) function focuses on **what** needs to happen, while the low-level details (the **how**) are delegated to helper functions.

---

### **4. Reading Code from Top to Bottom (The Stepdown Rule)**

Code should flow naturally from higher-level functions at the top to lower-level details at the bottom, like reading a story. This makes the code easier to understand.

#### **Bad Example**

```java
private void validateOrder(Order order) { /* ... */ }
private void calculateTotal(Order order) { /* ... */ }
private void printSuccessMessage() { /* ... */ }

public void processOrder(Order order) {
    if (!validateOrder(order)) return;
    calculateTotal(order);
    printSuccessMessage();
}
```

Here, helper methods are defined before the main `processOrder()` function, disrupting the natural flow of reading.

#### ✅ **Refactored (Stepdown Rule)**

```java
public void processOrder(Order order) {
    if (!validateOrder(order)) return;
    calculateTotal(order);
    printSuccessMessage();
}

private void validateOrder(Order order) { /* ... */ }
private void calculateTotal(Order order) { /* ... */ }
private void printSuccessMessage() { /* ... */ }
```

Now, you can read the code top-to-bottom without jumping around. High-level logic appears first, and details are progressively revealed below.

---

### **5. Function Arguments**

The ideal number of arguments for a function is zero.
Keep arguments to a minimum for better readability and usability. Avoid long argument lists.

#### **Best Practice**

- **No arguments:** Most readable and focused. ✅
  ```java
  public void printMessage() {
      System.out.println("Hello, World!");
  }
  ```
- **Monadic function (one argument):** Easy to understand. ✅

  ```java
  public void writeField(String name) {
      System.out.println("Field: " + name);
  }
  ```

- **Dyadic function (two arguments):** Acceptable but can cause confusion. ⚠️

  ```java
  Point p = new Point(0, 0); // Two related values: x and y.
  ```

- **Three or more arguments:** Try to refactor with objects or utility classes. ⛔
  ```java
  Circle makeCircle(double x, double y, double radius); // Refactor this:
  Circle makeCircle(Point center, double radius); // Cleaner and easier to read.
  ```

---

### **6. Common Monadic Forms**

Monadic functions take **one argument** and are easier to understand, use, and test compared to functions with multiple arguments. These functions typically fall into one of three categories:

#### **1. Asking a Question About the Argument**

The function evaluates or checks a condition related to the argument and returns a **boolean** result.

**Example:**

```java
boolean fileExists(String fileName) {
    File file = new File(fileName);
    return file.exists();
}
```

#### **2. Operating on the Argument, Transforming and Returning It**

The function takes the argument, **performs an operation**, and **returns a new result**. It doesn't modify the original argument.

**Example:**

```java
// Transforms the file name (`String`) into a file stream (`InputStream`).
InputStream fileOpen(String fileName) throws FileNotFoundException {
    return new FileInputStream(fileName);
}
```

#### **3. An Event: Using the Argument to Alter the State of the System**

The function performs a **state-changing action** in the system using the argument. It doesn't return a value but may modify internal states or trigger events.

**Example:**

```java
// Responds to a specific event (failed attempts) by altering the system state (locking an account or logging the failure).
void passwordAttemptFailedNTimes(int attempts) {
    if (attempts > 3) {
        System.out.println("Account locked due to too many failed attempts!");
    }
}
```

---

### **7. Dyadic Functions**

Two arguments can sometimes lead to confusion about their roles. Provide context or avoid if possible.

#### **Example:**

```java
// Bad
writeField(outputStream, name); // What is the role of outputStream here?

// Good
writeField(name); // Clear focus on the field to be written.
```

---

### **8. Argument Objects**

When you have multiple related arguments, group them into an object.

#### ⚠️ **Before Refactor**

```java
Circle makeCircle(double x, double y, double radius);
```

#### ✅ **After Refactor**

```java
Circle makeCircle(Point center, double radius); // Easier to understand and use.
```

---

### **9. Verbs and Keywords**

Use meaningful and descriptive names for functions.

#### **Example:**

```java
write(name);

// Better Alternative:
writeField(name);   // Adds more context.


// Bad
assertEquals(expected, actual); // Confusing order.

// Better Alternative
assertExpectedEqualsActual(expected, actual); // Clearer intent.
```

---

### **10. Have No Side Effects**

A function should either **do something** or **return something**, but not both.

#### **Bad Example**

```java
public boolean saveUser(User user) {
    // Saves the user and returns true if successful.
    database.save(user);
    return true;
}
```

#### ✅ **Good Example**

```java
public void saveUser(User user) {
    database.save(user); // Only saves the user.
}

public boolean isUserSaved(User user) {
    return database.isSaved(user); // Only checks if saved.
}
```

---

### **11. Switch Statements**
Avoid large `switch` statements for maintainability. Instead, use polymorphism.

#### **Bad Example**

```java
class Employee {
    int payAmount() {
        switch (getType()) {
            case ENGINEER: return monthlySalary;
            case SALESMAN: return monthlySalary + commission;
            case MANAGER:  return monthlySalary + bonus;
            default: throw new Exception("Invalid Employee Type");
        }
    }
}
```

#### ✅ **Good Example (Polymorphism)**

```java
abstract class EmployeeType {
    abstract int payAmount(Employee emp);
}

class Salesman extends EmployeeType {
    int payAmount(Employee emp) {
        return emp.getMonthlySalary() + emp.getCommission();
    }
}

class Manager extends EmployeeType {
    int payAmount(Employee emp) {
        return emp.getMonthlySalary() + emp.getBonus();
    }
}
```

With polymorphism, adding new employee types is straightforward without modifying existing code.

### **Summary**

**Clean functions:**  
- Are small and concise.
- Focus on doing one thing exceptionally well.
- Maintain a single level of abstraction.
- Follow a logical top-to-bottom flow for readability.
- Use clear, minimal, and appropriate function arguments.
- Utilize common monadic forms effectively for simplicity.
- Avoid dyadic functions unless necessary.
- Prefer argument objects to multiple arguments for clarity.
- Use meaningful verbs and keywords to describe actions clearly.
- Have no unintended side effects.
- Minimize or avoid using switch statements to reduce complexity.

<div id="clean-code-formatting"/>

## **Clean Code for Formatting**

Good formatting improves readability and helps developers quickly understand the structure and intent of the code.

---

### **Vertical Distance**

1. **Variables Close to Usage:**  
 Declare variables right before they are used to reduce the mental effort of tracking their purpose.

   ```java
   // Bad:
   int result; // declared far from usage
   // many lines of code
   result = computeSomething();

   // Good:
   int result = computeSomething(); // declared right before usage
   ```

2. **Instance Variables at the Top:**  
Keep instance variables at the top of a class to make the class structure clear.

   ```java
   public class MyClass {
       private String name; // instance variables at the top
       private int age;

       public MyClass(String name, int age) { /* constructor */ }
   }
   ```

3. **Dependent Functions Should Be Close:**  
If a function calls another, place them close together in the code, with the caller above the callee.

   ```java
   public void process() { // Caller
       calculate();
   }

   private void calculate() { // Callee
       // logic
   }
   ```

---

### **Horizontal Openness and Density**

- **Openness:** Use spaces to separate distinct code elements for better readability.

  ```java
  // Bad:
  if(x==y){z++;}

  // Good:
  if (x == y) { z++; }
  ```

- **Density:** Keep closely related elements together.
  ```java
  // Good:
  for (int i = 0; i < 10; i++) {
      // loop logic
  }
  ```

---

### **Horizontal Alignment**

```java
  private     int         number;
  private     String      name;
  public      boolean     isSuccessful;
```

---

### **Breaking Indentation**
 Use proper indentation when breaking long lines to maintain clarity and structure.

  ```java
  // Bad:
  if (condition1 && condition2 && condition3 && condition4) { doSomething(); }

  // Good:
  if (condition1 && condition2 &&
      condition3 && condition4) {
      doSomething();
  }
  ```

Proper formatting ensures code is easier to read, maintain, and debug, making collaboration among developers more effective.

<div id="clean-code-comments"/>

## **Clean Code for Comments**

Well-placed comments can improve code readability, but they should be used sparingly and thoughtfully. Comments should **add value**, not clutter.

---

### **Good Comments** ✅

Comments should clarify or provide useful information.

1. **Legal Comments:**  
   Necessary for licensing or legal purposes.

   ```java
   // Copyright (c) 2025 Amr Mosallem. All rights reserved.
   ```

2. **Informative Comments:**  
   Provide valuable information about the code's purpose or behavior that isn't immediately clear from the code itself.

   ```java
   // This value is calculated based on the user's timezone.
   int offset = getTimeZoneOffset();
   ```

3. **Explanation of Intent:**  
   Explain why something is done, not what is done (since the code should already explain "what").

   ```java
   // Using binary search to optimize performance for large datasets.
   int index = binarySearch(array, key);
   ```

4. **Clarification:**  
    Clarify any complex or non-obvious code logic.

   ```java
   // The XOR operation is used here to ensure no overlapping conditions.
   result = a ^ b;
   ```

5. **Warning of Consequence:**  
   Highlight potential side effects or important constraints.

   ```java
   // Warning: Modifying this function may affect downstream systems.
   updateDatabase();
   ```

6. **TODO Comments:**  
   Mark areas needing improvement or further work.
   ```java
   // TODO: Refactor this method to handle edge cases.
   processData();
   ```

---

### **Bad Comments** ⚠️

Avoid comments that create confusion or add unnecessary clutter.

1. **Mumbling:**  
   Vague or unclear comments that don't help.

   ```java
   // Do something here
   processData();
   ```

2. **Redundant Comments:**  
   Comments that repeat what is already clear from the code.

   ```java
   int x = 10; // set x to 10
   ```

3. **Mandated Comments:**  
   Comments that are forced or required by policy but don't add any real value.

   ```java
   // Method to calculate sum
   public int add(int a, int b) {
       return a + b;
   }
   ```

4. **Attributions and Bylines:**  
   Comments giving credit, often unnecessary in collaborative codebases.

   ```java
   // Written by: Amr Mosallem, 2025
   ```

5. **Commented-Out Code:**  
   Leaving old or unused code in the comments. It should be removed from the codebase.

   ```java
   // int oldValue = computeOldValue();
   // System.out.println(oldValue);
   ```

6. **Don’t Use Comments When a Function or Variable Can Explain It:**  
   If a comment explains what a variable or function does, consider renaming them to be more self-explanatory.

   ```java
   // Bad:
   // Check if the user is logged in
   if (user.status == 1) { ... }

   // Good:
   if (user.isLoggedIn()) { ... }
   ```

7. **Noise Comments:**  
   Adding unnecessary remarks that don't provide value.

   ```java
   // This is a loop
   for (int i = 0; i < 10; i++) { ... }
   ```

8. **Journal Comments:**  
   Logs or version history in comments (use version control systems instead).
   ```java
   // Updated on 2025-01-01: Added validation logic.
   // Updated on 2025-01-02: Fixed a bug in validation.
   ```

---

### **Summary**

Good comments are **rare, focused, and valuable**. If the code can explain itself through clear naming and structure, comments might not be needed at all. When you do use comments, ensure they are meaningful and maintainable.

<div id="clean-code-questions"/>

## **Clean Code Practice Questions**

### Question 1: Consider the method below. Do the variables need a more meaningful context? If so, suggest them?

```java
private void printGuessStatistics(char candidate, int count) {
    String number;
    String verb;
    String pluralModifier;
    if (count == 0) {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    } else if (count == 1) {
        number = "1";
        verb = "is";
        pluralModifier = "";
    } else {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    String guessMessage = String.format(
            "There %s %s %s%s", verb, number, candidate, pluralModifier);
    print(guessMessage);
}
```

#### **Answer**:

Yes, the variables need more meaningful names for clarity. Here are suggestions:

- `candidate` → `letterCandidate`
- `count` → `occurrenceCount`
- `number` → `quantityText`
- `verb` → `verbForm`
- `pluralModifier` → `pluralSuffix`
- `guessMessage` → `formattedGuessMessage`

This makes the purpose of each variable more obvious.

### Question 2: Consider the method below. Do as you can to make the code clean.

```java
import java.util.Scanner;

public class Main {
    class Point {
        public int x, y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int tests = scan.nextInt();
        scan.nextLine(); // Consume newline left-over
        for (int i = 0; i < tests; i++) {
            char[] line = scan.nextLine().replaceAll("\\s+", "").toCharArray();
            Point fB = new Main().new Point(line[0] - 65, line[1] - 48); // fB = first Point
            Point sB = new Main().new Point(line[2] - 65, line[3] - 48); // sB = second // same point
            if (fB.x == sB.x && fB.y == sB.y) {
                System.out.println(0 + " " + (char) ('A' + fB.x) + " " + fB.y);// calculating the slope (y2-y1)/(x2-x1).
                                                                               // It has to be written
            } else if (Math.abs(fB.x - sB.x) == Math.abs(fB.y - sB.y)) {
                System.out.println(1 + " " + (char) ('A' + fB.x) + " " + fB.y + " " + (char) ('A' + sB.x) + " " + sB.y);
            } // are they the same color?
            else if ((Math.abs(fB.x + fB.y) % 2) != (Math.abs(sB.x + sB.y) % 2)) {
                System.out.println("Impossible");
            } else {
                // negative slope for attacker
                int x = ((fB.y + fB.x) - (sB.y - sB.x)) / 2;
                int y = x + (sB.y - sB.x);
                // x or y are out of bounds, to avoid it, we get a positive slope for the
                if (x < 1 || x > 8 || y < 1 || y > 8) {
                    x = ((sB.y + sB.x) - (fB.y - fB.x)) / 2;
                    y = x + (fB.y - fB.x);
                }
                System.out.println(2 + " " + (char) ('A' + fB.x) + " " + fB.y + " " +
                        (char) ('A' + x) + " " + y + " " + (char) ('A' + sB.x) + " " + sB.y);
            }
        }
        // because I do clean Java!
        scan.close();
    }
}
```

#### **Answer**:

To clean up this code, the focus will be on improving readability, organization, and maintainability.

**Improvements Made:**

1. **Encapsulated `Point` as a static nested class** for easier access.
2. **Meaningful variable names** for better understanding.
3. **Removed inline comments** in favor of self-explanatory code.
4. **Decomposed complex logic** into methods.
5. **Improved structure and readability** with consistent formatting.

**Cleaned Code:**

```java
import java.util.Scanner;

public class Main {

    static class Point {
        public int x, y;

        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int testCases = scanner.nextInt();
        scanner.nextLine(); // Consume newline after integer input

        for (int i = 0; i < testCases; i++) {
            char[] input = scanner.nextLine().replaceAll("\\s+", "").toCharArray();
            Point start = new Point(input[0] - 'A', input[1] - '0');
            Point end = new Point(input[2] - 'A', input[3] - '0');

            handleTestCase(start, end);
        }
        scanner.close();
    }

    private static void handleTestCase(Point start, Point end) {
        if (isSamePoint(start, end)) {
            printResult(0, start);
        } else if (isOnSameDiagonal(start, end)) {
            printResult(1, start, end);
        } else if (!isSameColor(start, end)) {
            System.out.println("Impossible");
        } else {
            Point intermediate = findIntermediatePoint(start, end);
            printResult(2, start, intermediate, end);
        }
    }

    private static boolean isSamePoint(Point p1, Point p2) {
        return p1.x == p2.x && p1.y == p2.y;
    }

    private static boolean isOnSameDiagonal(Point p1, Point p2) {
        return Math.abs(p1.x - p2.x) == Math.abs(p1.y - p2.y);
    }

    private static boolean isSameColor(Point p1, Point p2) {
        return (Math.abs(p1.x + p1.y) % 2) == (Math.abs(p2.x + p2.y) % 2);
    }

    private static Point findIntermediatePoint(Point start, Point end) {
        int x = ((start.y + start.x) - (end.y - end.x)) / 2;
        int y = x + (end.y - end.x);

        if (x < 0 || x > 7 || y < 0 || y > 7) {
            x = ((end.y + end.x) - (start.y - start.x)) / 2;
            y = x + (start.y - start.x);
        }

        return new Point(x, y);
    }

    private static void printResult(int steps, Point... points) {
        System.out.print(steps);
        for (Point point : points) {
            System.out.print(" " + (char) ('A' + point.x) + " " + point.y);
        }
        System.out.println();
    }
}
```

**Key Changes:**

1. **Encapsulated logic in helper methods**:

   - `isSamePoint()`
   - `isOnSameDiagonal()`
   - `isSameColor()`
   - `findIntermediatePoint()`
   - `printResult()`

2. **Better variable naming**:

   - `fB` → `start`
   - `sB` → `end`
   - `x, y` are used meaningfully in context.

3. **Enhanced readability**: Structured code in logical blocks and removed hardcoded values where possible.

### Question 3: According to the clean code rules, what are the bad practice in the following code?

```java
private boolean isValidInsertion(int column) {
    boolean columnIsAvailable = column <= NUM_COLUMNS &&
    column >= 1 && numberOfItemsInColumn[column - 1] <
    NUM_ROWS;
    boolean gameIsOver = getWinner() != Chip.NONE;
    return columnIsAvailable && !gameIsOver;
}
```

#### **Answer**:

**Bad Practices in the Code**:

1. **Misleading Method Name**:

   - `isValidInsertion` implies only column validation, but it also checks the game's state (`gameIsOver`).
   - Suggestion: Rename to `canInsertChip`.

2. **Boolean Variables Naming**:

   - `columnIsAvailable` and `gameIsOver` mix validation logic and game state. Names should be more precise, e.g., `isColumnWithinBounds` and `isGameInProgress`.

3. **Magic Numbers**:

   - `1` and `column - 1` are hardcoded. Use named constants for clarity.

4. **Unclear Responsibility**:
   - The method does more than one thing: validates the column and checks if the game is over. These should be separate methods.

### Question 4: In your opinion, does this code has a side-effect or not? Clarify your answer.

```java
public class UserValidator {
    private Cryptographer cryptographer;

    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
            if ("Valid Password".equals(phrase)) {
                Session.initialize();
                return true;
            }
        }
        return false;
    }
}
```

#### **Answer:**

Yes, the code has a side effect. The method `checkPassword` not only validates the user's password but also initializes the session (`Session.initialize()`), which changes the system state. This violates the principle of a single responsibility for methods.

### Question 5: Name the clean code rule violated in the following codes:

**Code 1:**

```java
String yyyymmdstr = new
SimpleDateFormat("YYYY/MM/DD").format(new Date());
```

**Code 2:**

```java
getUserInfo();
getClientData();
getCustomerRecord();
```

**Code 3:**

```java
setTimeout(blastOff, 86400000);
```

**Code 4:**

```java
public void emailClients(List<Client> clients) {
    for (Client client : clients) {
        Client clientRecord = repository.findOne(client.getId());
        if (clientRecord.isActive()) {
            email(client);
        }
    }
}
```

#### **Answer:**

**Clean Code Rules Violated:**

1. **`String yyyymmdstr = new SimpleDateFormat("YYYY/MM/DD").format(new Date());`**

   - **Violation**: Misleading Naming.
     - The variable name `yyyymmdstr` is unclear and does not follow descriptive naming conventions.

2. **`getUserInfo(); getClientData(); getCustomerRecord();`**

   - **Violation**: Function Names Should Reveal Intent.
     - These names are too generic and don't clarify what specific data is retrieved.

3. **`setTimeout(blastOff, 86400000);`**

   - **Violation**: Magic Numbers.
     - `86400000` is unclear; use a named constant like `MILLISECONDS_IN_A_DAY` for clarity.

4. **`public void emailClients(List<Client> clients) {...}`**
   - **Violation**: Function Does More Than One Thing.
     - The method retrieves client records, checks their status, and sends emails. These responsibilities should be separated.

### Question 6: Answer the questions by referring to the version of the code in C shown below:

```C
int f(int j,int k){int i,m;m=0;for(i=0;i$<=$ 7;i++)
if(j$<=$v[i]&&v[i-1]$<=$k)m++;return m;}
```

1. Comment on the presentation / layout of this code.
2. Rewrite the code to make it look more conventional.
3. Could the original code run successfully without any changes? Give reasons for your answer.
4. Explain what the code is trying to achieve.

#### Answer:

1. **Comment on presentation/layout**:

   - The layout is unclear and messy.
   - Poor indentation and formatting make it hard to read.
   - Variable names like `i`, `j`, `k`, and `m` are vague.

2. **Rewritten Code**:

   ```c
   int countInRange(int lowerBound, int upperBound) {
       int index, count = 0;
       for (index = 0; index <= 7; index++) {
           if (lowerBound <= v[index] && v[index - 1] <= upperBound) {
               count++;
           }
       }
       return count;
   }
   ```

3. **Could it run successfully without changes?**  
   Yes, the original code could run successfully **if the syntax errors are fixed** (e.g., replacing `$<=$` with `<=`). However, the lack of clarity and readability makes it error-prone and hard to maintain.

4. **What is the code trying to achieve?**  
   It counts how many elements in the array `v` lie within a range defined by `j` (lower bound) and `k` (upper bound).

### Question 7: Demonstrate at least two forms of syntax for adding comments to source code.

#### **Answer:**

1. **Single-line comment**:

   ```java
   // This is a single-line comment
   ```

2. **Multi-line comment**:
   ```java
   /*
   This is a multi-line comment
   that spans across multiple lines.
   */
   ```

### Question 8: The following code segments are represented a bad code practice. Rewrite the code after cleaning & refactoring as much as you can.

```java
public void Eq(double a, double b, double c) {
    double D = b * b - 4 * a * c;
    if (D > 0) {
        double x1, x2;
        x1 = (-b - Math.sqrt(D)) / (2 * a);
        x2 = (-b + Math.sqrt(D)) / (2 * a);
        System.out.println("x1 = " + x1 + ", x2 = " + x2);
    } else if (D == 0) {
        double x;
        x = -b / (2 * a);
        System.out.println("x = " + x);
    } else {
        System.out.println("Equation has no roots");
    }
}
```

#### **Answer:**

```java
public void solveQuadraticEquation(double a, double b, double c) {
    double discriminant = calculateDiscriminant(a, b, c);

    if (discriminant > 0) {
        double[] roots = calculateRealRoots(a, b, discriminant);
        System.out.println("x1 = " + roots[0] + ", x2 = " + roots[1]);
    } else if (discriminant == 0) {
        double root = calculateSingleRoot(a, b);
        System.out.println("x = " + root);
    } else {
        System.out.println("Equation has no real roots");
    }
}

private double calculateDiscriminant(double a, double b, double c) {
    return b * b - 4 * a * c;
}

private double[] calculateRealRoots(double a, double b, double discriminant) {
    double x1 = (-b - Math.sqrt(discriminant)) / (2 * a);
    double x2 = (-b + Math.sqrt(discriminant)) / (2 * a);
    return new double[]{x1, x2};
}

private double calculateSingleRoot(double a, double b) {
    return -b / (2 * a);
}
```

### Improvements made:

1. **Descriptive method names**: Changed method name `Eq` to `solveQuadraticEquation` for clarity.
2. **Variables renamed**: Improved variable names for clarity (`D` → `discriminant`, `x1`, `x2`, `x` → `roots`).
3. **Extracted logic into helper methods**: Split logic into smaller methods (`calculateDiscriminant`, `calculateRealRoots`, and `calculateSingleRoot`) for better readability and reusability.
4. **Removed redundant code**: Combined repetitive logic to make the code more concise and maintainable.

<div id="code-refactor" \>

# Code Refactoring

<div id = "code-refactor-intro" \>

## **Introduction to Code Refactoring**

**Refactoring** is the process of restructuring existing code to improve its internal structure without changing its external behavior.

###**Reasons for Refactoring:**

1. **Bad Code Quality**: Code is poorly written or difficult to read.
2. **Code Smells**: Signs of problematic code needing improvement.
3. **Technical Debt**: Delayed improvements that hinder future progress.
4. **Complex Code**: Code that is overly complicated and hard to work with.

###**Advantages of Refactoring:**

1. **Improved Readability**: Cleaner, easier-to-understand code.
2. **Better Extendibility**: Simplified addition of new features.
3. **Lower Maintenance Costs**: Reduced complexity minimizes expenses.
4. **Enhanced Architecture**: Structural improvements without behavior changes.

###**Challenges of Refactoring:**

1. **Time Constraints**: Limited time for improvements.
2. **Reluctance**: Resistance to change due to familiarity with existing code.
3. **Fear Factor**: Concern about introducing bugs.
4. **Re-Testing**: Need to re-test functionality after changes.

---

### **Code Smells**

Signs that code needs refactoring:

1. **Duplicated Code**: Repeated logic increases maintenance efforts.
   - _Example_: Identical loops or methods across classes.
2. **Long Method**: Overly long functions reduce readability.
   - _Solution_: Break methods into smaller, focused functions.
3. **Long Class**: A class doing too much violates the Single Responsibility Principle.
4. **Too Many Parameters**: Hard-to-read and test functions.
   - _Solution_: Pass objects instead of multiple parameters.
5. **Feature Envy**: One class depends excessively on another class's methods.
   - _Solution_: Move methods to the relevant class.
6. **Lazy Class**: A class contributing too little functionality.
   - _Solution_: Merge it with a more active class.
7. **Contrived Complexity**: Overuse of design patterns where simpler solutions suffice.
8. **Complex to Debug**: Code is so intricate it becomes hard to troubleshoot.

**Conclusion:**  
Regular refactoring minimizes code smells, ensuring maintainable, efficient, and scalable software.

<div id = "code-refactor-technique" \>

## Simplifying Conditional Expression Techniques

### 1. Decompose Conditional

**Problem:** Complex conditional expressions are hard to read and maintain.

**Solution:** Break down the conditional logic into separate, meaningful methods or functions.

**Example Before Refactoring:**

```java
if (user.getAge() > 18 && user.hasValidId() && user.isNotBlacklisted()) {
    grantAccess();
}
```

The logic is crammed into the `if` condition, which can be hard to understand at a glance.

**Example After Refactoring:**

```java
if (isEligibleForAccess(user)) {
    grantAccess();
}

private boolean isEligibleForAccess(User user) {
    return user.getAge() > 18 && user.hasValidId() && user.isNotBlacklisted();
}
```

Now the `if` condition clearly expresses its intent. The detailed logic is moved to a method that explains what is being checked.

### 2. Consolidate Conditional Expression

**Problem:** Multiple conditions lead to the same result, making the code repetitive.

**Solution:** Combine these conditions into a single, unified expression.

**Example Before Refactoring:**

```java
double calculateTax() {
    if (income < 20000) return 0;
    if (isTaxExempt) return 0;
    if (isRetired) return 0;
    return income * 0.1;
}
```

**Example After Refactoring:**

```java
double calculateTax() {
    if (isNotTaxable(income, isTaxExempt, isRetired)) return 0;
    return income * 0.1;
}

private boolean isNotTaxable(double income, boolean isTaxExempt, boolean isRetired) {
    return income < 20000 || isTaxExempt || isRetired;
}
```

Multiple conditions are consolidated into a single helper method, `isNotTaxable`. This eliminates repetition and makes the tax calculation method concise and focused.

### 3. Replace Nested Conditional with Guard Clause

**Problem:** Deeply nested conditionals make it hard to follow the normal flow of the program.

**Solution:** Use guard clauses to handle special cases early, allowing the main logic to be simpler and flatter.

**Example Before Refactoring:**

```java
public String getMembershipType(int age, boolean isStudent) {
    if (age < 12) {
        return "Child";
    } else {
        if (age >= 12 && age < 18) {
            return "Teen";
        } else {
            if (age >= 18 && isStudent) {
                return "Student";
            } else {
                return "Adult";
            }
        }
    }
}
```

**Example After Refactoring:**

```java
public String getMembershipType(int age, boolean isStudent) {
    if (age < 12) return "Child";
    if (age < 18) return "Teen";
    if (isStudent) return "Student";
    return "Adult";
}
```

By using guard clauses, special cases (`age < 12`, `age < 18`, `isStudent`) are handled immediately. The final return is the default, making the flow of logic clearer and easier to follow.

### 4. Replace Conditional with Polymorphism

**Problem:** Conditionals vary behavior based on object types or properties.

**Solution:** Use polymorphism by creating subclasses and overriding methods for specific behavior.

**Example Before Refactoring:**

```java
if (shapeType.equals("Circle")) {
    drawCircle();
} else if (shapeType.equals("Square")) {
    drawSquare();
} else if (shapeType.equals("Triangle")) {
    drawTriangle();
}
```

Adding a new shape would require modifying this `if-else` block, which violates the **Open/Closed Principle**.
**Example After Refactoring:**

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle");
    }
}

class Square extends Shape {
    void draw() {
        System.out.println("Drawing Square");
    }
}

class Triangle extends Shape {
    void draw() {
        System.out.println("Drawing Triangle");
    }
}

// Usage
Shape shape = new Circle();
shape.draw();
```

Now, adding a new shape only requires creating a new subclass of `Shape`, no changes to existing code are needed.

<div id = "solid-principles" \>

# SOLID Principles

<div id = "solid-intro" \>

## **Introduction to SOLID Principles**

The SOLID principles are guidelines in **object-oriented programming** that help developers create robust, maintainable, and scalable software. These principles focus on addressing common issues like code rot, poor cohesion, and tight coupling, ultimately ensuring that the software remains adaptable to future requirements.

---

### **Code Rot**

**Code rot** refers to the gradual degradation of a codebase over time, often leading to reduced maintainability and increased technical debt. The following factors contribute to code rot:

1. **Rigidity**: The source code is hard to modify. Changing one feature often requires changing multiple parts of the code, making updates difficult.

2. **Fragility**: Changes in one area of the code cause unexpected issues elsewhere, creating unpredictable and unreliable software behavior.

3. **Immobility**: The inability to reuse components across different projects or within the same project. This limits scalability and leads to redundant code.

---

### **Cohesion & Coupling**

**Cohesion** and **coupling** are essential software design principles that determine the organization and interaction of components in a system.

### **Coupling**

- **Definition**: The degree of dependency between different components or modules.
- **High Coupling (Bad)**:

  - Strong interdependencies between components.
  - Leads to tightly bound systems, making changes more complex.
  - **High Coupling Example**: In this example, the classes are tightly coupled, as `OrderProcessor` directly depends on the implementation details of both `Inventory` and `PaymentGateway`. Any change in these classes will likely require changes in `OrderProcessor`.

    ```java
    class Inventory {
        public boolean checkStock(String product, int quantity) {
            // Implementation to check stock
            System.out.println("Checking stock for product: " + product);
            return true;
        }
    }

    class PaymentGateway {
        public boolean processPayment(String paymentDetails) {
            // Implementation to process payment
            System.out.println("Processing payment: " + paymentDetails);
            return true;
        }
    }

    class OrderProcessor {
        private Inventory inventory = new Inventory();
        private PaymentGateway paymentGateway = new PaymentGateway();

        public void processOrder(String product, int quantity, String paymentDetails) {
            if (inventory.checkStock(product, quantity)) {
                if (paymentGateway.processPayment(paymentDetails)) {
                    System.out.println("Order processed successfully!");
                }
            }
        }
    }
    ```

- **Low Coupling (Good)**:

  - Minimal dependencies between components.
  - Results in a more modular, maintainable system.
  - **Low Coupling Example**: In this example, `OrderProcessor` depends on abstractions (`InventoryService` and `PaymentService`) rather than concrete implementations. This reduces dependency and makes the system more modular.

    ```java
    interface InventoryService {
        boolean checkStock(String product, int quantity);
    }

    class Inventory implements InventoryService {
        @Override
        public boolean checkStock(String product, int quantity) {
            System.out.println("Checking stock for product: " + product);
            return true;
        }
    }

    interface PaymentService {
        boolean processPayment(String paymentDetails);
    }

    class PaymentGateway implements PaymentService {
        @Override
        public boolean processPayment(String paymentDetails) {
            System.out.println("Processing payment: " + paymentDetails);
            return true;
        }
    }

    class OrderProcessor {
        private InventoryService inventoryService;
        private PaymentService paymentService;

        public OrderProcessor(InventoryService inventoryService, PaymentService paymentService) {
            this.inventoryService = inventoryService;
            this.paymentService = paymentService;
        }

        public void processOrder(String product, int quantity, String paymentDetails) {
            if (inventoryService.checkStock(product, quantity)) {
                if (paymentService.processPayment(paymentDetails)) {
                    System.out.println("Order processed successfully!");
                }
            }
        }
    }

    class Main {
        public static void main(String[] args) {
            InventoryService inventoryService = new Inventory();
            PaymentService paymentService = new PaymentGateway();
            OrderProcessor orderProcessor = new OrderProcessor(inventoryService, paymentService);

            orderProcessor.processOrder("Laptop", 1, "CreditCard");
        }
    }
    ```

### **Cohesion**

- **Definition**: The degree to which responsibilities within a module or class are related.
- **High Cohesion**:

  - A module or class has a focused and well-defined purpose.
  - Easier to understand, maintain, and extend.
  - **Cohesion Example**: In this example, the `UserManager` class has a single, well-defined responsibility: managing user-related operations. It adheres to high cohesion principles.

    ```java
    class UserManager {
        public void createUser(String username, String email) {
            System.out.println("Creating user: " + username + " with email: " + email);
        }

        public void updateUser(String username, String newEmail) {
            System.out.println("Updating user: " + username + " with new email: " + newEmail);
        }

        public void deleteUser(String username) {
            System.out.println("Deleting user: " + username);
        }
    }

    class Main {
        public static void main(String[] args) {
            UserManager userManager = new UserManager();

            userManager.createUser("john_doe", "john@example.com");
            userManager.updateUser("john_doe", "john.doe@example.com");
            userManager.deleteUser("john_doe");
        }
    }
    ```

---

### **Abstract & Concrete**

#### **Abstract**:

- Generalized concepts or definitions that define the "what."
- Often represented by interfaces or abstract classes.
- Example: An interface `Shape` with a method `draw()`.

#### **Concrete**:

- Specific implementations that define the "how."
- Example: A `Circle` class implementing the `Shape` interface with its own `draw()` method.

<div id = "solid-srp" \>

## **1. Single Responsibility Principle (SRP)**

**A class should have only one reason to change, meaning it should focus on a single responsibility.**

**Purpose:** To separate concerns and ensure that each class does one thing well.

### **Bad Example (Violation)**

A single class handles multiple responsibilities (data storage and printing).

```java
class Report {
    private String content;

    public Report(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }

    public void print() {
        System.out.println("Printing report: " + content);
    }
}
```

### **Good Example (Adheres to SRP)**

Split responsibilities into separate classes.

```java
class Report {
    private String content;

    public Report(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }
}

class ReportPrinter {
    public void print(Report report) {
        System.out.println("Printing report: " + report.getContent());
    }
}
```

---

<div id = "solid-ocp" \>

## **2. Open/Closed Principle (OCP)**

**A class should be open for extension but closed for modification.**

**Purpose:** To make the code easier to extend without altering existing functionality.

### **Bad Example (Violation)**

Modifying existing code to add new behavior.

```java
class Shape {
    public void draw(String shapeType) {
        if (shapeType.equals("Circle")) {
            System.out.println("Drawing Circle");
        } else if (shapeType.equals("Rectangle")) {
            System.out.println("Drawing Rectangle");
        }
    }
}
```

### **Good Example (Adheres to OCP)**

Extend the behavior using polymorphism.

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing Circle");
    }
}

class Rectangle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing Rectangle");
    }
}
```

---

<div id = "solid-lsp" \>

## **3. Liskov Substitution Principle (LSP)**

**Subtypes must be substitutable for their base types without altering the correctness of the program.**

**Purpose:** To ensure derived classes extend the behavior of base classes without breaking functionality.

This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.
This is the expected behavior, because when we use inheritance we assume that the child class inherits everything that the superclass has. The child class extends the behavior but never narrows it down. Therefore, when a class does not obey this principle, it leads to some nasty bugs that are hard to detect.

### **Bad Example (Violation)**

Subclasses break the behavior of the parent class.

```java
class Bird {
    public void fly() {
        System.out.println("Flying...");
    }
}

class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguins can't fly!");
    }
}
```

### **Good Example (Adheres to LSP)**

Separate behaviors into appropriate interfaces.

```java
interface Flyable {
    void fly();
}

class Sparrow implements Flyable {
    public void fly() {
        System.out.println("Flying...");
    }
}

class Penguin {
    // Penguins don't fly, so no Flyable interface implemented.
}
```

---

<div id = "solid-isp" \>

## **4. Interface Segregation Principle (ISP)**

**A class should not be forced to implement interfaces it does not use.**

**Purpose:** To avoid bloated interfaces and ensure classes depend only on what they need.

### **Bad Example (Violation)**

A single interface forces classes to implement unused methods.

```java
interface Worker {
    void work();
    void eat();
}

class Robot implements Worker {
    public void work() {
        System.out.println("Working...");
    }

    public void eat() {
        throw new UnsupportedOperationException("Robots don't eat!");
    }
}
```

### **Good Example (Adheres to ISP)**

Split interfaces into smaller, focused ones.

```java
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Human implements Workable, Eatable {
    public void work() {
        System.out.println("Working...");
    }

    public void eat() {
        System.out.println("Eating...");
    }
}

class Robot implements Workable {
    public void work() {
        System.out.println("Working...");
    }
}
```

---

<div id = "solid-dip" \>

## **5. Dependency Inversion Principle (DIP)**

**High-level modules should not depend on low-level modules. Both should depend on abstractions.**
Additionally, abstractions should not depend on details. Details should depend on abstractions.
In simpler terms, the DIP suggests that classes should rely on abstractions (e.g., interfaces or abstract classes) rather than concrete implementations.

**Purpose:** To reduce coupling between classes and make the code more flexible.

### **Bad Example (Violation)**

High-level module depends on a low-level module directly.

```java
class Keyboard {
    public void type() {
        System.out.println("Typing...");
    }
}

class Computer {
    private Keyboard keyboard = new Keyboard();

    public void use() {
        keyboard.type();
    }
}
```

### **Good Example (Adheres to DIP)**

High-level module depends on an abstraction.

```java
interface InputDevice {
    void input();
}

class Keyboard implements InputDevice {
    public void input() {
        System.out.println("Typing...");
    }
}

class Mouse implements InputDevice {
    public void input() {
        System.out.println("Clicking...");
    }
}

class Computer {
    private InputDevice inputDevice;

    public Computer(InputDevice inputDevice) {
        this.inputDevice = inputDevice;
    }

    public void use() {
        inputDevice.input();
    }
}
```

---

- **SRP**: Split unrelated responsibilities into separate classes.
- **OCP**: Add new behavior via extension, not modification.
- **LSP**: Ensure subclasses uphold the parent class's behavior.
- **ISP**: Create interfaces tailored to specific needs.
- **DIP**: Rely on abstractions, not concrete implementations.

<div id = "solid-questions" \>

## Solid Principles Practice Questions

### Question 1: For the following scenarios, which SOLID principle violated in each:

1. The CityMap class represents a map consisting of a list of cities with various attributes. Although this represents a single logical object, the CityMap class takes on several very separate pieces of functionality which should, according to this principle, be divided into several classes. Those functionalities include managing the list of cities (add and remove), drawing the map on the screen, and calculating the total population.
2. A Computer object keeps track of its amount of RAM and its OS version. It also has methods for upgrading the RAM and updating the OS. Two classes, a DesktopComputer and a Phone, extend this class and implement its methods. A ComputerUpgrader object claims to be able to upgrade any Computer (that is, add more RAM and update the OS), but it really can’t add more RAM to a phone, so it must check to make sure the Computer object it has been given isn’t a Phone.
3. A single interface, Game" is created, for two classes, SingleplayerGame and MultiplayerGame. This is on the surface a logical structure. However, in this case, the methods getServerList and pauseGame, published in the Game interface, are not used by both clients (As a MultiplayerGame cannot be paused, and a SingleplayerGame does not have servers). Because of this mismatch, the SingleplayerGame is forced to throw an UnsupportedOperationException when getServerList is called on it, and MultiplayerGame is forced to throw an UnsupportedOperationException when pauseGame is called on it.

#### **Answer:**

1. **CityMap Class:** Violates the Single Responsibility Principle (SRP). The CityMap class is responsible for multiple tasks (managing cities, drawing the map, calculating population), and it should only have one responsibility. These should be separated into different classes.
2. **Computer and ComputerUpgrader:** Violates the Liskov Substitution Principle (LSP). The ComputerUpgrader assumes that any Computer can be upgraded, but a Phone cannot have its RAM upgraded. The upgrader should handle the differences between Computer types properly without making assumptions.
3. **Game Interface:** Violates the Interface Segregation Principle (ISP). The Game interface is forcing SingleplayerGame and MultiplayerGame to implement methods that don't apply to them (e.g., SingleplayerGame doesn’t need getServerList, and MultiplayerGame doesn’t need pauseGame). Separate interfaces should be used for the different functionalities.

### Question 2: Which SOLID principle can solve the problem in this code segment?

```java
public class DeliveryDriver{
    public void deliverProduct(Product product) {...}
}
public class DeliveryCompany{
    public void sendProduct(Product product){
    DeliveryDriver delivery = new DeliveryDriver();
    delivery.deliverProduct(product);
    }
}
```

#### **Answer:**

The problem in the code violates the **Dependency Inversion Principle (DIP)**, as `DeliveryCompany` directly depends on the `DeliveryDriver` class.

**Refactored code:**

```java
// Define an interface for the delivery service
public interface IDeliveryService {
    void deliverProduct(Product product);
}

// Implement the delivery service
public class DeliveryDriver implements IDeliveryService {
    public void deliverProduct(Product product) {
        // delivery logic here
    }
}

// Refactor DeliveryCompany to depend on the abstraction
public class DeliveryCompany {
    private IDeliveryService deliveryService;

    // Constructor injection to provide dependency
    public DeliveryCompany(IDeliveryService deliveryService) {
        this.deliveryService = deliveryService;
    }

    public void sendProduct(Product product) {
        deliveryService.deliverProduct(product);
    }
}
```

Now, `DeliveryCompany` depends on `IDeliveryService`, which allows for flexibility in using different delivery services.

### Question 3: Which SOLID principle can solve the problem in this code segment? Write the solution code.

```java
class Human {
    private String name; private String age;
    private String country;
    private String city; private String street;
    private String house; private String quarter;

    public String getFullAddress() {
    StringBuilder result = new StringBuilder();
    return result.append(country).append(", ").append(city)
    .append(", ").append(street).append(", ").append(house)
    .append(" ").append(quarter).toString();
    }
}
```

#### **Answer:**

The problem in this code violates the **Single Responsibility Principle (SRP)**. The `Human` class is responsible for both managing a person's details (name, age) and constructing a full address, which is not the primary responsibility of the class.

**Refactored code:**

```java
// Address class handles the responsibility of creating and managing an address
public class Address {
    private String country;
    private String city;
    private String street;
    private String house;
    private String quarter;

    public Address(String country, String city, String street, String house, String quarter) {
        this.country = country;
        this.city = city;
        this.street = street;
        this.house = house;
        this.quarter = quarter;
    }

    public String getFullAddress() {
        StringBuilder result = new StringBuilder();
        return result.append(country).append(", ").append(city)
                     .append(", ").append(street).append(", ").append(house)
                     .append(" ").append(quarter).toString();
    }
}

// Human class focuses on human-specific details, delegating address creation to Address
public class Human {
    private String name;
    private String age;
    private Address address;

    public Human(String name, String age, Address address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    public String getFullAddress() {
        return address.getFullAddress();
    }
}
```

In this solution:

- **The Address class** now has the sole responsibility for managing and constructing an address.
- **The Human class** focuses on human-specific details and delegates the address construction to the Address class.

This follows the **Single Responsibility Principle (SRP)** and makes the code more maintainable and easier to extend.

<div id="dp"\>

# Design Patterns

<div id="dp-intro"\>

## Introduction to Design Patterns

**Design patterns** are reusable solutions to common problems in software design. They are not specific pieces of code but rather templates that provide a structured approach to solving design challenges. Design patterns promote best practices, making code more maintainable, scalable, and understandable.

### Advantages of Using Design Patterns:

1. **Proven Solutions**: They offer reliable solutions tested and refined over time.
2. **Shared Vocabulary**: Patterns create a common language for developers, simplifying communication.
3. **Reusable Architectures**: They enable large-scale reuse of software designs, saving time and effort.

---

### Drawbacks of Design Patterns:

1. **Human-Driven Integration**: Applying patterns requires experience and thoughtful consideration, making it labor-intensive.
2. **Experience-Based Validation**: Patterns are validated through practice and discussion, not automated testing.

---

### Key Concepts of Design Patterns:

1. **Pattern Name**: A concise, memorable name that helps communicate the idea.
2. **Problem**: A clear description of the scenario where the pattern is applicable, including the conditions it addresses.
3. **Solution**: The design elements, their roles, and how they interact to solve the problem.
4. **Consequences**: The benefits and trade-offs of using the pattern, including its impact on system flexibility, extensibility, and portability.

<div id="dp-creational"\>

## **Creational Design Patterns**

Creational design patterns focus on the process of object creation. They abstract the instantiation logic to ensure flexibility and reusability, allowing you to create objects in a way that suits the situation without tightly coupling the code to specific implementations.

---

<div id="dp-singleton"\>

## **Singleton Design Pattern**

The **Singleton** pattern ensures a class has only one instance and provides a global point of access to it.

**Problem**: You need to ensure only one instance of a class exists and provide a global point of access to it (e.g., managing configurations or shared resources).  
**Solution**: Restrict class instantiation by using a private constructor and provide a static method to return the single instance.

**Key Points**:

1. Restricts instantiation of the class to a single object.
2. Provides a global method to access the instance.

### **Example (Double Checked Locking)**:

```java
public class Singleton {
    // Volatile ensures the instance is correctly handled in a multi-threaded environment
    private static volatile Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() { }

    // Method to provide global access to the Singleton instance
    public static Singleton getInstance() {
        if (instance == null) { // First check (no locking)
            synchronized (Singleton.class) { // Lock only for the first instance creation
                if (instance == null) { // Second check
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

**Usage**:

```java
Singleton obj1 = Singleton.getInstance();
Singleton obj2 = Singleton.getInstance();
// obj1 and obj2 are the same instance.
```

### **Practice Question: Singleton Logger**

Create a logging system where only one instance of the logger exists throughout the application. The logger should:

1. Provide a `log(String message)` method to display a message to the console.
2. Maintain a history of all logged messages (stored in a list).
3. Allow retrieving the logged messages through a method `getHistory()`.

**Requirements:**

- Ensure the logger has only one instance.
- Demonstrate the singleton behavior by logging messages from different parts of your program.

#### **Answer**:

```java
import java.util.ArrayList;
import java.util.List;

// Singleton Logger Class
class Logger {
    private static Logger instance; // Single instance of Logger
    private List<String> history;   // List to store logged messages

    // Private constructor to prevent instantiation
    private Logger() {
        history = new ArrayList<>();
    }

    // Public method to get the single instance of Logger
    public static Logger getInstance() {
        if (instance == null) {
            synchronized (Logger.class) { // Thread-safe initialization
                if (instance == null) {
                    instance = new Logger();
                }
            }
        }
        return instance;
    }

    // Method to log a message
    public void log(String message) {
        history.add(message);
        System.out.println("Log: " + message);
    }

    // Method to retrieve log history
    public List<String> getHistory() {
        return new ArrayList<>(history); // Return a copy to preserve encapsulation
    }
}

// Demonstration
public class SingletonLoggerDemo {
    public static void main(String[] args) {
        // Retrieve the single instance of Logger
        Logger logger1 = Logger.getInstance();

        // Log messages from different parts of the program
        logger1.log("Initializing application...");
        logger1.log("User login successful.");

        // Retrieve the same logger instance elsewhere
        Logger logger2 = Logger.getInstance();
        logger2.log("Fetching data from database...");
        logger2.log("Application shutting down.");

        // Ensure both logger1 and logger2 are the same instance
        System.out.println("Logger instances are the same: " + (logger1 == logger2));

        // Display log history
        System.out.println("\nLog History:");
        for (String message : logger1.getHistory()) {
            System.out.println(message);
        }
    }
}
```

---

**Explanation**

1. **Singleton Pattern**:

   - The `Logger` class ensures only one instance exists using the `getInstance()` method.
   - The instance is lazily initialized and made thread-safe with `synchronized`.

2. **Logging Messages**:

   - The `log(String message)` method adds messages to a `history` list and prints them to the console.

3. **History Retrieval**:

   - The `getHistory()` method returns a copy of the `history` list to ensure encapsulation.

4. **Demonstrating Singleton Behavior**:
   - The `main` method shows `logger1` and `logger2` pointing to the same instance, and all messages are stored in a shared history.

---

<div id="dp-factory"\>

## **Factory Design Pattern**

The **Factory** pattern provides a way to create objects without specifying their concrete types.

**Problem**: You need to create objects without exposing their instantiation logic or when the exact type of object to create depends on dynamic input.  
**Solution**: Define a method or class that encapsulates the logic for creating objects and returns them based on conditions or parameters.

### **Example**:

```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

class Rectangle implements Shape {
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}

class ShapeFactory {
    public static Shape getShape(String type) {
        if (type.equalsIgnoreCase("Circle")) {
            return new Circle();
        } else if (type.equalsIgnoreCase("Rectangle")) {
            return new Rectangle();
        }
        return null;
    }
}
```

**Usage**:

```java
Shape shape1 = ShapeFactory.getShape("Circle");
shape1.draw(); // Output: Drawing a Circle

Shape shape2 = ShapeFactory.getShape("Rectangle");
shape2.draw(); // Output: Drawing a Rectangle
```

### **Practice Question: Payment Processing System**

**Scenario**:  
You are building a **payment processing system** for an online store. The system must handle different payment methods: **Credit Card**, **PayPal**, and **Bank Transfer**. Each payment method processes transactions differently but implements the same interface to ensure consistency.

---

**Requirements**:

1. Create an interface `PaymentProcessor` with a method `processPayment(double amount)`.
2. Implement concrete classes for each payment method (`CreditCardPayment`, `PayPalPayment`, and `BankTransferPayment`).
3. Use the **Factory Method Pattern** to allow the system to create the appropriate payment processor based on the user input.
4. Write a `PaymentProcessorFactory` class that provides the factory method.
5. In the `Main` class, simulate a scenario where the user selects a payment method and processes a payment of $150.

---

**Expected Output**:  
When you run the program, it should print something like:

- `Processing $150 via Credit Card.`
- `Processing $150 via PayPal.`
- `Processing $150 via Bank Transfer.`

#### **Solution:**

```java
// PaymentProcessor Interface
interface PaymentProcessor {
    void processPayment(double amount);
}

// Concrete Class: CreditCardPayment
class CreditCardPayment implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing $" + amount + " via Credit Card.");
    }
}

// Concrete Class: PayPalPayment
class PayPalPayment implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing $" + amount + " via PayPal.");
    }
}

// Concrete Class: BankTransferPayment
class BankTransferPayment implements PaymentProcessor {
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing $" + amount + " via Bank Transfer.");
    }
}

// Factory Class: PaymentProcessorFactory
class PaymentProcessorFactory {
    public static PaymentProcessor getPaymentProcessor(String paymentMethod) {
        switch (paymentMethod.toLowerCase()) {
            case "creditcard":
                return new CreditCardPayment();
            case "paypal":
                return new PayPalPayment();
            case "banktransfer":
                return new BankTransferPayment();
            default:
                throw new IllegalArgumentException("Invalid payment method: " + paymentMethod);
        }
    }
}

// Main Class: Simulating the Payment System
public class PaymentProcessingSystem {
    public static void main(String[] args) {
        // Simulate user input
        String selectedPaymentMethod = "CreditCard"; // User selects Credit Card
        double amount = 150.0;

        // Get the appropriate payment processor
        PaymentProcessor processor = PaymentProcessorFactory.getPaymentProcessor(selectedPaymentMethod);

        // Process the payment
        processor.processPayment(amount);
    }
}
```

---

**Explanation**

1. **Interface (`PaymentProcessor`)**:  
   Defines the common method `processPayment(double amount)` that all payment methods must implement.

2. **Concrete Classes**:  
   Each class (`CreditCardPayment`, `PayPalPayment`, `BankTransferPayment`) implements `PaymentProcessor` and provides its own implementation of `processPayment()`.

3. **Factory Class (`PaymentProcessorFactory`)**:

   - The factory method `getPaymentProcessor(String paymentMethod)` creates and returns the appropriate payment processor instance based on the input.
   - Uses a `switch` statement to decide which class to instantiate.

4. **Main Class (`PaymentProcessingSystem`)**:
   - Simulates the selection of a payment method by the user.
   - Calls the factory method to get the appropriate `PaymentProcessor`.
   - Processes a payment of $150.

---

<div id="dp-builder"\>

## **Builder Design Pattern**

The **Builder** pattern separates the construction of a complex object from its representation, allowing you to create different representations of the object.

**Problem**: Constructing an object with many optional parameters or complex steps can lead to code that is difficult to read and subject to errors.  
**Solution**: Separate the object creation process into multiple steps using a builder class, allowing for step-by-step construction with clear and customizable configurations.

**Example**:

```java
class Car {
    private String engine;
    private int wheels;
    private String color;

    public Car(String engine, int wheels, String color) {
        this.engine = engine;
        this.wheels = wheels;
        this.color = color;
    }
}

class CarBuilder {
    private String engine;
    private int wheels;
    private String color;

    public CarBuilder setEngine(String engine) {
        this.engine = engine;
        return this;
    }

    public CarBuilder setWheels(int wheels) {
        this.wheels = wheels;
        return this;
    }

    public CarBuilder setColor(String color) {
        this.color = color;
        return this;
    }

    public Car build() {
        return new Car(engine, wheels, color);
    }
}
```

**Usage**:

```java
CarBuilder carBuilder = new CarBuilder();
carBuilder.setEngine("V8")
        .setWheels(4)
        .setColor("Red");

Car car = carBuilder.build();
```

### **Practice Question: Computer Builder**

**Scenario**:  
You are creating a system to build customized **computers** for an online store. A computer consists of a **CPU**, **RAM**, **storage**, **graphics card**, and an optional **operating system**. Customers should be able to choose specific configurations for each component.

**Task**:

1. Implement a `Computer` class to represent the final computer configuration.
2. Use the Builder design pattern to construct different types of computers, such as:
   - **Gaming PC**: High-end CPU, 16GB RAM, 1TB SSD, high-performance graphics card, and Windows OS.
   - **Office PC**: Mid-range CPU, 8GB RAM, 500GB HDD, integrated graphics, and no OS.
3. In the `main` method, demonstrate creating both computer configurations using the builder and print their details.

#### Solution:

```java
class Computer {
    String cpu, ram, storage, gpu, os;

    public Computer(String cpu, String ram, String storage, String gpu, String os) {
        this.cpu = cpu;
        this.ram = ram;
        this.storage = storage;
        this.gpu = gpu;
        this.os = os;
    }
}

class ComputerBuilder {
    String cpu, ram, storage, gpu, os;

    ComputerBuilder setCpu(String cpu) {
        this.cpu = cpu;
        return this;
    }

    ComputerBuilder setRam(String ram) {
        this.ram = ram;
        return this;
    }

    ComputerBuilder setStorage(String storage) {
        this.storage = storage;
        return this;
    }

    ComputerBuilder setGpu(String gpu) {
        this.gpu = gpu;
        return this;
    }

    ComputerBuilder setOs(String os) {
        this.os = os;
        return this;
    }

    Computer build() {
        return new Computer(cpu, ram, storage, gpu, os);
    }
}

public class ComputerBuilderApp {
    public static void main(String[] args) {
        Computer gamingPc = new ComputerBuilder()
                .setCpu("High-end")
                .setRam("16GB")
                .setStorage("1TB SSD")
                .setGpu("High-performance")
                .setOs("Windows")
                .build();

        Computer officePc = new ComputerBuilder()
                .setCpu("Mid-range")
                .setRam("8GB")
                .setStorage("500GB HDD")
                .setGpu("Integrated")
                .setOs("No OS")
                .build();
    }
}
```

---

These patterns address common problems in software design:

- **Singleton** for managing a single instance.
- **Factory** for dynamic object creation.
- **Builder** for constructing complex objects in a step-by-step manner.

<div id="dp-structural"\>

## **Structural Design Patterns**

Structural design patterns focus on organizing and constructing class structures in different ways. They utilize inheritance and composition techniques to build complex objects from simpler ones.

These patterns address design challenges related to the arrangement and relationships of classes and objects.

<div id="dp-adapter"\>

## **Adapter Design Pattern**

The **Adapter** Pattern allows incompatible interfaces to work together by providing a bridge between them. It converts the interface of a class into one that a client expects.

**Problem:** You have two incompatible interfaces, and you need them to work together.  
**Solution:** The Adapter pattern acts as a bridge, converting one interface into another that the client expects.

**Key Components**:

1. **Target**: The interface that the client expects to work with.
2. **Adapter**: Converts the interface of the Adaptee into the Target interface.
3. **Adaptee**: An existing class that needs adapting.
4. **Client**: The class that interacts with the Target interface.

### **Example:**

Imagine you have a phone charger that works with USB-C, but your power bank only supports Micro-USB. You use an **adapter** to make them compatible.

```java
// Target Interface
interface UsbC {
    void connectUsbC();
}

// Adaptee
class MicroUsbDevice {
    void connectMicroUsb() {
        System.out.println("Micro-USB device connected.");
    }
}

// Adapter
class UsbCAdapter implements UsbC {
    MicroUsbDevice microUsbDevice;

    UsbCAdapter(MicroUsbDevice microUsbDevice) {
        this.microUsbDevice = microUsbDevice;
    }

    @Override
    public void connectUsbC() {
        microUsbDevice.connectMicroUsb();
    }
}

// Client
public class AdapterExample {
    public static void main(String[] args) {
        MicroUsbDevice oldDevice = new MicroUsbDevice();
        UsbC usbCAdapter = new UsbCAdapter(oldDevice);

        System.out.println("Using an adapter to connect:");
        usbCAdapter.connectUsbC();
    }
}
```

- **Problem:** The client and the service have incompatible interfaces.
- **Solution:** The adapter translates the interface of the service into something the client understands.
- **Explanation of Example:** The `UsbCAdapter` allows the `MicroUsbDevice` to connect via a USB-C interface, bridging the gap between the two incompatible systems.

### **Practice Question: Shape Adapter**

**Scenario**:  
You are developing a drawing application that works with a `Shape` interface. The existing interface supports `Rectangle` and `Circle` shapes. However, a third-party library provides `Polygon` with its own methods. You want to adapt the `Polygon` class to work with the existing `Shape` interface without altering the third-party library.

1. Define a `Shape` interface with a method `draw()`.
2. Implement `Rectangle` and `Circle` classes based on the `Shape` interface.
3. Create a third-party class `Polygon` with a method `display()`.
4. Write an `Adapter` class to make `Polygon` compatible with `Shape`.
5. Test your code in a `main` method by using all three shapes (Rectangle, Circle, Polygon).

#### **Solution:**

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

interface Shape {
    void draw();
}

class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}

class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

class Polygon {
    public void display() {
        System.out.println("Drawing a Polygon");
    }
}

class PolygonAdapter implements Shape {
    Polygon polygon;

    PolygonAdapter() {
        this.polygon = new Polygon();
    }

    @Override
    public void draw() {
        this.polygon.display();
    }
}

public class AdapterPractice {
    public static void main(String[] args) {
        List<Shape> shapes = new ArrayList<>(Arrays.asList(new Rectangle(), new Circle(), new PolygonAdapter()));
        for (Shape shape : shapes)
            shape.draw();
    }
}
```

---

<div id="dp-composite"\>

## **Composite Design Pattern**

The **Composite** Pattern lets you treat individual objects and compositions of objects uniformly. It is used when you have a tree structure of objects.

**Problem:** You need to represent a hierarchy of objects (like a tree structure), where individual objects and groups of objects should be treated uniformly.  
**Solution:** The Composite pattern lets you compose objects into tree structures, allowing clients to work with individual objects and composites uniformly.

**Key Components**:

1. **Component (Interface or Abstract Class):** Declares common operations for both leaves and composites.
2. **Leaf:** Represents a single object with no children.
3. **Composite:** Represents a group of objects, which could include other composites or leaves.
4. **Client:** Interacts with components through the common interface.

### **Example:**

Think of a folder on your computer that contains files and other folders. You want to treat the folder and its contents uniformly—for instance, getting the size of the folder includes the sizes of its files and subfolders.

```java
// Component
import java.util.ArrayList;
import java.util.List;

interface FileSystem {
    void showDetails();
}

// Leaf
class File implements FileSystem {
    private String name;

    File(String name) {
        this.name = name;
    }

    @Override
    public void showDetails() {
        System.out.println("File: " + name);
    }
}

// Composite
class Folder implements FileSystem {
    private String name;
    private List<FileSystem> contents = new ArrayList<>();

    Folder(String name) {
        this.name = name;
    }

    void add(FileSystem fileSystem) {
        contents.add(fileSystem);
    }

    @Override
    public void showDetails() {
        System.out.println("Folder: " + name);
        for (FileSystem item : contents) {
            item.showDetails();
        }
    }
}

// Client
public class CompositeExample {
    public static void main(String[] args) {
        File file1 = new File("Document1.txt");
        File file2 = new File("Photo.jpg");

        Folder smallFolder = new Folder("MyFolder");
        smallFolder.add(file1);
        smallFolder.add(file2);

        Folder largeFolder = new Folder("MyLargeFolder");
        largeFolder.add(smallFolder);

        System.out.println("Folder and contents:");
        largeFolder.showDetails();
    }
}
```

- **Problem:** You need to handle individual objects and groups of objects in a uniform way.
- **Solution:** Create a structure (like a tree) where both individual objects and composites (groups) can be treated the same.
- **Explanation of Example:** The `Folder` can contain both `File` objects and other `Folder` objects. The `showDetails` method works for individual files and nested folders alike.

### **Practice Question: Company Department Hierarchy**

**Scenario**:  
Design a system to represent the hierarchy of a company's departments and employees.

- **Employees** are the leaf nodes, as they don't have any subordinates.
- **Departments** are composite nodes that can contain other departments or employees.

---

**Requirements**:

1. Create an interface `OrganizationComponent` with methods to:

   - Display details of the component.
   - Add subcomponents (for departments only).

2. Implement the following classes:

   - `Employee`: Represents individual employees (leaf nodes).
   - `Department`: Represents a department, which can contain employees and other departments (composite nodes).

3. Use the **Composite Pattern** to allow the hierarchy to treat individual employees and departments uniformly.
4. In the `Main` class, simulate adding employees and departments, and display the entire company hierarchy.

#### **Solution:**

```java
import java.util.ArrayList;
import java.util.List;

// Component Interface
interface OrganizationComponent {
    void showDetails(); // Display the details of the component
}

// Leaf: Employee
class Employee implements OrganizationComponent {
    String name;

    public Employee(String name) {
        this.name = name;
    }

    @Override
    public void showDetails() {
        System.out.println("Employee: " + name);
    }
}

// Composite: Department
class Department implements OrganizationComponent {
    String name;
    List<OrganizationComponent> components = new ArrayList<>();

    public Department(String name) {
        this.name = name;
    }

    // Add a subcomponent (either Employee or Department)
    public void addComponent(OrganizationComponent component) {
        components.add(component);
    }

    @Override
    public void showDetails() {
        System.out.println("Department: " + name);
        for (OrganizationComponent component : components) {
            component.showDetails();
        }
    }
}

// Main Class: Demonstrate the Composite Pattern
public class CompanyDepartment {
    public static void main(String[] args) {
        Department sales = new Department("Sales");
        sales.addComponent(new Employee("Amr Mosallem"));
        sales.addComponent(new Employee("John Doe"));

        Department marketing = new Department("Marketing");
        marketing.addComponent(new Employee("Alice Smith"));
        marketing.addComponent(new Employee("Bob Johnson"));

        Department headQuarters = new Department("Head Quarters");
        headQuarters.addComponent(sales);
        headQuarters.addComponent(marketing);

        headQuarters.showDetails();
    }
}
```

---

<div id="dp-facade"\>

## **Facade Design Pattern**

The **Facade** Pattern provides a simplified interface to a complex subsystem. It hides the complexity of the system and provides an easy-to-use API.

**Problem:**
A system has multiple complex subsystems, and you want to provide a simplified interface to clients.

**Solution:**
The Facade pattern provides a unified, higher-level interface that simplifies interactions with the subsystems.

---

### Example

When you turn on your TV, you don’t need to handle individual components like power, speakers, and display. Instead, you press one button, and everything works behind the scenes. The **facade** simplifies this process.

```java
// Subsystems
class Power {
    void turnOn() {
        System.out.println("Power on.");
    }
}

class Speakers {
    void activate() {
        System.out.println("Speakers activated.");
    }
}

class Display {
    void start() {
        System.out.println("Display started.");
    }
}

// Facade
class TelevisionFacade {
    private Power power;
    private Speakers speakers;
    private Display display;

    TelevisionFacade() {
        power = new Power();
        speakers = new Speakers();
        display = new Display();
    }

    void turnOnTv() {
        power.turnOn();
        speakers.activate();
        display.start();
    }
}

// Client
public class FacadeExample {
    public static void main(String[] args) {
        TelevisionFacade tv = new TelevisionFacade();
        System.out.println("Turning on the TV:");
        tv.turnOnTv();
    }
}
```

- **Problem:** A system has multiple complex subsystems that are hard to interact with directly.
- **Solution:** A facade provides a single, simplified interface to interact with those subsystems.
- **Explanation of Example:** The `TelevisionFacade` hides the complexity of managing `Power`, `Speakers`, and `Display` subsystems, allowing the client to turn on the TV with one method call.

### **Practice Question: Home Entertainment System**

#### **Scenario**:

You are tasked with creating a system to simplify the operation of a **home entertainment system**. The system consists of the following subsystems:

1. **TV**
2. **Sound System**
3. **Streaming Service**

Users should be able to:

1. Start a "Movie Night" with one action that turns on the TV, sets up the sound system, and starts the streaming service.
2. End "Movie Night" with one action that turns off all the subsystems.

**Requirements**:

1. Create classes for each subsystem (`TV`, `SoundSystem`, `StreamingService`) with methods to turn them on, off, or start specific functionalities.
2. Implement a **Facade Class** (`HomeTheaterFacade`) to simplify interactions with these subsystems.
3. In the `Main` class, demonstrate starting and ending "Movie Night" using the facade.

---

#### **Solution:**

```java
// Subsystem: TV
class TV {
    public void turnOn() {
        System.out.println("TV is turned ON.");
    }

    public void turnOff() {
        System.out.println("TV is turned OFF.");
    }
}

// Subsystem: Sound System
class SoundSystem {
    public void turnOn() {
        System.out.println("Sound System is turned ON.");
    }

    public void turnOff() {
        System.out.println("Sound System is turned OFF.");
    }

    public void setSurroundSound() {
        System.out.println("Sound System is set to Surround Sound mode.");
    }
}

// Subsystem: Streaming Service
class StreamingService {
    public void startStreaming() {
        System.out.println("Streaming Service is started.");
    }

    public void stopStreaming() {
        System.out.println("Streaming Service is stopped.");
    }
}

// Facade: Home Theater
class HomeTheaterFacade {
    private TV tv;
    private SoundSystem soundSystem;
    private StreamingService streamingService;

    public HomeTheaterFacade() {
        this.tv = new TV();
        this.soundSystem = new SoundSystem();
        this.streamingService = new StreamingService();
    }

    public void startMovieNight() {
        System.out.println("Starting Movie Night...");
        tv.turnOn();
        soundSystem.turnOn();
        soundSystem.setSurroundSound();
        streamingService.startStreaming();
        System.out.println("Enjoy your movie!");
    }

    public void endMovieNight() {
        System.out.println("Ending Movie Night...");
        streamingService.stopStreaming();
        soundSystem.turnOff();
        tv.turnOff();
        System.out.println("Movie Night ended.");
    }
}

// Main Class: Demonstration
public class FacadePatternDemo {
    public static void main(String[] args) {
        HomeTheaterFacade homeTheater = new HomeTheaterFacade();

        // Start Movie Night
        homeTheater.startMovieNight();

        // End Movie Night
        homeTheater.endMovieNight();
    }
}
```

<div id="dp-behavioral"\>

## **Behavioral Design Patterns**

**Behavioral patterns** focus on how objects interact and communicate with one another. They define clear protocols for these interactions to ensure flexibility and efficiency. These patterns make it easier to design loosely coupled systems, where each part can function independently but still cooperate effectively.

<div id="dp-strategy"\>

## **Strategy Design Pattern**

The **Strategy** Pattern is a behavioral design pattern that allows you to define a family of algorithms, encapsulate them in separate classes, and make them interchangeable. It enables selecting an algorithm’s behavior at runtime, promoting flexibility and code reusability.

**Problem:** You have multiple algorithms or behaviors, and you want to select one at runtime without changing the code that uses it.  
**Solution:** Encapsulate each algorithm in its own class and make them interchangeable. Use a context class to decide which algorithm to use.

### **Example**

You are designing a transportation app. Depending on the user's choice, the app should calculate the travel time using different transportation modes: car, bus, or bike. The calculation logic differs for each mode.

#### **Without Strategy Pattern**:

```java
class Transportation {
    void calculateTime(String mode) {
        if (mode.equals("car")) {
            System.out.println("Calculating time by car...");
        } else if (mode.equals("bus")) {
            System.out.println("Calculating time by bus...");
        } else if (mode.equals("bike")) {
            System.out.println("Calculating time by bike...");
        } else {
            System.out.println("Invalid mode!");
        }
    }
}

public class ProblemExample {
    public static void main(String[] args) {
        Transportation transport = new Transportation();
        transport.calculateTime("car");
        transport.calculateTime("bike");
    }
}
```

#### **Solution with Strategy Pattern:**

```java
// Strategy Interface
interface TravelStrategy {
    void calculateTime();
}

// Concrete Strategies
class Car implements TravelStrategy {
    @Override
    public void calculateTime() {
        System.out.println("Calculating time by car...");
    }
}

class Bus implements TravelStrategy {
    @Override
    public void calculateTime() {
        System.out.println("Calculating time by bus...");
    }
}

class Bike implements TravelStrategy {
    @Override
    public void calculateTime() {
        System.out.println("Calculating time by bike...");
    }
}

// Context
class Transportation {
    private TravelStrategy mode;

    void setTravelStrategy(TravelStrategy mode) {
        this.mode = mode;
    }

    void calculateTime() {
        mode.calculateTime();
    }
}

// Client
public class StrategyExample {
    public static void main(String[] args) {
        Transportation transport = new Transportation();

        transport.setTravelStrategy(new Car());
        transport.calculateTime();

        transport.setTravelStrategy(new Bike());
        transport.calculateTime();
    }
}
```

### Practice Question: Payment Processor

**Problem**:  
You are building a payment system that supports multiple payment methods, such as Credit Card, PayPal, and Smart Wallet. Each payment method has a different implementation for processing payments. The system should be able to switch between payment methods dynamically without modifying the code for the payment processor.

**Task**:  
Implement the Strategy Design Pattern to handle multiple payment methods. Create a `PaymentProcessor` class that can use different payment strategies. The system should process payments using the strategy specified at runtime.

---

#### **Solution:**
```java
// Strategy Interface
interface PaymentStrategy {
    void pay(double amount);
}

// Concrete Strategies
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using Credit Card ending in " + cardNumber.substring(cardNumber.length() - 4));
    }
}

class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using PayPal account: " + email);
    }
}

class SmartWalletPayment implements PaymentStrategy {
    private String walletAddress;

    public SmartWalletPayment(String walletAddress) {
        this.walletAddress = walletAddress;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using smart wallet: " + walletAddress);
    }
}

// Context
class PaymentProcessor {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void processPayment(double amount) {
        if (paymentStrategy == null) {
            throw new IllegalStateException("Payment strategy is not set!");
        }
        paymentStrategy.pay(amount);
    }
}

// Client
public class StrategyPatternExample {
    public static void main(String[] args) {
        PaymentProcessor processor = new PaymentProcessor();

        // Use Credit Card payment
        processor.setPaymentStrategy(new CreditCardPayment("1234-5678-9876-5432"));
        processor.processPayment(100.00);

        // Switch to PayPal payment
        processor.setPaymentStrategy(new PayPalPayment("user@example.com"));
        processor.processPayment(200.50);

        // Switch to Cryptocurrency payment
        processor.setPaymentStrategy(new SmartWalletPayment("1A2B3C4D5E6F"));
        processor.processPayment(500.75);
    }
}
```
**Explanation:**
1. **Strategy Interface**: `PaymentStrategy` defines a common interface for all payment methods.
2. **Concrete Strategies**: 
   - `CreditCardPayment` handles payments via credit cards.
   - `PayPalPayment` handles payments via PayPal.
   - `SmartWalletPayment` handles payments via the bank.
3. **Context**: The `PaymentProcessor` class uses a `PaymentStrategy` to process payments. It is flexible and can switch strategies dynamically.
4. **Client**: The `main` method demonstrates how to use the `PaymentProcessor` with different payment strategies. The payment method is set at runtime using the `setPaymentStrategy` method.

This design pattern ensures that the code is flexible, extendable, and adheres to the Open/Closed Principle, as new payment methods can be added without modifying existing code.

---

<div id="dp-observer"\>

## **Observer Design Pattern**

The **Observer** Pattern is a behavioral design pattern that defines a one-to-many relationship between objects. When the state of the subject (e.g., stock price) changes, all its dependents (observers) are notified automatically, promoting loose coupling and scalability.

**Problem:** An object (subject) needs to notify multiple other objects (observers) whenever its state changes.  
**Solution:** Define a one-to-many relationship between the subject and its observers. When the subject changes, it automatically notifies all observers.

### **Example:**
You are designing a notification service. Depending on the user's subscription type, the service should send updates via email or SMS. The system should allow adding or removing subscribers dynamically and notify all active subscribers when a new message is sent.

#### **Before Applying the Observer Pattern:**
Here is an example of a notification system before implementing the Observer Pattern. All notifications are hardcoded, making it difficult to add or remove notification types dynamically.

```java
// Notification System Without Observer Pattern
class NotificationService {
    void sendNotification(String message) {
        sendEmail(message);
        sendSms(message);
    }

    private void sendEmail(String message) {
        System.out.println("Alice received email: " + message);
    }

    private void sendSms(String message) {
        System.out.println("Bob received SMS: " + message);
    }
}

// Client
public class BeforeObserverExample {
    public static void main(String[] args) {
        NotificationService service = new NotificationService();

        System.out.println("Sending notification 1:");
        service.sendNotification("Your package has shipped!");

        // Removing email notifications requires manually modifying the code.
        System.out.println("\nSending notification 2:");
        service.sendNotification("Your package is out for delivery!");
    }
}
```

**Issues Before Applying the Observer Pattern**
1. **Hardcoding**: Adding or removing notification types (e.g., email, SMS) requires direct modification of the code.  
2. **Scalability**: Adding a new notification type (e.g., push notifications) requires adding a new method and changing the logic in `sendNotification`. (Violating Open-Closed Principle)  
3. **Tight Coupling**: The `NotificationService` class depends directly on the notification methods, making the system inflexible.  

#### **After Applying the Observer Pattern:**
The Observer Pattern resolves these issues by allowing notification types to be added or removed dynamically without modifying the `NotificationService` logic.
```java
import java.util.ArrayList;
import java.util.List;

// Observer Interface
interface Observer {
    void update(String message);
}

// Concrete Observers
class EmailSubscriber implements Observer {
    private String name;

    EmailSubscriber(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received email: " + message);
    }
}

class SmsSubscriber implements Observer {
    private String name;

    SmsSubscriber(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received SMS: " + message);
    }
}

// Subject
class NotificationService {
    private List<Observer> observers = new ArrayList<>();

    void addObserver(Observer observer) {
        observers.add(observer);
    }

    void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

// Client
public class ObserverExample {
    public static void main(String[] args) {
        NotificationService service = new NotificationService();

        Observer emailSubscriber = new EmailSubscriber("Alice");
        Observer smsSubscriber = new SmsSubscriber("Bob");

        service.addObserver(emailSubscriber);
        service.addObserver(smsSubscriber);

        System.out.println("Sending notification 1:");
        service.notifyObservers("Your package has shipped!");

        service.removeObserver(emailSubscriber);

        System.out.println("\nSending notification 2:");
        service.notifyObservers("Your package is out for delivery!");
    }
}
```
**Explanation**:
- The `Observer` interface defines an `update` method that observers must implement.
- `EmailSubscriber` and `SmsSubscriber` are concrete observers that act upon receiving notifications.
- The `NotificationService` (subject) maintains a list of observers and notifies them when an event occurs.

---

### Practice Question: Weather Station

**Scenario**:  
You are developing a Weather Station application that broadcasts weather updates (temperature and humidity) to multiple display devices. These devices include a Phone Display, a TV Display, and a Web Dashboard. Whenever the weather data changes, all registered devices should automatically receive the updates without having to query the Weather Station manually.  

**Task**:  
1. Design a solution using the Observer Design Pattern.  
2. Implement the following components:  
   - A `WeatherStation` class that acts as the subject, maintaining a list of registered observers and notifying them whenever weather data is updated.  
   - Observer classes (`PhoneDisplay`, `TvDisplay`, and `WebDashboard`) that receive updates and display the latest weather information.  
3. Demonstrate the following in your solution:  
   - Adding observers to the `WeatherStation`.  
   - Updating weather data and notifying all registered observers.  
   - Removing an observer and showing how updates are sent only to the remaining observers.  

Use clean and structured code to solve the problem.


#### **Solution:**
```java
import java.util.ArrayList;
import java.util.List;

// Observer Interface
interface Observer {
    void update(String weather);
}

// Concrete Observers
class PhoneDisplay implements Observer {
    String name;

    public PhoneDisplay(String name) {
        this.name = name;
    }

    @Override
    public void update(String weather) {
        System.out.println("Phone: " + this.name + ", weather is: " + weather);
    }
}

class TvDisplay implements Observer {
    String name;

    public TvDisplay(String name) {
        this.name = name;
    }

    @Override
    public void update(String weather) {
        System.out.println("TV: " + this.name + ", weather is: " + weather);
    }
}

class WebDashboard implements Observer {
    String name;

    public WebDashboard(String name) {
        this.name = name;
    }

    @Override
    public void update(String weather) {
        System.out.println("WebDashboard: " + this.name + ", weather is: " + weather);
    }
}

// Subject
class WeatherStation {
    private List<Observer> observers = new ArrayList<>();
    private String weather;

    void addObserver(Observer observer) {
        this.observers.add(observer);
    }

    void removeObserver(Observer observer) {
        this.observers.remove(observer);
    }

    void setWhether(String weather) {
        this.weather = weather;
        for (Observer observer : observers) {
            observer.update(weather);
        }
    }
}

// Client
public class ObserverPractice {

    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();

        // Create observers
        Observer phoneObserver = new PhoneDisplay("Samsung");
        Observer tvObserver = new TvDisplay("LG");
        Observer webObserver = new WebDashboard("Google");

        // Register observers
        weatherStation.addObserver(phoneObserver);
        weatherStation.addObserver(tvObserver);
        weatherStation.addObserver(webObserver);

        // Update the weather
        weatherStation.setWhether("Sunny");
        
        // Unregister observer
        weatherStation.removeObserver(tvObserver);
        weatherStation.setWhether("Rainy");
    }
}
```
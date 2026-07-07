1. What is CI/CD?

CI/CD means Continuous Integration and Continuous Delivery/Deployment.

Think of it like this:

Developer writes code → code gets checked/tested automatically → app gets built → app gets deployed.

CI = Continuous Integration

CI means developers regularly push code to a shared repository like GitHub/Bitbucket/GitLab.

Every time code is pushed, the system automatically:

pulls the latest code
compiles/builds the project
runs unit tests
checks code quality
reports if something breaks

Example:

Developer pushes Java code to Git
↓
CI pipeline runs
↓
Maven builds the project
↓
JUnit tests run
↓
SonarQube checks quality
↓
Pass or fail result

Interview answer:

CI/CD is the process of automating build, test, and deployment. CI focuses on integrating code changes frequently and testing them automatically. CD focuses on delivering or deploying the application to environments like UAT, staging, or production.

2. What is Jenkins? What does it do?

Jenkins is an automation tool used for CI/CD.

It helps automate repeated development tasks.

For a Java/Spring Boot project, Jenkins can:

pull code from Git
run Maven/Gradle build
run unit tests
run code quality checks
create a .jar file
deploy the application to a server/container
send success/failure notification

Example Jenkins pipeline:

Git Push
↓
Jenkins starts
↓
mvn clean install
↓
run tests
↓
build jar
↓
deploy to UAT

Simple interview answer:

Jenkins is a CI/CD automation server. It is used to automatically build, test, and deploy applications whenever developers push code. It reduces manual work and helps teams catch errors early.

Similar applications to Jenkins

Common alternatives:

GitLab CI/CD
GitHub Actions
Bitbucket Pipelines
Azure DevOps
TeamCity
Bamboo
CircleCI
Travis CI

For your interview, say:

Jenkins is one of the most common CI/CD tools, but similar tools include GitHub Actions, GitLab CI, Azure DevOps, TeamCity, and Bamboo.

3. When do we use finally in Exception Handling?

finally is used when you want code to run no matter what happens.

It runs whether:

try succeeds
try throws exception
catch handles exception
Example:
try {
    int result = 10 / 0;
    System.out.println(result);
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
} finally {
    System.out.println("This always runs");
}

Output:

Cannot divide by zero
This always runs
Why use finally?

Usually for cleanup:

close file
close database connection
close scanner
release resources
log final message

Example:

Scanner scanner = null;

try {
    scanner = new Scanner(System.in);
    int number = scanner.nextInt();
    System.out.println(number);
} catch (Exception e) {
    System.out.println("Invalid input");
} finally {
    if (scanner != null) {
        scanner.close();
    }
}

Interview answer:

We use finally to execute important cleanup code that must run whether an exception happens or not. Common examples are closing files, database connections, network connections, or releasing resources.

Important modern Java note:

Nowadays, for closing resources, we often use try-with-resources:

try (Scanner scanner = new Scanner(System.in)) {
    int number = scanner.nextInt();
    System.out.println(number);
} catch (Exception e) {
    System.out.println("Invalid input");
}

This automatically closes the scanner.

4. SOLID Principles

SOLID is 5 object-oriented design principles.

They help you write code that is:

cleaner
easier to maintain
easier to test
less tightly coupled
S — Single Responsibility Principle

A class should have one main responsibility.

Bad:

class Report {
    void generateReport() {}
    void saveToDatabase() {}
    void sendEmail() {}
}

This class does too much.

Better:

class ReportGenerator {
    void generateReport() {}
}

class ReportRepository {
    void saveToDatabase() {}
}

class EmailService {
    void sendEmail() {}
}

Interview answer:

Single Responsibility Principle means a class should have only one reason to change. Each class should focus on one responsibility.

O — Open/Closed Principle

Code should be open for extension but closed for modification.

Meaning: you should be able to add new behavior without changing old tested code too much.

Bad:

class PaymentService {
    void pay(String type) {
        if (type.equals("card")) {
            System.out.println("Pay by card");
        } else if (type.equals("paypal")) {
            System.out.println("Pay by PayPal");
        }
    }
}

Every new payment type requires changing this class.

Better:

interface PaymentMethod {
    void pay();
}

class CardPayment implements PaymentMethod {
    public void pay() {
        System.out.println("Pay by card");
    }
}

class PaypalPayment implements PaymentMethod {
    public void pay() {
        System.out.println("Pay by PayPal");
    }
}

Now you can add:

class CryptoPayment implements PaymentMethod {
    public void pay() {
        System.out.println("Pay by crypto");
    }
}

without changing old classes.

Interview answer:

Open/Closed Principle means classes should be open for extension but closed for modification. We can add new functionality using inheritance, interfaces, or polymorphism instead of editing existing code.

L — Liskov Substitution Principle

A child class should be usable wherever the parent class is expected.

Simple meaning:

If Dog extends Animal, then using a Dog as an Animal should not break the program.

Bad example:

class Bird {
    void fly() {
        System.out.println("Flying");
    }
}

class Penguin extends Bird {
    void fly() {
        throw new UnsupportedOperationException("Penguins cannot fly");
    }
}

Problem: not all birds can fly.

Better:

interface Flyable {
    void fly();
}

class Sparrow implements Flyable {
    public void fly() {
        System.out.println("Flying");
    }
}

class Penguin {
    void swim() {
        System.out.println("Swimming");
    }
}

Interview answer:

Liskov Substitution Principle means a subclass should be able to replace its parent class without causing incorrect behavior.

I — Interface Segregation Principle

Do not force a class to implement methods it does not need.

Bad:

interface Worker {
    void work();
    void eat();
}

class Robot implements Worker {
    public void work() {}

    public void eat() {
        // Robot does not eat
    }
}

Better:

interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Human implements Workable, Eatable {
    public void work() {}
    public void eat() {}
}

class Robot implements Workable {
    public void work() {}
}

Interview answer:

Interface Segregation Principle means it is better to have smaller, specific interfaces instead of one large interface that forces classes to implement unnecessary methods.

D — Dependency Inversion Principle

Depend on abstractions, not concrete classes.

Bad:

class OrderService {
    private EmailService emailService = new EmailService();
}

OrderService is tightly coupled to EmailService.

Better:

interface NotificationService {
    void send();
}

class EmailService implements NotificationService {
    public void send() {
        System.out.println("Sending email");
    }
}

class OrderService {
    private NotificationService notificationService;

    public OrderService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }
}

Now OrderService can use email, SMS, Slack, etc.

Interview answer:

Dependency Inversion Principle means high-level classes should not depend directly on low-level classes. They should depend on interfaces or abstractions. This makes code easier to test and change.

Easy memory for SOLID
S = One class, one job
O = Add new features without changing old code
L = Child class should not break parent behavior
I = Small specific interfaces
D = Depend on interface, not concrete class
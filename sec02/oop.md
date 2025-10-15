# 🎯 Object-Oriented Programming & SOLID Principles in Dart

## 📚 Table of Contents
1. [What is Object-Oriented Programming?](#what-is-object-oriented-programming)
2. [Four Pillars of OOP](#four-pillars-of-oop)
3. [Classes & Objects](#classes--objects)
4. [Inheritance](#inheritance)
5. [Polymorphism](#polymorphism)
6. [Abstraction](#abstraction)
7. [Encapsulation](#encapsulation)
8. [SOLID Principles](#solid-principles)
9. [Advanced OOP Concepts](#advanced-oop-concepts)

## 🤔 What is Object-Oriented Programming?

Object-Oriented Programming (OOP) is a programming paradigm that organizes software design around **objects** rather than functions and logic. An object contains data (attributes) and behavior (methods).

### Key Benefits:
- **Modularity**: Code organized into reusable components
- **Maintainability**: Easier to update and modify
- **Reusability**: Objects can be reused across programs
- **Scalability**: Easier to manage complex systems

## 🏛️ Four Pillars of OOP

```dart
void main() {
  print("=== FOUR PILLARS OF OOP ===");
  
  // Encapsulation
  var bankAccount = BankAccount("123456", 1000.0);
  bankAccount.deposit(500.0);
  print("Balance: \$${bankAccount.getBalance()}");
  
  // Inheritance
  var dog = Dog("Buddy", 3);
  dog.speak();
  dog.fetch();
  
  // Polymorphism
  Animal myPet = Cat("Whiskers", 2);
  myPet.speak(); // Runtime polymorphism
  
  // Abstraction
  var circle = Circle(5.0);
  print("Circle Area: ${circle.calculateArea()}");
  print("Circle Perimeter: ${circle.calculatePerimeter()}");
}
```

## 🏗️ Classes & Objects

### Basic Class Structure
```dart
// 🎯 Basic Class Definition
class Student {
  // 🔹 Instance Variables (Properties)
  String name;
  int age;
  double gpa;
  
  // 🔹 Constructor
  Student(this.name, this.age, this.gpa);
  
  // 🔹 Named Constructor
  Student.fromMap(Map<String, dynamic> map)
      : name = map['name'],
        age = map['age'],
        gpa = map['gpa'];
  
  // 🔹 Methods
  void displayInfo() {
    print('Student: $name, Age: $age, GPA: $gpa');
  }
  
  bool isHonorStudent() {
    return gpa >= 3.5;
  }
  
  // 🔹 Getters
  String get status => isHonorStudent() ? "Honor Student" : "Regular Student";
  
  // 🔹 Setters
  set updateGPA(double newGpa) {
    if (newGpa >= 0.0 && newGpa <= 4.0) {
      gpa = newGpa;
    } else {
      throw ArgumentError("GPA must be between 0.0 and 4.0");
    }
  }
}

void classExamples() {
  // Creating objects
  var student1 = Student("Ahmed", 20, 3.8);
  var student2 = Student.fromMap({
    'name': 'Fatima',
    'age': 22,
    'gpa': 3.9
  });
  
  student1.displayInfo();
  student2.displayInfo();
  
  print("${student1.name} is ${student1.status}");
  student1.updateGPA = 3.9;
  print("Updated GPA: ${student1.gpa}");
}
```

### Constructors in Depth
```dart
class Car {
  String brand;
  String model;
  int year;
  double price;
  
  // 🔹 Default Constructor
  Car(this.brand, this.model, this.year, this.price);
  
  // 🔹 Named Constructor
  Car.luxury(String brand, String model, int year)
      : this(brand, model, year, 100000.0);
  
  // 🔹 Factory Constructor
  factory Car.fromJson(Map<String, dynamic> json) {
    return Car(
      json['brand'],
      json['model'],
      json['year'],
      json['price'],
    );
  }
  
  // 🔹 Redirecting Constructor
  Car.oldCar(String brand, String model) : this(brand, model, 2000, 5000.0);
  
  // 🔹 Constant Constructor
  const Car.constant(this.brand, this.model, this.year, this.price);
  
  void displayInfo() {
    print('$year $brand $model - \$$price');
  }
}

void constructorExamples() {
  var car1 = Car("Toyota", "Camry", 2023, 30000.0);
  var car2 = Car.luxury("Mercedes", "S-Class", 2023);
  var car3 = Car.fromJson({
    'brand': 'BMW',
    'model': 'X5',
    'year': 2023,
    'price': 65000.0
  });
  
  car1.displayInfo();
  car2.displayInfo();
  car3.displayInfo();
}
```

## 📈 Inheritance

### Basic Inheritance
```dart
// 🎯 Base Class (Parent)
class Animal {
  String name;
  int age;
  
  Animal(this.name, this.age);
  
  void speak() {
    print("$name makes a sound");
  }
  
  void sleep() {
    print("$name is sleeping");
  }
  
  // 🎯 Virtual method - can be overridden
  void eat() {
    print("$name is eating");
  }
}

// 🎯 Derived Class (Child)
class Dog extends Animal {
  String breed;
  
  Dog(String name, int age, this.breed) : super(name, age);
  
  // 🎯 Method Overriding
  @override
  void speak() {
    print("$name the $breed barks!");
  }
  
  // 🎯 Additional method
  void fetch() {
    print("$name is fetching the ball");
  }
  
  @override
  void eat() {
    print("$name is eating dog food");
  }
}

class Cat extends Animal {
  Cat(String name, int age) : super(name, age);
  
  @override
  void speak() {
    print("$name meows!");
  }
  
  void climb() {
    print("$name is climbing a tree");
  }
}

void inheritanceExamples() {
  var dog = Dog("Buddy", 3, "Golden Retriever");
  var cat = Cat("Whiskers", 2);
  
  dog.speak();    // Overridden method
  dog.sleep();    // Inherited method
  dog.fetch();    // Child class method
  dog.eat();      // Overridden method
  
  cat.speak();    // Overridden method
  cat.climb();    // Child class method
}
```

### Multi-level Inheritance
```dart
class Person {
  String name;
  int age;
  
  Person(this.name, this.age);
  
  void introduce() {
    print("Hello, I'm $name, $age years old");
  }
}

class Student extends Person {
  String studentId;
  double gpa;
  
  Student(String name, int age, this.studentId, this.gpa) : super(name, age);
  
  void study() {
    print("$name is studying");
  }
  
  @override
  void introduce() {
    print("I'm $name, a student with GPA: $gpa");
  }
}

class GraduateStudent extends Student {
  String researchTopic;
  
  GraduateStudent(String name, int age, String studentId, double gpa, this.researchTopic)
      : super(name, age, studentId, gpa);
  
  void conductResearch() {
    print("$name is conducting research on: $researchTopic");
  }
  
  @override
  void introduce() {
    print("I'm $name, a graduate student researching: $researchTopic");
  }
}

void multiLevelInheritance() {
  var gradStudent = GraduateStudent(
    "Dr. Smith", 28, "GS123", 3.9, "Artificial Intelligence"
  );
  
  gradStudent.introduce();        // GraduateStudent version
  gradStudent.study();            // Student method
  gradStudent.conductResearch();  // GraduateStudent method
}
```

## 🔄 Polymorphism

### Runtime Polymorphism
```dart
abstract class Shape {
  double calculateArea();
  double calculatePerimeter();
  
  void describe() {
    print("This is a shape with area: ${calculateArea()}");
  }
}

class Circle extends Shape {
  double radius;
  
  Circle(this.radius);
  
  @override
  double calculateArea() => 3.14159 * radius * radius;
  
  @override
  double calculatePerimeter() => 2 * 3.14159 * radius;
  
  @override
  void describe() {
    print("Circle with radius $radius - Area: ${calculateArea()}");
  }
}

class Rectangle extends Shape {
  double width;
  double height;
  
  Rectangle(this.width, this.height);
  
  @override
  double calculateArea() => width * height;
  
  @override
  double calculatePerimeter() => 2 * (width + height);
  
  @override
  void describe() {
    print("Rectangle ${width}x$height - Area: ${calculateArea()}");
  }
}

class Triangle extends Shape {
  double base;
  double height;
  
  Triangle(this.base, this.height);
  
  @override
  double calculateArea() => 0.5 * base * height;
  
  @override
  double calculatePerimeter() => base * 3; // Simplified for equilateral
  
  @override
  void describe() {
    print("Triangle base:$base height:$height - Area: ${calculateArea()}");
  }
}

void polymorphismExamples() {
  // 🎯 Polymorphism in action
  List<Shape> shapes = [
    Circle(5.0),
    Rectangle(4.0, 6.0),
    Triangle(3.0, 4.0)
  ];
  
  for (var shape in shapes) {
    shape.describe(); // Different behavior for each shape
    print("Perimeter: ${shape.calculatePerimeter()}\n");
  }
  
  // 🎯 Type checking and casting
  for (var shape in shapes) {
    if (shape is Circle) {
      print("This is a circle with radius: ${shape.radius}");
    } else if (shape is Rectangle) {
      print("This is a rectangle: ${shape.width}x${shape.height}");
    } else if (shape is Triangle) {
      print("This is a triangle with base: ${shape.base}");
    }
  }
}
```

## 🔒 Encapsulation

### Private Members and Getters/Setters
```dart
class BankAccount {
  // 🔹 Private members (start with underscore)
  String _accountNumber;
  double _balance;
  String _accountHolder;
  
  // 🔹 Public getter for private field
  String get accountNumber => _accountNumber;
  
  // 🔹 Public getter with computed value
  double get balance => _balance;
  String get accountHolder => _accountHolder;
  
  // 🔹 Private setter
  set _setBalance(double newBalance) {
    if (newBalance >= 0) {
      _balance = newBalance;
    } else {
      throw ArgumentError("Balance cannot be negative");
    }
  }
  
  BankAccount(this._accountNumber, this._balance, this._accountHolder);
  
  // 🔹 Public methods to control access
  void deposit(double amount) {
    if (amount > 0) {
      _setBalance = _balance + amount;
      print("Deposited: \$$amount. New balance: \$$_balance");
    } else {
      throw ArgumentError("Deposit amount must be positive");
    }
  }
  
  void withdraw(double amount) {
    if (amount > 0 && amount <= _balance) {
      _setBalance = _balance - amount;
      print("Withdrawn: \$$amount. New balance: \$$_balance");
    } else {
      throw ArgumentError("Invalid withdrawal amount");
    }
  }
  
  // 🔹 Private method
  void _logTransaction(String type, double amount) {
    print("LOG: $type of \$$amount for account $_accountNumber");
  }
  
  void transfer(BankAccount recipient, double amount) {
    if (amount <= _balance) {
      this.withdraw(amount);
      recipient.deposit(amount);
      _logTransaction("TRANSFER", amount);
    }
  }
}

void encapsulationExamples() {
  var account1 = BankAccount("123456", 1000.0, "Ahmed Mohamed");
  var account2 = BankAccount("789012", 500.0, "Fatima Ali");
  
  // Can access via public methods only
  account1.deposit(500.0);
  account1.withdraw(200.0);
  
  print("Account holder: ${account1.accountHolder}");
  print("Balance: \$${account1.balance}");
  
  // Transfer between accounts
  account1.transfer(account2, 300.0);
  
  // This would cause error - private field
  // account1._balance = 1000000; // Compilation error
}
```

## 🎭 Abstraction

### Abstract Classes and Interfaces
```dart
// 🎯 Abstract Class - cannot be instantiated
abstract class Vehicle {
  String make;
  String model;
  int year;
  
  Vehicle(this.make, this.model, this.year);
  
  // 🎯 Abstract method - must be implemented by subclasses
  void start();
  void stop();
  
  // 🎯 Concrete method in abstract class
  void displayInfo() {
    print('$year $make $model');
  }
  
  // 🎯 Can have implemented methods in abstract class
  void honk() {
    print("Beep beep!");
  }
}

// 🎯 Interface (Dart uses abstract classes as interfaces)
abstract class ElectricVehicle {
  void charge();
  int getBatteryLevel();
}

// 🎯 Implementing both abstract class and interface
class ElectricCar extends Vehicle implements ElectricVehicle {
  double batteryCapacity;
  double currentCharge;
  
  ElectricCar(String make, String model, int year, this.batteryCapacity)
      : super(make, model, year) {
    currentCharge = 100.0; // Start fully charged
  }
  
  @override
  void start() {
    if (currentCharge > 0) {
      print("$make $model started silently");
      currentCharge -= 5.0;
    } else {
      print("Battery too low to start");
    }
  }
  
  @override
  void stop() {
    print("$make $model stopped");
  }
  
  @override
  void charge() {
    currentCharge = 100.0;
    print("$make $model fully charged");
  }
  
  @override
  int getBatteryLevel() {
    return currentCharge.round();
  }
  
  @override
  void displayInfo() {
    super.displayInfo();
    print("Battery: $batteryCapacity kWh, Charge: ${getBatteryLevel()}%");
  }
}

class Motorcycle extends Vehicle {
  Motorcycle(String make, String model, int year) : super(make, model, year);
  
  @override
  void start() {
    print("$make $model motorcycle roaring to life");
  }
  
  @override
  void stop() {
    print("$make $model motorcycle engine off");
  }
  
  void wheelie() {
    print("$make $model doing a wheelie!");
  }
}

void abstractionExamples() {
  // Vehicle vehicle = Vehicle(); // Error - cannot instantiate abstract class
  
  var tesla = ElectricCar("Tesla", "Model S", 2023, 100.0);
  var harley = Motorcycle("Harley Davidson", "Sportster", 2023);
  
  tesla.displayInfo();
  tesla.start();
  tesla.charge();
  print("Battery level: ${tesla.getBatteryLevel()}%");
  
  harley.displayInfo();
  harley.start();
  harley.wheelie();
}
```

## ⚡ SOLID Principles

### 1. Single Responsibility Principle (SRP)
```dart
// ❌ Violates SRP - Too many responsibilities
class BadUser {
  String name;
  String email;
  
  BadUser(this.name, this.email);
  
  void saveToDatabase() {
    print("Saving $name to database...");
    // Database logic
  }
  
  void sendEmail(String message) {
    print("Sending email to $email: $message");
    // Email logic
  }
  
  void validateEmail() {
    // Validation logic
  }
  
  void generateReport() {
    // Report generation logic
  }
}

// ✅ Follows SRP - Each class has one responsibility
class User {
  String name;
  String email;
  
  User(this.name, this.email);
}

class UserRepository {
  void saveUser(User user) {
    print("Saving ${user.name} to database...");
    // Only database operations
  }
  
  User getUser(String email) {
    // Database retrieval logic
    return User("Retrieved User", email);
  }
}

class EmailService {
  void sendEmail(User user, String message) {
    print("Sending email to ${user.email}: $message");
    // Only email operations
  }
}

class UserValidator {
  bool validateEmail(String email) {
    return email.contains('@') && email.contains('.');
  }
  
  bool validateUser(User user) {
    return user.name.isNotEmpty && validateEmail(user.email);
  }
}

void srpExample() {
  var user = User("Ahmed", "ahmed@bfcai.edu.eg");
  var validator = UserValidator();
  var repository = UserRepository();
  var emailService = EmailService();
  
  if (validator.validateUser(user)) {
    repository.saveUser(user);
    emailService.sendEmail(user, "Welcome to our platform!");
  }
}
```

### 2. Open/Closed Principle (OCP)
```dart
// ❌ Violates OCP - Need to modify existing code for new types
class BadAreaCalculator {
  double calculateArea(dynamic shape) {
    if (shape is Rectangle) {
      return shape.width * shape.height;
    } else if (shape is Circle) {
      return 3.14159 * shape.radius * shape.radius;
    }
    // Need to modify this method for every new shape
    return 0.0;
  }
}

// ✅ Follows OCP - Open for extension, closed for modification
abstract class Shape {
  double calculateArea();
}

class Rectangle extends Shape {
  double width;
  double height;
  
  Rectangle(this.width, this.height);
  
  @override
  double calculateArea() => width * height;
}

class Circle extends Shape {
  double radius;
  
  Circle(this.radius);
  
  @override
  double calculateArea() => 3.14159 * radius * radius;
}

class Triangle extends Shape {
  double base;
  double height;
  
  Triangle(this.base, this.height);
  
  @override
  double calculateArea() => 0.5 * base * height;
}

// ✅ Can add new shapes without modifying AreaCalculator
class AreaCalculator {
  double calculateTotalArea(List<Shape> shapes) {
    double totalArea = 0.0;
    for (var shape in shapes) {
      totalArea += shape.calculateArea();
    }
    return totalArea;
  }
}

void ocpExample() {
  var shapes = [
    Rectangle(4, 5),
    Circle(3),
    Triangle(6, 4)
  ];
  
  var calculator = AreaCalculator();
  var totalArea = calculator.calculateTotalArea(shapes);
  print("Total area: $totalArea");
}
```

### 3. Liskov Substitution Principle (LSP)
```dart
// ❌ Violates LSP - Square is not a proper substitute for Rectangle
class Rectangle {
  double width;
  double height;
  
  Rectangle(this.width, this.height);
  
  double get area => width * height;
  
  void setDimensions(double width, double height) {
    this.width = width;
    this.height = height;
  }
}

class BadSquare extends Rectangle {
  BadSquare(double side) : super(side, side);
  
  @override
  void setDimensions(double width, double height) {
    super.setDimensions(width, width); // Violates rectangle behavior
  }
}

// ✅ Follows LSP - Proper inheritance hierarchy
abstract class Shape {
  double get area;
}

class GoodRectangle implements Shape {
  double width;
  double height;
  
  GoodRectangle(this.width, this.height);
  
  @override
  double get area => width * height;
}

class GoodSquare implements Shape {
  double side;
  
  GoodSquare(this.side);
  
  @override
  double get area => side * side;
}

void lspExample() {
  // ✅ Both can be used interchangeably as Shapes
  List<Shape> shapes = [
    GoodRectangle(4, 5),
    GoodSquare(4)
  ];
  
  for (var shape in shapes) {
    print("Area: ${shape.area}");
  }
}
```

### 4. Interface Segregation Principle (ISP)
```dart
// ❌ Violates ISP - Large interface forcing implementations
abstract class BadWorker {
  void work();
  void eat();
  void sleep();
  void code();
  void design();
  void test();
}

class BadDeveloper implements BadWorker {
  @override void work() => print("Working");
  @override void eat() => print("Eating");
  @override void sleep() => print("Sleeping");
  @override void code() => print("Coding");      // Relevant
  @override void design() => print("Designing"); // Not really developer's job
  @override void test() => print("Testing");     // Sometimes, but not always
}

// ✅ Follows ISP - Segregated interfaces
abstract class Worker {
  void work();
  void takeBreak();
}

abstract class Coder {
  void code();
  void debug();
}

abstract class Designer {
  void design();
  void createPrototype();
}

abstract class Tester {
  void test();
  void writeTestCases();
}

// ✅ Implement only relevant interfaces
class Developer implements Worker, Coder {
  @override
  void work() => print("Developer working");
  
  @override
  void takeBreak() => print("Developer taking break");
  
  @override
  void code() => print("Developer coding");
  
  @override
  void debug() => print("Developer debugging");
}

class UXDesigner implements Worker, Designer {
  @override
  void work() => print("Designer working");
  
  @override
  void takeBreak() => print("Designer taking break");
  
  @override
  void design() => print("Designer designing");
  
  @override
  void createPrototype() => print("Designer creating prototype");
}

void ispExample() {
  var developer = Developer();
  var designer = UXDesigner();
  
  developer.work();
  developer.code();
  
  designer.work();
  designer.design();
}
```

### 5. Dependency Inversion Principle (DIP)
```dart
// ❌ Violates DIP - High-level module depends on low-level module
class BadMySQLDatabase {
  void connect() => print("Connecting to MySQL");
  void query(String sql) => print("Executing: $sql");
}

class BadUserService {
  BadMySQLDatabase _database;
  
  BadUserService() : _database = BadMySQLDatabase();
  
  void getUser(int id) {
    _database.connect();
    _database.query("SELECT * FROM users WHERE id = $id");
  }
}

// ✅ Follows DIP - Both depend on abstractions
abstract class Database {
  void connect();
  void query(String sql);
}

class MySQLDatabase implements Database {
  @override
  void connect() => print("Connecting to MySQL");
  
  @override
  void query(String sql) => print("MySQL executing: $sql");
}

class PostgreSQLDatabase implements Database {
  @override
  void connect() => print("Connecting to PostgreSQL");
  
  @override
  void query(String sql) => print("PostgreSQL executing: $sql");
}

class MongoDB implements Database {
  @override
  void connect() => print("Connecting to MongoDB");
  
  @override
  void query(String sql) => print("MongoDB executing: $sql");
}

// ✅ High-level module depends on abstraction
class UserService {
  Database _database;
  
  UserService(this._database); // Dependency injection
  
  void getUser(int id) {
    _database.connect();
    _database.query("SELECT * FROM users WHERE id = $id");
  }
}

// ✅ Factory for creating database instances
class DatabaseFactory {
  static Database createDatabase(String type) {
    switch (type) {
      case 'mysql':
        return MySQLDatabase();
      case 'postgres':
        return PostgreSQLDatabase();
      case 'mongo':
        return MongoDB();
      default:
        throw ArgumentError("Unknown database type: $type");
    }
  }
}

void dipExample() {
  // ✅ Easy to switch database implementations
  var mysqlService = UserService(DatabaseFactory.createDatabase('mysql'));
  var postgresService = UserService(DatabaseFactory.createDatabase('postgres'));
  var mongoService = UserService(DatabaseFactory.createDatabase('mongo'));
  
  mysqlService.getUser(1);
  postgresService.getUser(1);
  mongoService.getUser(1);
}
```

## 🚀 Advanced OOP Concepts

### Mixins
```dart
// 🎯 Mixins - Reusable code across class hierarchies
mixin Logger {
  void log(String message) {
    print("LOG [${DateTime.now()}]: $message");
  }
}

mixin Serializable {
  String toJson() {
    return "{}"; // Simplified JSON serialization
  }
}

mixin EmailSender {
  void sendEmail(String to, String subject, String body) {
    print("Sending email to $to: $subject");
    print("Body: $body");
  }
}

class User with Logger, Serializable {
  String name;
  String email;
  
  User(this.name, this.email);
  
  void register() {
    log("User $name registered with email $email");
  }
}

class Admin with Logger, Serializable, EmailSender {
  String name;
  
  Admin(this.name);
  
  void manageUsers() {
    log("Admin $name managing users");
    sendEmail("team@company.com", "Admin Report", "Monthly admin report");
  }
}

void mixinExamples() {
  var user = User("Ahmed", "ahmed@bfcai.edu.eg");
  user.register();
  print("User JSON: ${user.toJson()}");
  
  var admin = Admin("System Admin");
  admin.manageUsers();
}
```

### Generics
```dart
// 🎯 Generic Classes
class Repository<T> {
  List<T> _items = [];
  
  void add(T item) {
    _items.add(item);
  }
  
  T get(int index) => _items[index];
  
  List<T> getAll() => List<T>.from(_items);
  
  void remove(T item) {
    _items.remove(item);
  }
}

// 🎯 Generic Methods
T findFirst<T>(List<T> items, bool Function(T) test) {
  for (var item in items) {
    if (test(item)) {
      return item;
    }
  }
  throw Exception("Item not found");
}

// 🎯 Generic Constraints
abstract class Identifiable {
  String get id;
}

class UserRepository<T extends Identifiable> {
  Map<String, T> _items = {};
  
  void add(T item) {
    _items[item.id] = item;
  }
  
  T? get(String id) => _items[id];
}

class Product implements Identifiable {
  @override
  final String id;
  final String name;
  final double price;
  
  Product(this.id, this.name, this.price);
}

void genericExamples() {
  // Generic class usage
  var userRepo = Repository<String>();
  userRepo.add("Ahmed");
  userRepo.add("Fatima");
  print("All users: ${userRepo.getAll()}");
  
  var productRepo = Repository<Map<String, dynamic>>();
  productRepo.add({"id": "1", "name": "Laptop", "price": 999.99});
  
  // Generic method usage
  var numbers = [1, 2, 3, 4, 5];
  var firstEven = findFirst(numbers, (n) => n % 2 == 0);
  print("First even number: $firstEven");
  
  // Generic constraints
  var identifiedRepo = UserRepository<Product>();
  var laptop = Product("123", "Laptop", 999.99);
  identifiedRepo.add(laptop);
  print("Retrieved product: ${identifiedRepo.get("123")?.name}");
}
```

## 🎯 Complete OOP System Example

```dart
// 🎯 Complete E-commerce System demonstrating OOP & SOLID
abstract class PaymentMethod {
  void processPayment(double amount);
  bool validate();
}

class CreditCard implements PaymentMethod {
  String cardNumber;
  String expiryDate;
  String cvv;
  
  CreditCard(this.cardNumber, this.expiryDate, this.cvv);
  
  @override
  void processPayment(double amount) {
    if (validate()) {
      print("Processing credit card payment of \$$amount");
      // Actual payment processing logic
    } else {
      throw Exception("Invalid credit card details");
    }
  }
  
  @override
  bool validate() {
    return cardNumber.length == 16 && 
           cvv.length == 3 && 
           expiryDate.isNotEmpty;
  }
}

class PayPal implements PaymentMethod {
  String email;
  
  PayPal(this.email);
  
  @override
  void processPayment(double amount) {
    if (validate()) {
      print("Processing PayPal payment of \$$amount for $email");
    } else {
      throw Exception("Invalid PayPal email");
    }
  }
  
  @override
  bool validate() {
    return email.contains('@') && email.contains('.');
  }
}

abstract class Product {
  String get id;
  String get name;
  double get price;
  String get description;
}

class PhysicalProduct implements Product {
  @override
  final String id;
  @override
  final String name;
  @override
  final double price;
  @override
  final String description;
  final double weight;
  final String dimensions;
  
  PhysicalProduct({
    required this.id,
    required this.name,
    required this.price,
    required this.description,
    required this.weight,
    required this.dimensions,
  });
}

class DigitalProduct implements Product {
  @override
  final String id;
  @override
  final String name;
  @override
  final double price;
  @override
  final String description;
  final String downloadUrl;
  final double fileSize;
  
  DigitalProduct({
    required this.id,
    required this.name,
    required this.price,
    required this.description,
    required this.downloadUrl,
    required this.fileSize,
  });
}

class Order {
  final String id;
  final List<Product> products;
  final PaymentMethod paymentMethod;
  final DateTime orderDate;
  
  Order({
    required this.id,
    required this.products,
    required this.paymentMethod,
  }) : orderDate = DateTime.now();
  
  double get totalAmount {
    return products.fold(0.0, (sum, product) => sum + product.price);
  }
  
  void processOrder() {
    try {
      if (paymentMethod.validate()) {
        paymentMethod.processPayment(totalAmount);
        print("Order $id processed successfully!");
        print("Total: \$$totalAmount");
        print("Products: ${products.map((p) => p.name).toList()}");
      }
    } catch (e) {
      print("Failed to process order: $e");
    }
  }
}

class OrderProcessor {
  void processOrders(List<Order> orders) {
    for (var order in orders) {
      print("\n--- Processing Order ${order.id} ---");
      order.processOrder();
    }
  }
}

void completeOopExample() {
  print("=== E-COMMERCE OOP SYSTEM ===\n");
  
  // Create products
  var products = [
    PhysicalProduct(
      id: "1",
      name: "Smartphone",
      price: 699.99,
      description: "Latest smartphone",
      weight: 0.2,
      dimensions: "15x7x0.8 cm",
    ),
    DigitalProduct(
      id: "2",
      name: "E-book",
      price: 19.99,
      description: "Programming guide",
      downloadUrl: "https://example.com/ebook",
      fileSize: 2.5,
    ),
  ];
  
  // Create payment methods
  var creditCard = CreditCard("1234567812345678", "12/25", "123");
  var paypal = PayPal("customer@example.com");
  
  // Create orders
  var orders = [
    Order(
      id: "ORD001",
      products: [products[0]], // Physical product
      paymentMethod: creditCard,
    ),
    Order(
      id: "ORD002",
      products: [products[1]], // Digital product
      paymentMethod: paypal,
    ),
    Order(
      id: "ORD003",
      products: products, // Both products
      paymentMethod: creditCard,
    ),
  ];
  
  // Process orders
  var processor = OrderProcessor();
  processor.processOrders(orders);
}

void main() {
  // Run all examples
  classExamples();
  constructorExamples();
  inheritanceExamples();
  polymorphismExamples();
  encapsulationExamples();
  abstractionExamples();
  
  // SOLID Principles
  srpExample();
  ocpExample();
  lspExample();
  ispExample();
  dipExample();
  
  // Advanced Concepts
  mixinExamples();
  genericExamples();
  
  // Complete System
  completeOopExample();
}
```

## 💡 Key Takeaways

### OOP Principles:
1. **Encapsulation**: Hide implementation details, expose only necessary interfaces
2. **Inheritance**: Create hierarchical relationships between classes
3. **Polymorphism**: Same interface, different implementations
4. **Abstraction**: Define contracts without implementation details

### SOLID Principles:
1. **Single Responsibility**: One class, one responsibility
2. **Open/Closed**: Open for extension, closed for modification
3. **Liskov Substitution**: Subtypes must be substitutable for their base types
4. **Interface Segregation**: Many specific interfaces are better than one general interface
5. **Dependency Inversion**: Depend on abstractions, not concretions

### Best Practices:
- Use `final` for immutable properties
- Prefer composition over inheritance when appropriate
- Use mixins for cross-cutting concerns
- Leverage generics for type-safe reusable code
- Follow dependency injection for testable code

This OOP foundation is essential for building robust, maintainable Flutter applications! 🚀

# 🎯 Structured Programming with Dart - Expert Guide

## 📚 Table of Contents
1. [What is Structured Programming?](#what-is-structured-programming)
2. [Variables & Data Types](#variables--data-types)
3. [Control Flow Structures](#control-flow-structures)
4. [Functions & Modularity](#functions--modularity)
5. [Collections](#collections)
6. [Error Handling](#error-handling)
7. [Best Practices](#best-practices)

## 🤔 What is Structured Programming?

Structured programming is a paradigm that emphasizes:
- **Sequential execution** - Code executes line by line
- **Selection** - Making decisions with if/else, switch
- **Iteration** - Repeating tasks with loops
- **Modularity** - Breaking code into functions

Dart perfectly supports these principles with its clean syntax and powerful features.

## 🏷️ Variables & Data Types

### Basic Data Types
```dart
void main() {
  // 🔹 Number Types
  int age = 25;                    // Integer
  double price = 99.99;            // Double precision
  num anyNumber = 42;              // Can be int or double
  
  // 🔹 Text Type
  String name = "BFCAI Student";   // String
  String multiline = '''
  This is a
  multi-line
  string''';
  
  // 🔹 Boolean Type
  bool isActive = true;            // Boolean
  bool isEmpty = false;
  
  // 🔹 Dynamic Type (Use sparingly!)
  dynamic dynamicVar = "I can be anything";
  dynamicVar = 100;                // Now it's an integer
  dynamicVar = true;               // Now it's a boolean
}
```

### Type Inference with `var` and `final`
```dart
void typeInference() {
  // 🎯 var - Type is inferred at compile time
  var message = "Hello Dart";      // Compiler knows it's String
  var count = 42;                  // Compiler knows it's int
  var rating = 4.5;                // Compiler knows it's double
  
  // 🎯 final - Single assignment (runtime constant)
  final university = "BFCAI";      // Cannot be reassigned
  final currentTime = DateTime.now(); // Evaluated at runtime
  
  // 🎯 const - Compile-time constant
  const pi = 3.14159;              // Must be known at compile time
  const maxAttempts = 3;           // Compile-time constant
  
  print('University: $university, PI: $pi');
}
```

### Null Safety in Dart
```dart
void nullSafety() {
  // 🛡️ Non-nullable by default
  String name = "Dart";            // Cannot be null
  // String? nullableName = null;  // This would cause error
  
  // 🛡️ Nullable types (explicitly marked with ?)
  String? nullableString;          // Can be null
  nullableString = null;           // This is allowed
  nullableString = "Now it has value";
  
  // 🛡️ Null-aware operators
  String? possiblyNull;
  
  // Null-aware assignment
  String value = possiblyNull ?? "Default Value";
  
  // Null-aware access
  int? length = possiblyNull?.length;
  
  // Null assertion operator (use carefully!)
  String forcedValue = possiblyNull!; // Throws if null
  
  print('Value: $value, Length: $length');
}
```

## 🎮 Control Flow Structures

### If-Else Statements
```dart
void controlFlow() {
  int score = 85;
  String grade;
  
  // 🔹 Basic if-else
  if (score >= 90) {
    grade = "A";
    print("Excellent!");
  } else if (score >= 80) {
    grade = "B";  // This will execute
    print("Very Good!");
  } else if (score >= 70) {
    grade = "C";
    print("Good");
  } else {
    grade = "F";
    print("Needs Improvement");
  }
  
  print("Your grade: $grade");
  
  // 🔹 Conditional expressions
  String status = score >= 50 ? "Pass" : "Fail";
  String feedback = score >= 80 ? "Excellent" : "Good effort";
  
  print("Status: $status, Feedback: $feedback");
}
```

### Switch Statement
```dart
void switchExample() {
  String day = "Monday";
  String schedule;
  
  switch (day) {
    case "Monday":
      schedule = "Team meeting at 10 AM";
      break;
    case "Tuesday":
      schedule = "Code review session";
      break;
    case "Wednesday":
      schedule = "Project work";
      break;
    case "Thursday":
      schedule = "Client presentation";
      break;
    case "Friday":
      schedule = "Weekly planning";
      break;
    default:
      schedule = "Weekend - No meetings";
  }
  
  print("On $day: $schedule");
  
  // 🔹 Enhanced switch with expressions (Dart 3.0+)
  int number = 2;
  String description = switch (number) {
    1 => "One",
    2 => "Two",    // This will match
    3 => "Three",
    _ => "Unknown",
  };
  
  print("Number $number is: $description");
}
```

### Loops - Iteration Structures
```dart
void loopExamples() {
  print("=== For Loop ===");
  // 🔹 Traditional for loop
  for (int i = 1; i <= 5; i++) {
    print("Count: $i");
  }
  
  print("\n=== For-in Loop ===");
  // 🔹 For-in loop with collections
  List<String> fruits = ['Apple', 'Banana', 'Orange', 'Mango'];
  for (String fruit in fruits) {
    print("Fruit: $fruit");
  }
  
  print("\n=== For-each Loop ===");
  // 🔹 For-each with function
  fruits.forEach((fruit) {
    print("Processing: $fruit");
  });
  
  // 🔹 Shorter for-each
  fruits.forEach(print);
  
  print("\n=== While Loop ===");
  // 🔹 While loop
  int counter = 1;
  while (counter <= 3) {
    print("While counter: $counter");
    counter++;
  }
  
  print("\n=== Do-While Loop ===");
  // 🔹 Do-while loop (executes at least once)
  int attempts = 0;
  do {
    print("Attempt: ${attempts + 1}");
    attempts++;
  } while (attempts < 3);
}
```

## 📦 Functions & Modularity

### Basic Function Structure
```dart
// 🎯 Function definition
int calculateSum(int a, int b) {
  return a + b;
}

// 🎯 Arrow function (for single expression)
double calculateArea(double radius) => 3.14159 * radius * radius;

// 🎯 Function with optional parameters
void printUserInfo(String name, [int? age, String? city]) {
  print("Name: $name");
  if (age != null) print("Age: $age");
  if (city != null) print("City: $city");
}

// 🎯 Function with named parameters
void configureApp({required String title, int width = 800, int height = 600}) {
  print("App: $title, Size: ${width}x$height");
}

// 🎯 Function with default values
String greet(String name, {String greeting = "Hello"}) {
  return "$greeting, $name!";
}

void functionExamples() {
  // Calling functions
  int result = calculateSum(10, 20);
  print("Sum: $result");
  
  double area = calculateArea(5.0);
  print("Area: $area");
  
  printUserInfo("Alice");
  printUserInfo("Bob", 25, "Cairo");
  
  configureApp(title: "My Flutter App", width: 1024);
  
  String message = greet("Sarah", greeting: "Hi");
  print(message);
}
```

### Higher-Order Functions
```dart
void higherOrderFunctions() {
  List<int> numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  
  // 🔹 map - Transform each element
  List<int> squared = numbers.map((number) => number * number).toList();
  print("Squared: $squared");
  
  // 🔹 where - Filter elements
  List<int> evenNumbers = numbers.where((number) => number % 2 == 0).toList();
  print("Even numbers: $evenNumbers");
  
  // 🔹 reduce - Combine elements
  int sum = numbers.reduce((value, element) => value + element);
  print("Sum: $sum");
  
  // 🔹 forEach - Perform action on each element
  print("Numbers:");
  numbers.forEach((number) => print(" - $number"));
  
  // 🔹 Custom higher-order function
  void processNumbers(List<int> numbers, int Function(int) processor) {
    for (int number in numbers) {
      int result = processor(number);
      print("Processed: $result");
    }
  }
  
  print("\nCustom processing:");
  processNumbers(numbers, (n) => n * 2);
}
```

## 🗃️ Collections

### Lists
```dart
void listExamples() {
  // 🔹 List creation
  List<String> students = ['Ahmed', 'Mohamed', 'Fatima'];
  List<int> scores = [85, 92, 78, 96];
  var mixed = [1, 'hello', 3.14, true]; // Not recommended - loses type safety
  
  // 🔹 List operations
  students.add('Aisha');                    // Add element
  students.insert(1, 'Omar');               // Insert at index
  students.remove('Mohamed');               // Remove element
  students.removeAt(0);                     // Remove at index
  
  // 🔹 List properties
  print('Length: ${students.length}');
  print('Is empty: ${students.isEmpty}');
  print('First element: ${students.first}');
  print('Last element: ${students.last}');
  
  // 🔹 List iteration
  for (int i = 0; i < students.length; i++) {
    print('Student ${i + 1}: ${students[i]}');
  }
  
  // 🔹 List methods
  scores.sort();                           // Sort the list
  List<int> reversed = scores.reversed.toList(); // Reverse
  bool hasHighScore = scores.any((score) => score > 90); // Check condition
  List<int> highScores = scores.where((score) => score > 85).toList(); // Filter
  
  print('Sorted scores: $scores');
  print('High scores: $highScores');
}
```

### Maps
```dart
void mapExamples() {
  // 🔹 Map creation
  Map<String, int> studentAges = {
    'Ahmed': 20,
    'Fatima': 22,
    'Omar': 21,
  };
  
  Map<String, dynamic> studentInfo = {
    'name': 'Mohamed',
    'age': 23,
    'gpa': 3.8,
    'isGraduated': false,
  };
  
  // 🔹 Map operations
  studentAges['Aisha'] = 19;              // Add new key-value
  studentAges['Ahmed'] = 21;              // Update value
  studentAges.remove('Omar');             // Remove key
  
  // 🔹 Map access
  print('Fatima\'s age: ${studentAges['Fatima']}');
  print('Contains Ali: ${studentAges.containsKey('Ali')}');
  
  // 🔹 Map iteration
  studentAges.forEach((name, age) {
    print('$name is $age years old');
  });
  
  for (var entry in studentAges.entries) {
    print('${entry.key}: ${entry.value}');
  }
  
  // 🔹 Map transformation
  Map<String, String> ageDescriptions = studentAges.map((name, age) {
    return MapEntry(name, '$name is $age years old');
  });
  
  print('Age descriptions: $ageDescriptions');
}
```

### Sets
```dart
void setExamples() {
  // 🔹 Set creation
  Set<String> uniqueNames = {'Ahmed', 'Fatima', 'Omar', 'Ahmed'}; // Duplicates removed
  Set<int> primeNumbers = {2, 3, 5, 7, 11, 13};
  
  print('Unique names: $uniqueNames'); // Only one 'Ahmed'
  
  // 🔹 Set operations
  uniqueNames.add('Aisha');
  uniqueNames.add('Ahmed');           // Won't add duplicate
  uniqueNames.remove('Omar');
  
  // 🔹 Set operations (union, intersection, difference)
  Set<String> groupA = {'Ahmed', 'Fatima', 'Omar'};
  Set<String> groupB = {'Omar', 'Aisha', 'Mohamed'};
  
  Set<String> union = groupA.union(groupB);
  Set<String> intersection = groupA.intersection(groupB);
  Set<String> difference = groupA.difference(groupB);
  
  print('Union: $union');
  print('Intersection: $intersection');
  print('Difference: $difference');
}
```

## 🚨 Error Handling

### Try-Catch Blocks
```dart
void errorHandling() {
  // 🔹 Basic try-catch
  try {
    double result = 10 / 0; // This will cause division by zero
    print("Result: $result");
  } catch (e) {
    print("Error occurred: $e");
  }
  
  // 🔹 Specific exception handling
  try {
    List<int> numbers = [1, 2, 3];
    print(numbers[5]); // Index out of range
  } on RangeError {
    print("Index out of range!");
  } on FormatException {
    print("Format error!");
  } catch (e) {
    print("Unknown error: $e");
  } finally {
    print("This always executes");
  }
  
  // 🔹 Custom exceptions
  try {
    validateAge(-5);
  } catch (e) {
    print("Validation error: $e");
  }
}

void validateAge(int age) {
  if (age < 0) {
    throw ArgumentError("Age cannot be negative");
  }
  if (age > 150) {
    throw ArgumentError("Age seems unrealistic");
  }
  print("Age $age is valid");
}
```

## 💡 Best Practices

### Code Organization
```dart
// 🎯 Keep functions small and focused
double calculateCircleArea(double radius) => 3.14159 * radius * radius;

double calculateRectangleArea(double width, double height) => width * height;

// 🎯 Use descriptive variable names
void goodNaming() {
  int studentCount = 45;                    // Good
  double averageScore = 85.5;               // Good
  String courseTitle = "Flutter Development"; // Good
  
  // Avoid:
  int sc = 45;                              // Bad
  double avg = 85.5;                        // Bad
  String ct = "Flutter Development";        // Bad
}

// 🎯 Use constants for magic numbers
class AppConstants {
  static const int maxLoginAttempts = 3;
  static const double taxRate = 0.14;
  static const String appName = "BFCAI Learning";
}

void useConstants() {
  if (loginAttempts > AppConstants.maxLoginAttempts) {
    print("Account locked");
  }
}

// 🎯 Proper documentation
/// Calculates the final grade based on scores and weights
/// 
/// [scores] - List of assignment scores (0-100)
/// [weights] - List of corresponding weights (should sum to 1.0)
/// 
/// Returns the final grade as a percentage
/// 
/// Throws [ArgumentError] if lists have different lengths
/// or weights don't sum to 1.0
double calculateFinalGrade(List<double> scores, List<double> weights) {
  if (scores.length != weights.length) {
    throw ArgumentError("Scores and weights must have same length");
  }
  
  double totalWeight = weights.reduce((sum, weight) => sum + weight);
  if (totalWeight.abs() - 1.0 > 0.001) {
    throw ArgumentError("Weights must sum to 1.0");
  }
  
  double finalGrade = 0.0;
  for (int i = 0; i < scores.length; i++) {
    finalGrade += scores[i] * weights[i];
  }
  
  return finalGrade;
}
```

### Complete Structured Programming Example
```dart
void structuredProgrammingDemo() {
  print("=== STUDENT GRADE MANAGEMENT SYSTEM ===\n");
  
  // Data storage using collections
  Map<String, List<double>> studentGrades = {
    'Ahmed': [85.0, 92.0, 78.0],
    'Fatima': [95.0, 88.0, 91.0],
    'Omar': [72.0, 85.0, 79.0],
  };
  
  List<double> assignmentWeights = [0.3, 0.4, 0.3]; // Must sum to 1.0
  
  // Process each student using structured programming principles
  studentGrades.forEach((studentName, grades) {
    print("Processing: $studentName");
    
    // Sequence - step by step execution
    try {
      // Selection - decision making
      if (grades.length != assignmentWeights.length) {
        print("  ⚠️  Grade count mismatch for $studentName");
        return; // Skip this student
      }
      
      // Iteration - processing multiple items
      double total = 0.0;
      for (int i = 0; i < grades.length; i++) {
        total += grades[i];
      }
      double average = total / grades.length;
      
      // Modularity - using functions
      double finalGrade = calculateFinalGrade(grades, assignmentWeights);
      
      // More selection
      String performance;
      if (finalGrade >= 90) {
        performance = "Excellent 🎉";
      } else if (finalGrade >= 80) {
        performance = "Very Good 👍";
      } else if (finalGrade >= 70) {
        performance = "Good 👌";
      } else {
        performance = "Needs Improvement 📚";
      }
      
      // Output results
      print("  Grades: $grades");
      print("  Average: ${average.toStringAsFixed(2)}");
      print("  Final Grade: ${finalGrade.toStringAsFixed(2)}%");
      print("  Performance: $performance\n");
      
    } catch (e) {
      // Error handling
      print("  ❌ Error processing $studentName: $e\n");
    }
  });
  
  print("=== PROCESSING COMPLETE ===");
}

void main() {
  // Run all examples
  typeInference();
  controlFlow();
  switchExample();
  loopExamples();
  functionExamples();
  higherOrderFunctions();
  listExamples();
  mapExamples();
  setExamples();
  errorHandling();
  structuredProgrammingDemo();
}
```

## 🎯 Key Takeaways

1. **Variables & Types**: Use strong typing and leverage type inference
2. **Control Flow**: Master if-else, switch, and loops for program logic
3. **Functions**: Break code into reusable, focused functions
4. **Collections**: Use Lists, Maps, and Sets appropriately for data storage
5. **Error Handling**: Write robust code with proper exception handling
6. **Modularity**: Keep code organized and maintainable

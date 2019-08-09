

# Dart Programing

[Dart Programming Tutorial](https://www.tutorialspoint.com/dart_programming/index.htm)



# Evenironment

Online Editor https://dartpad.dev



Install SDK

```bash
brew tap dart-lang/dart
brew install dart
```

dart2js

```bash
dart2js --out=out.js input.dart
```



# Syntax

Dart program is composed of:

* Variable and operators
* Classes
* Functions
* Expressions and Programming Constructs
* Decision Making and Loop Constructs
* Comments
* Libraries and Packages
* Typedefs
* Data structures represents as Collections and Generics



Comments

```dart
// single line comment
/* multiline 
comments
*/
```



# Data Types

* Numbers, int and double
* Strings
* Booleans
* Lists
* Maps
* Dynamics
* Symbol
* Runes



```dart
void main() {
  double i = num.parse('10.1');
  print(i.isFinite);
  print(i.ceil);
  String t = 'this a boring string';
  print(t.isEmpty);
  print(t.toUpperCase());
  bool b = 3 > 2;
  if (b) {
    print('3 > 2');
  }
  var list1 = List(3);
  var list2 = List();
  list2.add(1);
  list2.add(2);
  print(list1);
  print(list2);
  print(list2.first);
  var map1 = Map();
  map1['foo'] = 'bar';
  print(map1);
  map1.forEach((var k, var v){ print('$k: $v');});
}
```



# Variables

Typed syntax

```dart
var name1 = 'Smith';
Sring name2 = 'Smith';
int num = 10;
void main() {
	String name = 1;
}
```

Uninitialed variable has value of null

```dart
int num;
print(num);
```

Final and Const

runtime imuttable vs compile time imuttable

```dart
void main() { 
   final v1 = 12; 
   const v2 = 13; 
   v1 = 13
   v2 = 12; 
}
```

# Operators

Arithmetic

* +
* -
* *
* -
* ~/ (divide return int result)
* % reminder
* ++
* --

Equality

* `>`
*  `<`
*  `>=`
*  `<=`
*  `==`
*  `!=` 

Type testing 

* is
* is!

Type convert

* as

Bitwise

* &
* |
* ^
* ~

Assignment

* =
* ??= (assign value only if value is null)
* +=
* -=
* *=
* /=

Logical

* &&
* ||
* !

Conditional Expression

```dart
void main() {
  int r = 12;
  String res = r > 10 ? 'good' : 'bad';
	print(res);
}
```



# Loops

```dart
void main() {
  for (int i = 1; i < 5; i++) {
    print('hello dart!')
  }
  int i = 1;
  do {
    print('hello dart!');
    i++;
  } while (i < 5);
  while (i < 10) {
    print('hello dart!');
  }
}
```



# Condition

```dart
void main() {
  int i = 10;
  if (i < 1) {
    print('too small');
  } else if (i < 5) {
    print('ok');
  } else {
    print('too big');
  }
}
```



# Enum

```dart
enum Status {
  none,
  running,
  stopped,
  paused,
}
```



# Function

```dart
// optional argument
void func1(int i, [int j]) {
  print(i);
}

// optional parameter
void func2(int i, {int j}) {
  print(i);
}

factorial(int num) {
  if (num <= 0) {
    return 1;
  } else {
    return (num* factorial(num -1 ));
  }
}

void main() {
  func1(1);
  func2(2);
  print(factorial(3));
	void test () => print('arrow function');
  test();
}
```



# Interface

Class declarations are themselves interface.



```dart
class Printer {
  void printData() {
  }
}

class Console {
  void hasConsole() {
  }
}

class ConsolePrinter implements Console,Printer {
  void printData() {
  	print('I can print console');
  }
  
  void hasConsole() {
    print('I have a console');
  }
}

void main() {
  ConsolePrinter cp = ConsolePrinter();
  cp.printData();
  cp.hasConsole();
}
```

# Class

```dart
class Car {
  String engine;
  Car({this.engine});
  void printEngine() {
    print('my engine is $engine');
  }
}

class Student {
  String name;
  String get fullName {
    return name;
  }
  void set fullName(String name) {
    this.name = name;
  }
}

// only support single parent class
class ECar extends Car {
  static int energy = 150;
  String engine;
  ECar({this.engine});
  void charge() {
    print('I am charging');
  }
  
  @override
  void printEngine() {
    super.printEngine();
    print('my e-engine is $engine');
  }
}

void main() {
  Car c = Car(engine: 'E1001');
  c.printEngine();
  print(ECar.energy);
  ECar ec = ECar(engine: 'tesla');
  ec.charge();
  ec.printEngine();
  Student s = Student();
  print(s.fullName);
  s.fullName = 'xdays';
  print(s.fullName);
}
```



# Collection

```dart
import 'dart:collection'; 
void main() { 
   Queue numQ = new Queue(); 
   numQ.addAll([100,200,300]);  
   Iterator i= numQ.iterator; 
   
   while(i.moveNext()) { 
      print(i.current); 
   } 
}
```



# Generics

To be explained



# Packages

```
pub get
pub upgrade
pub build
pub help
```



# Exceptions

* DeferredLoadException
* FormatException
* IntegerDivisionByZeroException
* IOException
* Timeout



```dart
try {
  1/0;
} catch (e) {
  print(e);
} final {
  print('I will be excuted lastly');
}

try {
  1/0;
}
on IntegerDivisionByZeroException {
  print('can not divided by zero!');
}

throw Exception();
```



# Libraries

Encapsulation in library

```dart
_identifier
```

Define a library

```dart
libary name;
```



# Async

```dart
import "dart:async"; 
import "dart:io";  

void main(){ 
   File file = new File('/etc/groups'); 
   Future<String> f = file.readAsString();  
  
   // returns a futrue, this is Async method 
   f.then((data)=>print(data));  
   
   // once file is read , call back method is invoked  
   print("End of main");  
   // this get printed first, showing fileReading is non blocking or async 
}
```



`async` and `await` keyword
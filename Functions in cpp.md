In C++, functions can be categorized into various types based on their functionality, purpose, and how they are defined and used. Here's a detailed breakdown:

---

## **1. Built-in Functions**
These are pre-defined functions provided by C++ as part of its standard library.

### **Examples**:
- `cout`, `cin` (for input/output operations)
- `sqrt()`, `pow()` (from `<cmath>` library for mathematical operations)
- `strlen()`, `strcmp()` (from `<cstring>` for string operations)

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    cout << "Square root of 16: " << sqrt(16) << endl;
    cout << "2 raised to the power 3: " << pow(2, 3) << endl;
    return 0;
}
```

---

## **2. User-Defined Functions**
These are functions created by the programmer to perform specific tasks.

### **Example**:
```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
    return a + b;
}

int main() {
    cout << "Sum: " << add(5, 10) << endl;
    return 0;
}
```

---

## **3. Inline Functions**
Marked with the `inline` keyword, these functions are expanded at the point of call to save function call overhead.

### **Example**:
```cpp
#include <iostream>
using namespace std;

inline int multiply(int a, int b) {
    return a * b;
}

int main() {
    cout << "Product: " << multiply(4, 5) << endl;
    return 0;
}
```

---

## **4. Recursive Functions**
A function that calls itself to solve smaller instances of the same problem. It must have a base case to avoid infinite recursion.

### **Example**:
```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    if (n == 0 || n == 1) return 1; // Base case
    return n * factorial(n - 1);   // Recursive call
}

int main() {
    cout << "Factorial of 5: " << factorial(5) << endl;
    return 0;
}
```

---

## **5. Friend Functions**
A friend function has special access to the private and protected members of a class.

### **Example**:
```cpp
#include <iostream>
using namespace std;

class Box {
private:
    double width;

public:
    Box(double w) : width(w) {}

    // Friend function
    friend double getWidth(Box b);
};

double getWidth(Box b) {
    return b.width;
}

int main() {
    Box box(10.5);
    cout << "Width of box: " << getWidth(box) << endl;
    return 0;
}
```

---

## **6. Static Functions**
A static function is associated with the class rather than any object and can only access static members of the class.

### **Example**:
```cpp
#include <iostream>
using namespace std;

class Counter {
private:
    static int count;

public:
    static void increment() {
        count++;
    }

    static int getCount() {
        return count;
    }
};

int Counter::count = 0;

int main() {
    Counter::increment();
    Counter::increment();
    cout << "Count: " << Counter::getCount() << endl;
    return 0;
}
```

---

## **7. Virtual Functions**
Used in inheritance to achieve **runtime polymorphism**. A virtual function can be overridden in derived classes.

### **Example**:
```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void display() {
        cout << "Base class display" << endl;
    }
};

class Derived : public Base {
public:
    void display() override {
        cout << "Derived class display" << endl;
    }
};

int main() {
    Base* basePtr;
    Derived d;
    basePtr = &d;

    basePtr->display(); // Output: Derived class display
    return 0;
}
```

---

## **8. Pure Virtual Functions**
A pure virtual function is a function that is declared but not defined in the base class. It makes the class abstract.

### **Example**:
```cpp
#include <iostream>
using namespace std;

class Shape {
public:
    virtual void draw() = 0; // Pure virtual function
};

class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing Circle" << endl;
    }
};

int main() {
    Shape* shape = new Circle();
    shape->draw();
    delete shape;
    return 0;
}
```

---

## **9. Lambda Functions**
Introduced in C++11, these are anonymous functions defined inline.

### **Example**:
```cpp
#include <iostream>
using namespace std;

int main() {
    auto add = [](int a, int b) { return a + b; };
    cout << "Sum: " << add(5, 10) << endl;
    return 0;
}
```

---

## **10. Member Functions**
Functions defined within a class.

### **Example**:
```cpp
#include <iostream>
using namespace std;

class Car {
private:
    string brand;

public:
    void setBrand(string b) {
        brand = b;
    }

    void display() {
        cout << "Car Brand: " << brand << endl;
    }
};

int main() {
    Car car;
    car.setBrand("Toyota");
    car.display();
    return 0;
}
```

---

## **11. Overloaded Functions**
Functions with the same name but different parameter types or counts.

### **Example**:
```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int main() {
    cout << "Sum (int): " << add(3, 4) << endl;
    cout << "Sum (double): " << add(3.5, 4.2) << endl;
    return 0;
}
```

---

### **Comparison of Types**

| Function Type          | Key Feature                                       |
|------------------------|---------------------------------------------------|
| Built-in Functions      | Predefined in libraries                          |
| User-defined Functions  | Created by the programmer                        |
| Inline Functions        | Reduced overhead for small tasks                 |
| Recursive Functions     | Calls itself to solve sub-problems               |
| Friend Functions        | Access private/protected members of a class      |
| Static Functions        | Class-level functions, not tied to an object     |
| Virtual Functions       | Supports runtime polymorphism                    |
| Pure Virtual Functions  | Makes the class abstract                         |
| Lambda Functions        | Anonymous functions                              |
| Member Functions        | Defined inside a class                           |
| Overloaded Functions    | Functions with the same name but different usage |

---

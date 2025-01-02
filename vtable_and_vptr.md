### **Vtable and Vptr in C++**

In C++, **Vtable (Virtual Table)** and **Vptr (Virtual Pointer)** are key components of the mechanism that enables **runtime polymorphism** through virtual functions. They allow dynamic method dispatch, ensuring the correct overridden function in the derived class is called when using a base class pointer or reference.

---

### **What is a Vtable?**
1. **Vtable** (short for Virtual Table) is a **data structure** created by the compiler for classes with virtual functions.
2. It is essentially a table (array) of **function pointers**. Each entry in the Vtable corresponds to a virtual function of the class.
3. Every class with virtual functions has its own Vtable, which is created at compile time.

---

### **What is a Vptr?**
1. **Vptr** (short for Virtual Pointer) is a hidden **pointer** added by the compiler to each object of a class with virtual functions.
2. The Vptr points to the **Vtable** of the class corresponding to the object.
3. When a virtual function is called, the Vptr is used to look up the appropriate function in the Vtable and invoke it.

---

### **How Do Vtable and Vptr Work?**

1. **Object Creation**:
   - When an object of a class with virtual functions is created, its Vptr is initialized to point to the Vtable of the class.
2. **Derived Classes**:
   - If the class is inherited and the derived class overrides virtual functions, the derived class's Vtable is created, and the Vptr of derived objects points to this new Vtable.
3. **Function Call**:
   - When a virtual function is called using a base class pointer or reference, the compiler uses the Vptr of the object to access the appropriate function pointer in the Vtable and call the correct function.

---

### **Example**

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void display() {
        cout << "Base class display" << endl;
    }
    virtual void show() {
        cout << "Base class show" << endl;
    }
};

class Derived : public Base {
public:
    void display() override {
        cout << "Derived class display" << endl;
    }
    void show() override {
        cout << "Derived class show" << endl;
    }
};

int main() {
    Base* basePtr; // Base class pointer
    Derived derivedObj;

    basePtr = &derivedObj; // Base class pointer pointing to derived object

    basePtr->display(); // Calls Derived class's display() due to Vtable
    basePtr->show();    // Calls Derived class's show() due to Vtable

    return 0;
}
```

**Output**:
```
Derived class display
Derived class show
```

---

### **Behind the Scenes**

#### Step 1: Vtable Creation
1. The **compiler creates a Vtable** for both `Base` and `Derived` classes:
   - **Base Vtable**:
     - Points to `Base::display()`
     - Points to `Base::show()`
   - **Derived Vtable**:
     - Points to `Derived::display()`
     - Points to `Derived::show()`

#### Step 2: Vptr Initialization
1. When `Derived derivedObj` is created:
   - The **Vptr of `derivedObj`** is initialized to point to the **Derived Vtable**.

#### Step 3: Function Call
1. When `basePtr->display()` is called:
   - The compiler uses the **Vptr** of `derivedObj` to find the **Derived Vtable**.
   - From the Vtable, it retrieves the function pointer for `Derived::display()` and calls it.

---

### **Diagram for Better Understanding**

#### **Memory Layout**
```
+-----------------+       +-----------------------+
| Base Class Obj  | ----> | Base Vtable           |
| Vptr ---------->        | [0]: Base::display()  |
+-----------------+        | [1]: Base::show()     |
                           +-----------------------+

+-----------------+       +-----------------------+
| Derived Obj     | ----> | Derived Vtable        |
| Vptr ---------->        | [0]: Derived::display()|
+-----------------+        | [1]: Derived::show()  |
                           +-----------------------+
```

---

### **Key Points**
1. **Overridden Functions**:
   - If a derived class overrides a virtual function, the derived class's Vtable will have a pointer to the derived class's version of the function.
2. **Non-Virtual Functions**:
   - These do not use the Vtable mechanism. Calls to non-virtual functions are resolved at compile time (static binding).
3. **Vptr Overhead**:
   - Every object of a class with virtual functions has an additional memory overhead for storing the Vptr.
4. **Performance**:
   - Virtual function calls are slightly slower than non-virtual function calls due to the indirection introduced by the Vtable lookup.

---

### **Advantages of Vtable and Vptr**
- Enables **runtime polymorphism**, allowing dynamic behavior based on the actual object type.
- Simplifies code by allowing base class pointers/references to handle derived class objects seamlessly.

---


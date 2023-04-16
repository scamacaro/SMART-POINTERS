# SMART-POINTERS
/* Sanyerlis Camacaro- CSC275 - Sancamac@uat.edu Assignment: Smart Pointers
This code demonstrates how to:
Over comment all your code for the future you in your own words.
Make a great UX. (This can be accomplished with lots of cout statements letting the user know what is going on.)
Your program should do something, in addition, to clearly demonstrating smart pointers.
You need at least one type of smart pointer. A unique_ptr, or shared_ptr, or weak_ptr.
Demonstrate when the pointers go out of scope and therefore the values are deleted.
Hint: Use cout to print something to show when the pointers go out of scope and therefore the values are deleted.

I've prepared a C++ code sample that demonstrates the use of unique_ptr, shared_ptr, and weak_ptr as requested,
while ensuring a good user experience with clear output statements. 
The code comments will help you understand each section and its purpose.

This program demonstrates the use of unique_ptr, shared_ptr, and weak_ptr smart pointers. 
It also provides a clear UX with cout statements describing each step of the process.
*/

#include <iostream> // includes input and out as the standard library.
#include <memory> // allocator

using namespace std; // means using standard namespace and that I dont have to type std:: in front of each line.

// Creating a simple class called MyClass
class MyClass {
public:
    int value;

    MyClass(int v) : value(v) {
        cout << "MyClass object created with value: " << value << endl;
    }

    ~MyClass() {
        cout << "MyClass object with value " << value << " is being destroyed." << endl;
    }
};

void unique_ptr_demo() {
    cout << "\n=== Unique Pointer Demo ===\n" << endl;

    // Creating a unique pointer to manage the MyClass object
    unique_ptr<MyClass> uptr(new MyClass(42));

    // Unique pointers can't be copied, but they can be moved
    // unique_ptr<MyClass> uptr2 = uptr; // This line would cause a compilation error
    unique_ptr<MyClass> uptr2 = move(uptr); // This line transfers ownership from uptr to uptr2

    cout << "Unique pointer demonstration completed." << endl << endl;
}

void shared_ptr_demo() {
    cout << "\n=== Shared Pointer Demo ===\n" << endl;

    // Creating a shared pointer to manage the MyClass object
    shared_ptr<MyClass> sptr(new MyClass(84));

    // Creating another shared pointer that shares ownership with the first one
    shared_ptr<MyClass> sptr2 = sptr;

    // The use_count method returns the number of shared_ptr instances sharing ownership
    cout << "Number of shared pointers owning the MyClass object: " << sptr.use_count() << endl;

    cout << "Shared pointer demonstration completed." << endl << endl;
}

void weak_ptr_demo() {
    cout << "\n=== Weak Pointer Demo ===\n" << endl;

    // Creating a shared pointer to manage the MyClass object
    shared_ptr<MyClass> sptr(new MyClass(168));

    // Creating a weak pointer that observes the MyClass object
    weak_ptr<MyClass> wptr(sptr);

    // The use_count method works with weak_ptr too
    cout << "Number of shared pointers owning the MyClass object: " << wptr.use_count() << endl;

    cout << "Weak pointer demonstration completed." << endl << endl;
}

int main() {
    cout << "Smart pointers demonstration:" << endl << endl;

    unique_ptr_demo();
    // Unique pointer goes out of scope here and deletes the MyClass object

    shared_ptr_demo();
    // Shared pointers go out of scope here and delete the MyClass object

    weak_ptr_demo();
    // The shared pointer goes out of scope here and deletes the MyClass object
    // The weak pointer doesn't affect object lifetime

    cout << "\nAll demonstrations are complete.\n" << endl;

    cout << "\nThank you for using the Smart Pointer Demo!\n" << endl;

    return 0;
}

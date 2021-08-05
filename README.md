# OOP
## Implement Object Oriented programming features in swift and c++

## Abstraction: Abstraction act like a base class. Suppose some types of object have some same functionality and attributes. So what can we do to increase our code reusablity? We can make an abstruct class then implement our common methods and attributes in it. Whatever child class needed those functionality, just inharite this base class and use the base method if it fulfill our requirement or override it. So, abstruct class contain at least one pure virtual method(whose defination is not provided) and have concrite methods or others properties as well. We can not make instance of abstruct class. We can use them through child class. The c++ implementation are given below.

```c++
#include <iostream>

using namespace std;

class Shape {
   public:
      virtual int Area() = 0; // Pure virtual function is declared as follows.
      // Function to set width.
      void setWidth(int w) {
         width = w;
      }
      // Function to set height.
      void setHeight(int h) {
         height = h;
      }
   
   protected:
      int width;
      int height;
};

// A rectangle is a shape; it inherits shape.
class Rectangle: public Shape {
   public:
      // The implementation for Area is specific to a rectangle.
      int Area() { 
         return (width * height); 
      }
};
// A triangle is a shape too; it inherits shape.
class Triangle: public Shape {
   public:
      // Triangle uses the same Area function but implements it to
      // return the area of a triangle.
      int Area() { 
         return (width * height)/2; 
      }
};

int main() {
  Rectangle R;
  Triangle T;
  
  R.setWidth(5);
  R.setHeight(10);

  T.setWidth(20);
  T.setHeight(8);

  cout << "The area of the rectangle is: " << R.Area() << endl;
  cout << "The area of the triangle is: " << T.Area() << endl;
}
```

watch his answer about interface,
"https://stackoverflow.com/questions/318064/how-do-you-declare-an-interface-in-c/9571456#9571456"
## Interface: It only have declaration method. No implementation are provided. So, it's like a template without any detail implementation. Whatever class want to use those template method those class can inharite it. So, we can say a list of pure virtual function and the drive class must need to implement them.

```c++
class IBase {
public:
    virtual ~IBase() {}; // destructor, use it to call destructor of the inherit classes
    virtual void Describe() = 0; // pure virtual method
};

class Tester : public IBase {
public:
    Tester(std::string name);
    virtual ~Tester();
    virtual void Describe();
private:
    std::string privatename;
};

Tester::Tester(std::string name) {
    std::cout << "Tester constructor" << std::endl;
    this->privatename = name;
}

Tester::~Tester() {
    std::cout << "Tester destructor" << std::endl;
}

void Tester::Describe() {
    std::cout << "I'm Tester [" << this->privatename << "]" << std::endl;
}


void descriptor(IBase * obj) {
    obj->Describe();
}

int main(int argc, char** argv) {

    std::cout << std::endl << "Tester Testing..." << std::endl;
    Tester * obj1 = new Tester("Declared with Tester");
    descriptor(obj1);
    delete obj1;

    std::cout << std::endl << "IBase Testing..." << std::endl;
    IBase * obj2 = new Tester("Declared with IBase");
    descriptor(obj2);
    delete obj2;

    // this is a bad usage of the object since it is created with "new" but there are no "delete"
    std::cout << std::endl << "Tester not defined..." << std::endl;
    descriptor(new Tester("Not defined"));


    return 0;
}

```

# C++ Notes

This document contains my notes, sample code, and pseudocode as I dive deeper into my C++ journey. This allows me to create a C++ Reference Guide as I learn, similiar to my [Python Reference Guide](https://github.com/TypicalRandomNerd/python-reference-guide) for Python.



## Namespaces
The first thing one should learn about C++ is namespaces. If you're coming over from C you're likely already familiar with namespaces. However, if you skipped C you are likely to be experiencing namespaces for the first time. A namespace is a scope where functions can reside. This prevents naming conflicts. You'll see C++ programs written in one of two ways: in-code namespaces and globally declared namespaces.


## My first program!
#### Globally declared namespace

    #include <iostream>
    using namespace std;

    int main()
    {
        cout << "Hello, world!";
    }


#### In-line declared namespace

    #include <iostream>

    int main(void)
    {
        std::cout << "Hello, world!";
    }

* They're both the same program.
* "std::" can be omitted by adding "using namespace std" at the top of your code (or any other namespace)
  * If you are familiar with Python, it's the C++ version of "import <libraryname>" and "from libraryname import modulename".
* Void can also be omitted as an argument to the main() function since void doesn't pass anything; however, just know you may see code written both ways, as sampled above.


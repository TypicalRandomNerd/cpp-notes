# C++ Notes

This document contains my notes, sample code, and pseudocode as I dive deeper into my C++ journey. This allows me to create a C++ Reference Guide as I learn, similiar to my [Python Reference Guide](https://github.com/TypicalRandomNerd/python-reference-guide) for Python.

## Getting Started With C++
Lets take a look at our first program:  

**Code:**

    #include <iostream>

    int main()
    {
        std::cout << "Hello, world!";
    }
    
The first time I saw a typical Hello World program in C++ compared to Python, I instantly closed the browser and said C++ isn't for me. It was **that** intimidating to me.  

If you are coming over from something like Python, the above code albeit simple, probably still looks cryptic. We'll be breaking things down as we go and you are sure to have a better understanding of how the C++ language works.

## IWYU: Include What You Use
This is a common phrase you're going to (possibly) hear in the C++ community. C++ is a very old, cryptic, and to be quite honest, dumb language. C++ assumes nothing, and will only do hat you tell it. It will also know know about what you expose to it. This is one of the things that (likely) makes it so fast compared to other languages.  

If we take the cryptic code above of our first program and strip away the #include statement, C++ has no idea what cout is. You haven't told it about the library where cout resides in, so it's completely oblivious to the fact that it even exists.  

**Code:**

    int main()
    {
       std::cout << "Hello World\n"; 
       return 0;
    }

**Output:**

    $g++ -o main *.cpp
    main.cpp: In function ‘int main()’:
    main.cpp:3:9: error: ‘cout’ is not a member of ‘std’
        std::cout << "Hello World\n";
             ^~~~

It knows that the std namespace exists, and we can test that by typing random gobbly goop in place of the std namespace:  

**Code:**

    int main()
    {
       stsdfsdfd::cout << "Hello World\n"; 
       return 0;
    }

**Output:**

    $g++ -o main *.cpp
    main.cpp: In function ‘int main()’:
    main.cpp:3:4: error: ‘stsdfsdfd’ has not been declared
        stsdfsdfd::cout << "Hello World\n";
        ^~~~~~~~~

But it just has no clue what I mean by cout until I tell it at the top of my code to include the iostream library as senn in the original code, our program now executes:  

**Code:**

    #include <iostream>

    int main()
    {
        std::cout << "Hello, world!";
    }
    
**Output:**
    
    $g++ -o main *.cpp
    $main
    Hello, world!

## Namespaces
Like the libraries, namespaces also have to be declared before the compiler knows what you are talking about. Namespaces can be declared in one of two ways: globally, and in-line.

#### Globally declared

    using namespace namespacename;

#### In-line declared

    namespacename::function();
    
Without declaring a namespace, we'll run into compiling errors.

**Code:**

    #include <iostream>

    int main()
    {
        cout << "Hello, world!";
    }
    
**Output:**

    $g++ -o main *.cpp
    main.cpp: In function ‘int main()’:
    main.cpp:5:5: error: ‘cout’ was not declared in this scope
         cout << "Hello, world!";
         ^~~~
    main.cpp:5:5: note: suggested alternative:
    In file included from main.cpp:1:0:
    /usr/include/c++/7/iostream:61:18: note:   ‘std::cout’
       extern ostream cout;  /// Linked to standard output
                      ^~~~



## The main() Function
Every C++ program must have a main() function. This was vastly different from me coming over from Python since that's not the case with that language.

## My first program!
#### Globally declared namespace

**Code:**

    #include <iostream>
    using namespace std;

    int main()
    {
        cout << "Hello, world!";
    }

**Output:**

    $g++ -o main *.cpp
    $main
    Hello, world!

#### In-line declared namespace

**Code:**

    #include <iostream>

    int main(void)
    {
        std::cout << "Hello, world!";
    }

**Output:**

    $g++ -o main *.cpp
    $main
    Hello, world!

If you include your namespaces globally, you don't have to declare them in-line in your code.  

>Not to be confused with the actual _#include_ line, which is for libraries.  




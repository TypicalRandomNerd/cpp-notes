# C++ Notes

This document contains my notes, sample code, and pseudocode as I dive deeper into my C++ journey. This allows me to create a C++ Reference Guide as I learn, similiar to my [Python Reference Guide](https://github.com/TypicalRandomNerd/python-reference-guide) for Python.

## Getting Started With C++
Lets take a look at our first program:

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

    int main()
    {
       std::cout << "Hello World\n"; 
       return 0;
    }



    $g++ -o main *.cpp
    main.cpp: In function ‘int main()’:
    main.cpp:3:9: error: ‘cout’ is not a member of ‘std’
        std::cout << "Hello World\n";
             ^~~~

It knows that the std namespace exists, and we can test that by typing random gobbly goop in place of the std namespace:

    int main()
    {
       stsdfsdfd::cout << "Hello World\n"; 
       return 0;
    }



    $g++ -o main *.cpp
    main.cpp: In function ‘int main()’:
    main.cpp:3:4: error: ‘stsdfsdfd’ has not been declared
        stsdfsdfd::cout << "Hello World\n";
        ^~~~~~~~~

But it just has no clue what I mean by cout until I tell it at the top of my code to include the iostream library as senn in the original code, our program now executes:

    #include <iostream>

    int main()
    {
        std::cout << "Hello, world!";
    }
    
    
    
    $g++ -o main *.cpp
    $main
    Hello, world!

## Namespaces
The first thing one should learn about C++ is namespaces. If you're coming over from C you're likely already familiar with namespaces. However, if you skipped C you are likely to be experiencing namespaces for the first time. A namespace is a scope where functions can reside. This prevents naming conflicts. You'll see C++ programs written in one of two ways: in-code namespaces and globally declared namespaces.

#### Globally declared

    using namespace namespacename;

#### In-line declared

    namespacename::function();
    
## The main() Function
Every C++ program must have a main() function. This was vastly different from me coming over from Python since that's not the case with that language.

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


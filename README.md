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

>**NOTE:** Not to be confused with the actual _#include_ line, which is for libraries.  

It is already becoming a lot and we haven't even set our first variable yet, but without these foundational skills you will not be able to understand how to get beyond a basic "Hello, world!" program.

## New Line
Remember how I said C++ is an incredibly stupid and cryptic language and it will only do what you explicitly tell it to? The same comes to a new line. If you try to run cout statements in succession to print multiple lines of text, C++ will start the next line right against the end of the preceding line unless you tell it to break a new line.  

**Code:**

    #include <iostream>
    using namespace std;

    int main()
    {
      cout << "Hello World!";
      cout << "I am learning C++";
      return 0;
    }
    
**Output:**

    $g++ -o main *.cpp
    $main
    Hello World!I am learning C++
    
We can instruct C++ to move down a line in one of two ways:

#### \n escape sequence
Beginning or ending a string with "\n" will instruct the compiler to move down a line.

**Code:**

    #include <iostream>
    using namespace std;

    int main() {
      cout << "Hello World!\n";
      cout << "\nI am learning C++";
      return 0;
    }
    
**Output:**

    $g++ -o main *.cpp
    $main
    Hello World!

    I am learning C++
    
A line is skipped because we instruct it to move down a line at the end of the first cout statement; then again at the beginning of the second cout statement. If we only use the \n sequence in the first cout statement, then the second cout statement would be right under the first statement:

**Output:**

    $g++ -o main *.cpp
    $main
    Hello World!
    I am learning C++

#### endl
endl is a string manipulator in the std namespace, so to use it we must either declare the std namespace globally or in-line when we call endl.

**Code:**

    #include <iostream>
    using namespace std;

    int main() {
      cout << "Hello World!" << endl;
      cout << "I am learning C++";
      return 0;
    }
    
**Output:**

    $g++ -o main *.cpp
    $main
    Hello World!
    I am learning C++
    
Whether to use the \n escape sequence or the endl string manipulator is not a one-size-fits-all choice. Like with anything else, _**use the best tool for the job**_.

## Commenting
Code commenting is something you will without a doubt do and can be done in two different ways.

#### Single Line
A single line comment can be accomplished by using two slashes //

    cout << "Hello World!"; // This is a comment

#### Multi Line
Multi line comments are common when you need to describe a snippet of code in more detail and can be accomplished with the /*.

    /* The code below will print the words Hello World!
    to the screen, and it is amazing */
    cout << "Hello World!";

This document contains my notes, sample code, and pseudocode as I dive deeper into my C++ journey. This allows me to create a C++ Reference Guide as I learn, similiar to my [Python Reference Guide](https://github.com/TypicalRandomNerd/python-reference-guide) for Python.

I will do my best to explain things, but it is recommended to have some programming experience to better understand this guide, preferably in Java or C#. This is not a full book, but instead a shortcut guide, so if you lack knowledge of what a variable is and how to access and evaluate variables in other languages then this probably isn't for you. Instead, a fully fledged C++ book such as C++ Crash Course may be better suited for you.

# Getting Started With C++

## The Basics

C++ is a strongly typed programming language. The language assumes nothing and only does what the programmer (you) tells it to do.

Lets take a look at our first program:  

**Code:**

    #include <iostream>

    int main()
    {
        std::cout << "Hello, world!";
    }
    
The first time I saw a typical Hello World program in C++ compared to Python, I instantly closed the browser and said C++ isn't for me. It was **that** intimidating to me.  

If you are coming over from something like Python, the above code albeit simple, probably still looks cryptic. We'll be breaking things down as we go and you are sure to have a better understanding of how the C++ language works.

#### IWYU: Include What You Use
This is a common phrase you're going to (possibly) hear in the C++ community. C++ is a very old, cryptic, and to be quite honest, dumb language. C++ assumes nothing, and will only do hat you tell it. This is one of the things that (likely) makes it so fast compared to other languages.  

If we take the cryptic code above of our first program and strip away the `#include` statement, C++ has no idea what `cout` is. You haven't told it about the library where `cout` resides in, so it's completely oblivious to the fact that it even exists.  

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

It knows that the `std` namespace exists, and we can test that by typing random gobbly goop in place of the `std` namespace:  

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

But it just has no clue what I mean by cout until I tell it at the top of my code to include the `iostream` library as seen in the original code, our program now executes:  

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

#### Namespaces
Like the libraries, namespaces also have to be declared before the compiler knows what you are talking about. Namespaces can be declared in one of two ways: globally, and in-line.

##### Globally declared

    using namespace namespacename;

##### In-line declared

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



#### The main() Function
Every C++ program must have a `main()` function. This was vastly different from me coming over from Python since that's not the case with that language. Typically a more complex program will have functions where the logic for different parts of your program is stored, and it will all come together within the `main()` function where everything wil actually be executed.

#### My first program!
##### Globally declared namespace

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

##### In-line declared namespace

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

>**NOTE:** Not to be confused with the actual `#include` line, which is for libraries.  

It is already becoming a lot and we haven't even set our first variable yet, but without these foundational skills you will not be able to understand how to get beyond a basic "Hello, world!" program.

#### New Line
Remember how I said C++ is an incredibly stupid and cryptic language and it will only do what you explicitly tell it to? The same comes to a new line. If you try to run `cout` statements in succession to print multiple lines of text, C++ will start the next line right against the end of the preceding line (on the same line) unless you tell it to break a new line.  

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

##### \n escape sequence
Beginning or ending a string with `\n` will instruct the compiler to move down a line.

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
    
A line is skipped because we instruct it to move down a line at the end of the first `cout` statement; then again at the beginning of the second `cout` statement. If we only use the `\n` sequence in the first `cout` statement, then the second `cout` statement would be right under the first statement:

**Output:**

    $g++ -o main *.cpp
    $main
    Hello World!
    I am learning C++

##### endl
`endl` is a string manipulator in the `std` namespace, so to use it we must either declare the `std` namespace globally or in-line when we call `endl`.

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
    
Typically the `\n` escape sequence is preferred over `endl`; however, either one will do the jpb. The main difference is `endl` clears the buffer, where `\n` does not, so one _could_ yield different results in your program over the other.

#### Commenting
Code commenting is something you will without a doubt do and can be done in two different ways.

##### Single Line
A single line comment can be accomplished by using two slashes `//`.

    cout << "Hello World!"; // This is a comment

##### Multi Line
Multi line comments are common when you need to describe a snippet of code in more detail and can be accomplished with the `/* */` syntax.

    /* The code below will print the words Hello World!
    to the screen, and it is amazing */
    cout << "Hello World!";

There is no right or wrong when it comes to commenting; however, it is best to keep comments as short as possible.

#### Variables
Variables in C++ must be defined with a data type. Different datatypes are declared slightly differently.

* Any numerical datatype (int, float, double) is defined as `datatype var = value`. Where `value` is would be the integer.
* Strings are defined as `string variable = "value"`. Notice the `value` has double-quotes `" "` surrounding it. Unlike other programming languages such as Python, you cannot chose to use single `'` or double `"` quotes.
* Chars are defined as `char variable = 'value'`, where `'value'` is would be the character of your choice. Notice the single quotes `' '` surrounding the value. Char datatypes must be defined with a single `'` quote.  

#### Instantiating variables

Variables may be instantiated and declared on a single line, or broken up between declaring and instantiating.

**Code:**

    int myNum;
    myNum = 15;
    cout << myNum;

>or

**Code:**

    int myNum = 15;
    cout << myNum;
    
#### Multiple variables may be declared and instantiated on the same line of code, as long as the variables are all of the same data type.
 
    int x = 5, y = 6, z = 50;
    cout << x + y + z;

## Input
Input is captured primarily in one of two ways: `cin` or `getline`. `cin` works well for intergers and single word strings, but if you are trying to capture a phrase, `cin` will only capture the first word, at which you will need to use `getline`.

#### cin

**Code:**

    string name; // Create a string variable
    cout << "Hello, what is your name? \n"; // Prompt user for their name
    cin >> name; // Capture input in our newly created variable
    
#### getline()

**Code:**

    string name;
    cout << "Hello, what is your name? \n";
    getline(cin, name);
    cout << name;
    
We create a string type called name, then we prompt the user for their name, we call the `getline()` method and pass the `cin` command along with the variable the input is to be stored in.

#### Operators
Operators work the same in C++ as any other language, so they will be skipped. If you need a refresher, [this](https://www.google.com/search?q=programming%20with%20operators&cad=h) will get you up to speed.

#### IF Statements
If statements are powerful statements that check for conditions, and performs a certain action depending on the conditional check.

**Code:**

    int main()
    {
        int a = 1;
        int b = 2;

        if (a > b)
        {
            cout << a << " is greater than " << b << "\n";
        }
        else
        {
            cout << b << " is greater than " << a << "\n";
        }
    }

We're comparing the value of `a` and `b`. If the value of `a` is greater, we print the values and state the value of `a` is greater than `b`. If `a` is not greater than `b`, then we print the value of `b` and state that it is greater than `a`.

#### Switch Statements
Switch statements are kind of like if statements, but very cryptic, and can be somewhat limiting. They use `switches` known as `cases` to determine which statement is executed.

* Switch statements can only be used with `char`, `int`, and `enum` datatypes
* Case labels must be constants
* Must execute a `break` at the end of each `case`

#### While Statements
While `X` is true do `Y`. In a nutshell, that's what a while statement is. While statements should be used with caution because it is easy to put yourself in an infinite loop.

**Code:**

    int main()
    {
        int i = 1;
        while (true)
        {
            cout << i * i << '\n';
            ++i;
        }
    }

The following code puts the program in an infinite loop where it prints out square roots starting with 1 going on until the computer runs into what is called an overflow. You'll notice numbers eventually go negative, then back to positive, and negative again. While this doesn't cause our simple 10 line console program to crash, a more complicated program would cease to function properly and may outright crash and throw an exception.

#### For Loops
A more common loop type is your for loop, also known as an `iteration` statement. In other languages, they may be called a `for each` loop. A for loop will iterate through something -- maybe an array (list if you are coming from Python), or even just a range of numbers, and executes a statement for each iteration.

**Code:**

    int main()
    {
        for (int i = 0; i < 5; ++i)
        {
            cout << i << "\n";
        }
    }
    
The most basic for loop new programmers are exposed to. Essentially we set the variable `i` to `0`, then we say if `i` is less than `5`, print out `i`, then increment it. If it looks confusing to you, picture it like this:

**Code:**

    int main()
    {
        int i = 0;
        while (i < 5)
        {
            cout << i << "\n";
            ++i;
        }
    }
    
#### Functions
A function is a sequence of code -- or really an algorithm -- that is executed when the function is called. It is a great way to reuse code without having to copy and paste the code every time you want to use it. They can also take arguments, which can make the code within the function more dynamic.

**Code:**

    int cubed()
    {
        int i;
        cout << "Welcome to my first program, Square Root finder.\n\nPlease enter an integer: ";
        cin >> i;
        cout << i << " cubed == " << i * i * i << "\n\n";

        char play_again;
        cout << "Would you like to go again? ";
        cin >> play_again;


        switch (play_again)
        {
            case 'y':
                cout << "\n";
                cubed();
                break;
            case 'n':
                cout << "\nThank you for playing.\n";
                break;
            default:
                cout << "That is not a valid selection.\n";
                break;
        }
    }
    
>Our `function` is named `cubed`, which asks for input of an integer, returns the cubed value, and asks the player if they'd like to play again using a `switch` statement.

#### Vector
A dynamic data structure used to store or hold data that can be accessed by an `index`. Indexes begin with `0`, and incrementally go up. The first item in a vector has an index of `0`, the second has an index of `1`, the third with an index of `2`, and on.

##### Initializing a Vector
    vector<datatype> variable = {"value1", "value2", "value3"};
    
Remember how we declared strings with double quotes `"`, chars with single quotes `'`, and ints, doubles, and floats with no quotes? The same applies here, so to create a vector of strings, we would use the following syntax:

    vector<string> words = {"Word One", "Word Two", "Word Three"};
    
A vector may be initialized with blank values:

    vector<int> ints(10)
    
The `10` denotes the length of the vector.

* Cannot mix datatypes in a vector
  * For instance, an `int` vector may only contain `int` values
  
##### Accessing a Vector With a For Loop

    int main()
    {
        vector<int> ints = {1, 2, 3, 4, 5};
        for (int i = 0; i < ints.size(); ++i)
            cout << ints[i] << "\n";
    }

* First we initiate our vector and assign it 5 values
* Then we create a `for loop` that iterates through the vector
  * We use `size()` because without it we don't know how big the `vector` is
    * If we do `cout << ints.size() << "\n"`, we would receive an output of `5`
* And finally, we print out each value in the vector

If you are coming over from Python (like myself), think of `size()` as `len()` from Python. The only difference here is in Python, we don't have to pass the `len()`, or `size()` in our case because Python is smart enough to determine the length of a list or `vector` in C++ terms, whereas C++ is extremely cryptic and has no idea how long the `vector` is unless we tell it with the `size()` function.

##### Accessing a Vector With a Half-Open Sequence
A shortcut that can be used to loop through a vector with a `range for loop`. A `range for loop` does the same exact thing as the aforementioned `for loop`, but the syntax is much more simple.

**Code**

    int main()
    {
        vector<int> ints = {35, 30, 36, 5, 2};
        for (int x : ints)
            cout << x << "\n";
    }
    
The way we interpret this code in the `for loop` is "for each `x` in `ints`, print the value of `x` to the console". Much more simple than `for (int i = 0; i < ints.size(); ++i);`.

##### Expanding Our Vector
A vector can by dynamically increased with the `push_back()` function.

Start with an empty `vector`, then add to it:

int main()
{
    vector<int> ints = {35, 30, 36, 5, 2};
    for (int x : ints)
        cout << x << "\n";
}
    

# C-learning
Notes and Reviews from C++ learning -> C++ from programmer Udacity

## 1. Basics

### Adding comments

Comments can be added in **two ways**
1. As a comment **block**
2. As a single **line**

The prompt is enclosed in the symbols: '/*' and '*/'. This is how we signify comment block. For example:

```c++
    /*The start of a comment block.
     Everything between is in the comment block.
     The end of a comment block.*/
```

Adding asterisks for each line of the comment block is not necessary, but it draws the attention to the comment block.

A comment can be added as a single line by preceding the comment with two slash marks **( // )**.

### Style Guides

There are a number of style guides available, **the best one is the one used by the people who are paying you.**

A straightforward style guide is:
               [Modern C++ Coding Guidelines](https://github.com/Microsoft/AirSim/blob/master/docs/coding_guidelines.md)
               
For a more detailed guideline:
               [Google C++ Style Guideline](https://google.github.io/styleguide/cppguide.html)

### Using Namespace

```c++
using namespace std;
 int main()
 {
 }
```
This tells the compiler to assume we are using the standard library, so **we don’t have to write std::.**

**Some controversy about using namespace:** When the commands are not explicitly defined, there is a possibility that when your code is added to a large project, your code might reference a command from a different library.

### Define Constants

In C++ we can define a variable as a constant. Meaning, its value does not change for the life of the program.
 
We use the keyword 'const' to define a constant. For example: 
```c++
const int weightGoal = 100;
```

With this statement we have set the integer weightGoal to 100. It cannot be changed during the program. If you want to change the value of weightGoal, you will have to edit the source code and recompile it.

### Enumerated Constats

C++ also allows for enumerated constants. This means the programmer can create a new variable type and then assign a finite number of values to it. Here is the form of the enum keyword:

```c++
enum type_name {
  value1,
  value2,
  value3,
  .
  .
} object_names;
```

### Format output

To format data we can use escape sequences. These do not require any additional libraries.

The most common ones are: 
- **\n - newline 
- \t - tab **

We can also format the output by using the **iomanip** library. Include it as #include.  For example, we can set the width of an output using the **setw** command.

```c++
#include <iomanip>

std::cout<<"\n\nThe text without any formating\n";
std::cout<<"Ints"<<"Floats"<<"Doubles"<< "\n";
std::cout<<"\nThe text with setw(15)\n";
std::cout<<"Ints"<<std::setw(15)<<"Floats"<<std::setw(15)<<"Doubles"<< "\n";
std::cout<<"\n\nThe text with tabs\n";
std::cout<<"Ints\t"<<"Floats\t"<<"Doubles"<< "\n";
```

Output will be:
```
The text without any formating
IntsFloatsDoubles

The text with setw(15)
Ints         Floats        Doubles


The text with tabs
Ints    Floats    Doubles
```

### File IO

File IO steps:
- Include the <fstream> library 
 - Create a stream (input, output, both)
      - ofstream myfile; (for writing to a file)
      - ifstream myfile; (for reading a file)
      - fstream myfile; (for reading and writing a file)
 - Open the file  myfile.open(“filename”);
 - Write or read the file
 - Close the file myfile.close();

```c++
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main () {
    string line;
    //create an output stream to write to the file
    //append the new lines to the end of the file
    ofstream myfileI ("input.txt", ios::app);
    if (myfileI.is_open())
    {
        myfileI << "\nI am adding a line.\n";
        myfileI << "I am adding another line.\n";
        myfileI.close();
    }
    else cout << "Unable to open file for writing";

    //create an input stream to read the file
    ifstream myfileO ("input.txt");
    //During the creation of ifstream, the file is opened. 
    //So we do not have explicitly open the file. 
    if (myfileO.is_open())
    {
        while ( getline (myfileO,line) )
        {
            cout << line << '\n';
        }
        myfileO.close();
    }

    else cout << "Unable to open file for reading";

    return 0;
}
```

### Header Files

As we have seen we can include additional libraries in C++, we can also include **our own libraries.**

Traditionally, these files are called header files and they have an **.hpp extension**. Although **any extension will work.**

- Header files contain information about how to do a task.
- The main program contains information about what to do.

Add a statement to include main.hpp
```c++
#include "main.hpp"
```
**Please note … I’m using double quotes here.**

Then we create a header file. We moved the include and the using statements from the main.ccp and put them in the header file.

### User Input

std::cin for reading from the console.

##String Input

So, we now know that std::cin will not retrieve strings that have a space in them. It will see the space as the end of the input. We will obviously need a method to enter strings.

C++ has a function called getline.

**getline:** it will retrieve characters from the std::cin source and stores them in the variable called variableName. It will retrieve all characters until the newline or “\n” is detected.

[Information on the getline command](http://www.cplusplus.com/reference/string/string/getline/)

### To convert the string variable to a numeric variable.

Steps for using Stringstream:

1. Include the Stringstream library.
```c++
#include<sstream>
 ```
2. Use getline to get the string from the user
```c++
std::getline(std::cin, stringVariable);
```
3. Convert the string variable to a float variable.
```c++
std::stringstream(stringVariable) >> numericVariable;
```

Information about string stream can be found at: [StringStream tutorial](http://www.cplusplus.com/reference/sstream/)

## 2. Compilation and execution

### Compiling

Compiling is the process of translating the code that you've written into machine code that processors understand. Every program, regardless of the source language, needs to be compiled in order to execute. This is true even for scripting languages like Python or JavaScript. In these cases, the interpreter (or a similar system) is responsible for compiling code on the fly in a process known as just-in-time compiling. To the user, compilation and execution of scripting languages are effectively a single action. (Of course, the actual process of compiling code at run-time is much more complicated than what was described here in one sentence. It's also very much dependent on the exact language and runtime in question.)

Unlike scripted languages, compiled languages treat compilation and execution as two distinct steps. Compiling a program leaves you with an executable (often called a "binary"), a non-human readable file with machine code that the processor can run.

The nice thing about binaries is that they're generally distributable. So long as it was built with the right architecture in mind, you can copy an executable and run it immediately on other machines (like downloading a .exe file on Windows) without any need to share your source code or have the user perform any intermediate tasks before execution.

There are many tools available to help you compile, ranging from barebones tools, such as **g++** on Unix, to complex build systems that are integrated into IDEs like Visual Studio and Eclipse.

There is a high-level build tool called **CMake** that is fairly popular and cross-platform. CMake in and of itself, however, does not compile code. CMake results in compilation configurations. It depends on a lower-level build tool called **Make** to manage compiling from source. And then Make depends on a compiler to do the actual compiling.

### Object Files

Compiling source code, like a single .cpp file, results in something called an object file. An object file contains machine code but may not be executable in and of itself. Among other things, object files describe their own public APIs (usually called symbols) as well as references that need to be resolved from other object files. Depended upon object files might come from other source files within the same project or from external or system libraries.

In order to be executable, object files need to be linked together.

### Linking

Linking is the process of creating an executable by effectively combining object files. During the linking process, the linker (the thing that does the linking) resolves symbolic references between object files and outputs a self-contained binary with all the machine code needed to execute.

As an aside, linking is not required for all programs. Most operating systems allow **dynamic linking**, in which symbolic references point to libraries that are not compiled into the resulting binary. With dynamic linking, these references are resolved at runtime. An example of this is a program that depends on a system library. At runtime, the symbolic references of the program resolve to the symbols of the system library.

There are **pros and cons of dynamic linking**. On the one hand, dynamically linked libraries are not linked within binaries, which keeps the overall file size down. However, if the library changes at any point, your code will automatically link to the new version. Like any changing dependency, difficult to fix and surprising bugs sometimes arise when versions change.

## Compiling to Executable with a Compiler

Technically, you only need a compiler to compile C++ source code to a binary. A compiler does the dirty work of writing machine code for a given processor architecture. There are many compilers available. For this course, we picked the open source GNU Compiler Collection, more commonly called **G++** or **GCC**. gcc is a command line tool.

There are two challenges with using gcc alone, both of which relate to the fact that most C++ projects are large. For one thing, you need to pass the paths for all of the project's source header files and cpp files to gcc. This is in addition to any compiler flags or options. You can easily end up with single call to gcc that spans multiple lines on a terminal, which is unruly and error-prone.

Secondly, large projects will usually contain multiple linked binaries, each of which is compiled individually. If you're working in large project and only change one .cpp file, you generally only need to recompile that one binary - the rest of your project does not need to be compiled again! Compiling an entire project can take up to hours for large projects, and as such being intelligent about only compiling binaries with updated source code can save lots of time. GCC in and of itself is not smart enough to recognize what files in your project have changed and which haven't, and as such will recompile binaries needlessly - you'd need to manually change your gcc calls for the same optimizations. Luckily, there are tools that solve both of these problems!

#### References for using C++: 

- [Using C++ in a Unix Environment](https://www.cs.drexel.edu/~mcs171/Sp07/extras/g++/index.html)
- [Using C++ in a Windows Environment](https://arachnoid.com/cpptutor/setup_windows.html)

#### In summary to compile in a terminal:
1. Open a terminal window
2. Change the working directory to the directory of the program.
3. To compile the program: g++ filename.cpp -o executableName.
4. To execute the program: ./executableName.

**Common mistakes when executing in the terminal:**
- Make sure there are no spaces in filenames
- Make sure all the files you need are in the working directory (including header files), use 'ls' to check

## 3. Arithmetic Operations

Something different with other programming languages is the need of explicity assing of data types to variables. This low level aspect of C and C++ is what makes them so efficient. 

When doing math operations you may need to include the **cmath** library, it contains a number of useful functions.

[Additional details] (http://www.cplusplus.com/doc/tutorial/operators/)


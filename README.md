# C-learning
Notes and Reviews from C++ learning -> C++ from programmer Udacity

## Basics

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




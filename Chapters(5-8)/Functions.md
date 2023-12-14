# Chapter 6: Functions

## Objectives
- Define functions with formal parameters.
- Define and invoke value-returning and void functions.
- Pass arguments by value and understand their scope.
- Develop reusable, modular, easy to read, debug, and maintain code.
- Understand function overloading and ambiguous overloading.
- Use function prototypes to declare function headers.
- Define functions with default arguments.
- Improve runtime efficiency with inline functions.
- Determine the scope of local and global variables.
- Pass arguments by reference and understand differences between pass-by-value and pass-by-reference.
- Declare const parameters to prevent accidental modification.
- Write a function to convert hexadecimal numbers to decimal.
- Design and implement functions using stepwise refinement.

## 6.1 Introduction to Functions
- Functions define reusable code and organize/simplify code.
- Example of using functions to find the sum of integers within a specified range.

### Function to Compute Sum from `i1` to `i2`
```cpp
int sum(int i1, int i2) {
    int sum = 0;
    for (int i = i1; i <= i2; i++)
        sum += i;
    return sum;
}

int main() {
    cout << "Sum from 1 to 10 is " << sum(1, 10) << endl;
    cout << "Sum from 20 to 37 is " << sum(20, 37) << endl;
    cout << "Sum from 35 to 49 is " << sum(35, 49) << endl;
    return 0;
}
```

### 6.2 Defining a Function
- A function definition includes the function name, parameters, return value type, and body.
- Syntax for defining a function.

Example of a function to find the maximum of two integers.
```cpp
int max(int num1, int num2) {
    int result;
    if (num1 > num2)
        result = num1;
    else
        result = num2;
    return result;
}
```

### 6.3 Calling a Function
- Calling a function executes its code.
- Value-returning functions can be invoked as values or statements.

Example of a program to test the max function:
```cpp
int main() {
    int i = 5, j = 2, k = max(i, j);
    cout << "The maximum between " << i << " and " << j << " is " << k << endl;
    return 0;
}
```

### 6.4 Void Functions
- Void functions do not return a value.

Example: function to print a grade for a given score:
```cpp
void printGrade(double score) {
    if (score >= 90.0)
        cout << 'A' << endl;
    else if (score >= 80.0)
        cout << 'B' << endl;
    // Additional conditions...
}
```

### 6.5 Passing Arguments by Value
- Arguments are passed by value to functions.

Example: function to print a character n times:
```cpp
void nPrint(char ch, int n) {
    for (int i = 0; i < n; i++)
        cout << ch;
}
```

### 6.6 Modularizing Code
- Modularizing code makes it easy to maintain and debug, and enables code reuse.

Examples: Functions for computing GCD and printing prime numbers:
```cpp
int gcd(int n1, int n2) {
    while (n2 != 0) {
        int temp = n2;
        n2 = n1 % n2;
        n1 = temp;
    }
    return n1;
}
```

### 6.7 Overloading Functions
- Functions can be overloaded if they have different parameter lists.

Example: Overloading the max function for int and double types:
```cpp
int max(int num1, int num2) {
    if (num1 > num2)
        return num1;
    else
        return num2;
}

double max(double num1, double num2) {
    if (num1 > num2)
        return num1;
    else
        return num2;
}

double max(double num1, double num2, double num3) {
    return max(max(num1, num2), num3);
}

int main() {
    cout << "The maximum between 3 and 4 is " << max(3, 4) << endl;
    cout << "The maximum between 3.0 and 5.4 is " << max(3.0, 5.4) << endl;
    cout << "The maximum between 3.0, 5.4, and 10.14 is " << max(3.0, 5.4, 10.14) << endl;
    return 0;
}
```

### 6.8 Function Prototypes
- Function prototypes declare a function without implementing it.
- Prototypes allow function calls before the function definition.

Example: Prototypes for overloaded max functions:
```cpp
int max(int num1, int num2);
double max(double num1, double num2);
double max(double num1, double num2, double num3);

int main() {
    cout << "The maximum between 3 and 4 is " << max(3, 4) << endl;
    cout << "The maximum between 3.0 and 5.4 is " << max(3.0, 5.4) << endl;
    cout << "The maximum between 3.0, 5.4, and 10.14 is " << max(3.0, 5.4, 10.14) << endl;
    return 0;
}

int max(int num1, int num2) {
    if (num1 > num2)
        return num1;
    else
        return num2;
}

double max(double num1, double num2) {
    if (num1 > num2)
        return num1;
    else
        return num2;
}

double max(double num1, double num2, double num3) {
    return max(max(num1, num2), num3);
}
```

### 6.9 Default Arguments
- Default arguments are used if no arguments are passed to a function.

Example: Function for raising a number to a power, with default exponent:
```cpp
double pow(double base, int exponent = 2) {
    double result = 1;
    for (int i = 0; i < exponent; i++)
        result *= base;
    return result;
}

int main() {
    cout << "2^3 is " << pow(2, 3) << endl;
    cout << "2^2 is " << pow(2) << endl;
    return 0;
}
```

### 6.10 Inline Functions
- Inline functions increase efficiency by avoiding function calls for small, frequently called functions.

Example: Inline function for square of a number:
```cpp
inline int square(int num) {
    return num * num;
}

int main() {
    cout << "The square of 3 is " << square(3) << endl;
    return 0;
}
```

### 6.11 Scope of Variables
- Variables declared in a function are local to that function.
- Variables declared outside of all functions are global to the program.
- Local variables are destroyed when the function returns.
- Global variables are destroyed when the program terminates.
- Local variables can have the same name as global variables.
- Local variables take precedence over global variables.

Example: Differentiating local and global variables:
```cpp
int x = 1; // Global variable

void function1() {
    int x = 5; // Local variable
    cout << "Local x: " << x << endl;
}

int main() {
    cout << "Global x: " << x << endl;
    function1();
    return 0;
}
```

### 6.12 Passing Arguments by Reference
- Passing arguments by reference allows functions to modify arguments.
- Arguments are passed by reference by using the `&` operator.

Example: Function to swap two variables:
```cpp
void swap(int& n1, int& n2) {
    int temp = n1;
    n1 = n2;
    n2 = temp;
}

int main() {
    int num1 = 1;
    int num2 = 2;
    cout << "Before invoking the swap function, num1 is " << num1 << " and num2 is " << num2 << endl;
    swap(num1, num2);
    cout << "After invoking the swap function, num1 is " << num1 << " and num2 is " << num2 << endl;
    return 0;
}
```

### 6.13 Const Parameters
- Const parameters prevent accidental modification of arguments.
- Const parameters are declared with the `const` keyword.
- Const parameters can be passed by value or by reference.
- Const parameters passed by reference can only be used in read-only operations.

Example: Function to convert a hexadecimal digit to decimal:
```cpp
int hexDigitToDecimal(const char& ch) {
    if (ch >= 'A' && ch <= 'F')
        return 10 + ch - 'A';
    else // ch is '0', '1', ..., or '9'
        return ch - '0';
}

int main() {
    cout << hexDigitToDecimal('A') << endl;
    cout << hexDigitToDecimal('B') << endl;
    cout << hexDigitToDecimal('C') << endl;
    cout << hexDigitToDecimal('D') << endl;
    cout << hexDigitToDecimal('E') << endl;
    cout << hexDigitToDecimal('F') << endl;
    cout << hexDigitToDecimal('1') << endl;
    cout << hexDigitToDecimal('2') << endl;
    cout << hexDigitToDecimal('3') << endl;
    cout << hexDigitToDecimal('4') << endl;
    cout << hexDigitToDecimal('5') << endl;
    cout << hexDigitToDecimal('6') << endl;
    cout << hexDigitToDecimal('7') << endl;
    cout << hexDigitToDecimal('8') << endl;
    cout << hexDigitToDecimal('9') << endl;
    cout << hexDigitToDecimal('0') << endl;
    return 0;
}
```
### 6.14 Temperature Converter Function
Write a function to convert temperatures between Fahrenheit and Celsius.

```cpp
#include <iostream>
using namespace std;

// TODO: Define the function to convert Fahrenheit to Celsius
double fahrenheitToCelsius(double fahrenheit) {
    // Your code here
    return 0; // Replace with the correct calculation
}

// TODO: Define the function to convert Celsius to Fahrenheit
double celsiusToFahrenheit(double celsius) {
    // Your code here
    return 0; // Replace with the correct calculation
}

int main() {
    // Example usage
    double fahrenheit = 70;
    // TODO: Call the fahrenheitToCelsius function and print the result
    cout << fahrenheit << "°F is " << fahrenheitToCelsius(fahrenheit) << "°C." << endl;

    double celsius = 20;
    // TODO: Call the celsiusToFahrenheit function and print the result
    cout << celsius << "°C is " << celsiusToFahrenheit(celsius) << "°F." << endl;

    return 0;
}
```

### 6.15 Simple Interest Calculator
Implement a function to calculate simple interest.

```cpp
#include <iostream>
using namespace std;

// TODO: Define the function to calculate simple interest
double calculateSimpleInterest(double principal, double rate, int time) {
    // Your code here
    return 0; // Replace with the correct calculation
}

int main() {
    // Example values
    double principal = 1000;
    double rate = 5; // 5% interest rate
    int time = 3; // 3 years

    // TODO: Call the calculateSimpleInterest function and print the result
    cout << "Simple Interest for principal $" << principal
         << ", rate " << rate << "%, for " << time << " years is $"
         << calculateSimpleInterest(principal, rate, time) << endl;

    return 0;
}
```

## Conclusion
- Functions are essential for organizing and modularizing code in C++.
- Understanding and applying function concepts enhances code efficiency and maintainability.
- This chapter covers the basics and advanced aspects of function usage in C++.



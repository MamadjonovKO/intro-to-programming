# Chapter 5: Loops

## Objectives
- Write programs that execute statements repeatedly using `while` loops.
- Follow the loop design strategy to develop loops.
- Control loops with user confirmation or sentinel values.
- Understand input redirection from a file rather than typing from the keyboard.
- Read all data from a file.
- Write loops using `do-while` and `for` statements.
- Understand the similarities and differences of three types of loop statements.
- Write nested loops.
- Learn techniques for minimizing numerical errors.
- Learn loops from a variety of examples (GCD, FutureTuition, MonteCarloSimulation, Dec2Hex).
- Implement program control with `break` and `continue`.
- Write programs to test palindromes and display prime numbers.

## 5.1 Introduction to Loops
- Loops allow for repeated execution of a block of statements.
- Example of using a loop to display a message multiple times.
- Introduction to `while`, `do-while`, and `for` loops.

```cpp
#include <iostream>
using namespace std;

int main() {
    // Example of using a while loop to display a message multiple times
    int count = 0;
    while (count < 5) {
        cout << "This is a message from the while loop." << endl;
        count++;
    }

    // Example of using a do-while loop to display a message multiple times
    count = 0;
    do {
        cout << "This is a message from the do-while loop." << endl;
        count++;
    } while (count < 5);

    // Example of using a for loop to display a message multiple times
    for (int i = 0; i < 5; i++) {
        cout << "This is a message from the for loop." << endl;
    }

    return 0;
}
```

- The while loop continues as long as count is less than 5.
- The do-while loop also performs the same task, but it guarantees that the loop body is executed at least once.
- The for loop succinctly combines initialization, condition checking, and incrementing in one line, making it very handy for situations where you know in advance how many times the loop should run.


## 5.2 The `while` Loop
- Executes statements repeatedly while the condition is true.
- Counter-controlled loops: Use a variable to count the number of executions.
- Common errors: Off-by-one errors and infinite loops.
- Real-world example: Subtraction quiz with loop.

### Subtraction Quiz Using a while Loop

```cpp
#include <iostream>
#include <cstdlib> // Required for rand()
#include <ctime>   // Required for time()
using namespace std;

int main() {
    // Initialize random seed
    srand(time(0));

    int numberOfQuestions = 5; // Number of questions in the quiz
    int correctCount = 0;      // Count of correct answers
    int count = 0;             // Counter for the loop
    int number1, number2, answer;

    while (count < numberOfQuestions) {
        // Generate two random single-digit numbers
        number1 = rand() % 10;
        number2 = rand() % 10;

        // Ensure number1 is greater than or equal to number2
        if (number1 < number2) {
            int temp = number1;
            number1 = number2;
            number2 = temp;
        }

        // Ask the user to solve the subtraction problem
        cout << "What is " << number1 << " - " << number2 << "? ";
        cin >> answer;

        // Grade the answer and increment the correct count if necessary
        if (number1 - number2 == answer) {
            cout << "Correct!" << endl;
            correctCount++;
        } else {
            cout << "Wrong. The correct answer is " << number1 - number2 << endl;
        }

        // Increment the question count
        count++;

        // Note: Common errors to avoid
        // 1. Off-by-one error: Ensure the loop runs the correct number of times.
        // 2. Infinite loop: Increment the counter variable to ensure loop termination.
    }

    cout << "You got " << correctCount << " out of " << numberOfQuestions << " correct." << endl;

    return 0;
}
```
- The while loop keeps running until count is less than numberOfQuestions.
- Two random numbers are generated for each quiz question.
- The user is prompted to solve a subtraction problem. If the answer is correct, correctCount is incremented.
- After each question, count is incremented to eventually break out of the loop.

This example demonstrates a counter-controlled while loop, a practical use case, and highlights common pitfalls like off-by-one errors and infinite loops that programmers should be cautious about.

## 5.3 The `do-while` Loop
- Executes the loop body first, then checks the condition.
- Suitable when the loop body must execute at least once.
- Example: User input validation.
### User Input Validation Using do-while Loop

```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    do {
        cout << "Enter a number between 1 and 10: ";
        cin >> number;

        // Check if the input is within the valid range
        if (number < 1 || number > 10) {
            cout << "Invalid number. Please try again." << endl;
        }
    } while (number < 1 || number > 10);

    cout << "You entered a valid number: " << number << endl;

    return 0;
}
```
- The do-while loop is used to prompt the user for a number.
- The user's input is checked to see if it falls within the valid range (1 to 10).
- If the input is invalid, a message is displayed, and the loop continues.
- The loop ensures that the prompt is displayed at least once, even if the first input is valid.
- Once a valid number is entered, the loop terminates, and the program acknowledges the valid input.

This example clearly demonstrates how the do-while loop is effective for situations where the loop body must be executed at least once, such as validating user input.

## 5.4 The `for` Loop
- Concise syntax, typically used for counter-controlled iteration.
- Example: Printing multiples of a number.
### Printing Multiples of a Number Using for Loop

```cpp
#include <iostream>
using namespace std;

int main() {
    int number, limit;

    cout << "Enter a number to find its multiples: ";
    cin >> number;

    cout << "Enter the limit for multiples: ";
    cin >> limit;

    cout << "Multiples of " << number << " up to " << limit << " are: ";
    for (int i = 1; i <= limit; ++i) {
        cout << number * i << " ";
    }

    return 0;
}
```
- The user is prompted to enter a number and a limit.
- The for loop is used to iterate from 1 to the specified limit.
- In each iteration, the loop prints the current multiple of the entered number.
- The loop control variable i serves as the counter, controlling the number of iterations and the value of each multiple.

This for loop example showcases its use in scenarios where you need a specific number of iterations, and each iteration follows a predictable pattern, like generating multiples of a number.

## 5.5 Which Loop to Use?
- `while` and `for` are pretest loops (check condition before execution).
- `do-while` is a posttest loop (executes at least once).
- Select loop type based on readability and problem requirements.

#### 1. `while` Loop (Pretest Loop)
- The while loop checks its condition before executing the loop body.
- Suitable for situations where you may not need to execute the loop at all, depending on the condition.

Example: Reading user input until a valid number is entered:
```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    cout << "Enter a positive number: ";
    cin >> number;

    while (number <= 0) {
        cout << "Invalid number. Please enter a positive number: ";
        cin >> number;
    }

    cout << "You entered: " << number << endl;
    return 0;
}
```

#### 2. `do-while` Loop (Posttest Loop)
- Executes the loop body first, then checks the condition.
- Ensures that the loop body is executed at least once.

Example: Menu-driven program where the menu is displayed at least once:
```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;
    do {
        cout << "1. Play Game\n";
        cout << "2. Load Game\n";
        cout << "3. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;
    } while (choice != 3);

    cout << "Exiting program..." << endl;
    return 0;
}
```

#### 3. `for` Loop (Pretest Loop)
- Concise and ideal for counter-controlled iteration.
- The number of iterations is usually known beforehand.

Example: Displaying a sequence of numbers:
```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 1; i <= 10; ++i) {
        cout << i << " ";
    }
    return 0;
}
```

## 5.6 Nested Loops
- A loop inside another loop.
- Commonly used for multi-dimensional data processing(arrays, matrices etc) or when generating patterns.

Example: Multiplication table using nested `for` loops:
```cpp
#include <iostream>
#include <iomanip>  // For formatted output using setw

using namespace std;

int main() {
    const int MAX = 10; // Define the size of the multiplication table

    // Print the header for the table
    cout << "    ";
    for (int i = 1; i <= MAX; i++) {
        cout << setw(4) << i;
    }
    cout << "\n----------------------------------------\n";

    // Outer loop for each row
    for (int row = 1; row <= MAX; row++) {
        cout << setw(4) << row << "|"; // Print row number

        // Inner loop for each column
        for (int col = 1; col <= MAX; col++) {
            cout << setw(4) << row * col; // Print the product
        }

        cout << endl; // Move to the next line after each row
    }

    return 0;
}
```
This code generates a 10x10 multiplication table. The outer loop handles the rows, and for each row, the inner loop computes and displays the products for that row.

When using nested loops, it's crucial to manage loop counters correctly to avoid errors, such as infinite loops or incorrect data processing. Each loop should have a distinct counter variable (row for the outer loop and col for the inner loop in the above example), and their scopes should not overlap unless intended for specific purposes.

## 5.7 Minimizing Numeric Errors
- Floating-point arithmetic can introduce errors in loops.
### Strategies to Minimize Numeric Errors in Loops
#### 1. Use Integer Counters
Instead of using floating-point numbers as loop counters or for incremental changes, use integers. Convert them to floating-point only when necessary. This approach reduces the accumulation of rounding errors.

Example: Summing a series of fractions (1/2, 1/3, 1/4, ..., 1/n):
```cpp
double sum = 0.0;
int n = 100; // Total number of terms

for (int i = 2; i <= n; i++) {
    sum += 1.0 / static_cast<double>(i); // Use integer counter 'i'
}

cout << "Sum of series is: " << sum << endl;
```
Here, i is an integer counter, and the division is performed with a floating-point number, minimizing the accumulation of errors.

#### 2. Avoid Subtracting Nearly Equal Numbers
When two nearly equal floating-point numbers are subtracted, significant digits can be lost, leading to a loss of precision. If possible, restructure calculations to avoid such scenarios.
#### 3. Sum Smaller Numbers First
When summing a series of floating-point numbers, start with the smallest values. This approach ensures that smaller numbers contribute to the total sum before they become insignificant relative to larger numbers.

Example: Summing an array of floating-point numbers:
```cpp
vector<double> numbers = {0.0003, 0.0004, 5.0, 3.0, 2.0}; // Example array
sort(numbers.begin(), numbers.end()); // Sort numbers to sum smallest first

double total = 0.0;
for (double num : numbers) {
    total += num;
}

cout << "Total sum is: " << total << endl;
```

#### 4. Use Higher Precision Data Types When Necessary
If precision is critical and the range of values is large, consider using data types with higher precision, such as long double in C++.
#### 5. Mathematically Reformulate the Problem
Sometimes, rethinking the problem and using a different mathematical approach can inherently reduce errors. For instance, using iterative methods that accumulate less error or transforming the problem to a more stable numerical method.

Remember, while these strategies help minimize errors, they cannot eliminate them entirely due to the inherent nature of floating-point arithmetic. The key is to be aware of potential issues and apply the best practices to keep the errors within acceptable limits.

## 5.8 Case Studies
- Practical applications and examples of loops:
    - Finding the Greatest Common Divisor (GCD)
```cpp
int gcd(int a, int b) {
  while (b != 0) {
      int temp = b;
      b = a % b;
      a = temp;
  }
  return a;
}
    
int main() {
  cout << "gcd(24, 16) = " << gcd(24, 16) << endl;
  cout << "gcd(255, 25) = " << gcd(255, 25) << endl;
  cout << "gcd(255, 100) = " << gcd(255, 100) << endl;
  return 0;
}
```

- Predicting future tuition with incremental percentage increase
```cpp
double predictTuition(double initialTuition, double rateIncrease, int years) {
    double tuition = initialTuition;
    for (int i = 1; i <= years; i++) {
        tuition *= (1 + rateIncrease / 100);
    }
    return tuition;
}

int main() {
    cout << "Tuition in 10 years: $" << predictTuition(10000, 5, 10) << endl;
    cout << "Tuition in 20 years: $" << predictTuition(10000, 5, 20) << endl;
    return 0;
}
```
- Monte Carlo Simulation for estimating values(Used for estimating mathematical quantities, such as estimating the value of π)
```cpp
sdouble monteCarloPi(int iterations) {
    int insideCircle = 0;
    for (int i = 0; i < iterations; i++) {
        double x = rand() / (double)RAND_MAX;
        double y = rand() / (double)RAND_MAX;
        if (x * x + y * y <= 1) insideCircle++;
    }
    return 4 * insideCircle / (double)iterations;
}

int main() {
    cout << "Estimate of pi: " << monteCarloPi(1000000) << endl;
    return 0;
}
```
- Converting decimal to hexadecimal
```cpp
string decimalToHex(int decimal) {
    string hex = "";
    while (decimal > 0) {
        int hexDigit = decimal % 16;
        char hexChar = (hexDigit < 10) ? ('0' + hexDigit) : ('A' + hexDigit - 10);
        hex = hexChar + hex;
        decimal /= 16;
    }
    return (hex.empty() ? "0" : hex);
}

int main() {
    cout << "decimalToHex(100) = " << decimalToHex(100) << endl;
    cout << "decimalToHex(255) = " << decimalToHex(255) << endl;
    cout << "decimalToHex(2500) = " << decimalToHex(2500) << endl;
    return 0;
}
```
These examples illustrate how loops can be effectively used in various practical scenarios, from mathematical calculations to data conversions.

## 5.9 Keywords `break` and `continue`
- `break`: Exits the nearest enclosing loop immediately.
  Example: Finding the First Positive Integer Divisible by 7
```cpp
int number = 1;

while (true) {
    if (number % 7 == 0) {
        cout << "The first positive integer divisible by 7 is: " << number << endl;
        break; // Exit the loop as the condition is met
    }
    number++;
}
```
- `continue`: Skips to the next iteration of the nearest enclosing loop.
  Example: Printing Odd Numbers Up to 10
```cpp
for (int i = 1; i <= 10; i++) {
    if (i % 2 == 0) {
        continue; // Skip the rest of the loop for even numbers
    }
    cout << i << " "; // This will execute only for odd numbers
}
// Expected Output: 1 3 5 7 9
```
#### Summary
- `break`: Exits a loop when a specific condition is met. In the example, it stops the search for the first number divisible by 7.
- `continue`: Skips the current iteration if certain conditions are true. For instance, it skips even numbers in the loop of numbers from 1 to 10.
- Using these keywords can simplify certain tasks but should be employed carefully to maintain code readability.

## 5.10 Checking Palindromes(exercise)
- Algorithm and code example to check if a string is a palindrome.
```cpp
#include <iostream>
#include <string>
using namespace std;

bool isPalindrome(const string& str) {
    // TODO: Implement the logic to check if 'str' is a palindrome.
    // Use two pointers approach - one starting from the beginning (low)
    // and the other from the end (high). Compare characters and move
    // pointers towards the middle. Return true if palindrome, false otherwise.

    return false; // Placeholder return, to be modified by students
}

int main() {
    string input;
    cout << "Enter a string to check if it's a palindrome: ";
    getline(cin, input);

    if (isPalindrome(input)) {
        cout << "\"" << input << "\" is a palindrome." << endl;
    } else {
        cout << "\"" << input << "\" is not a palindrome." << endl;
    }

    return 0;
}
```

## 5.11 Displaying Prime Numbers(exercise)
- Program to display the first 50 prime numbers.
- Demonstrates the use of nested loops and prime number checking logic.
```cpp
#include <iostream>
using namespace std;

// Function to check if a number is prime
bool isPrime(int number) {
    // TODO: Implement the logic to check if 'number' is a prime number.
    // Use a loop to check if 'number' is divisible by any number less than itself.
    // Return true if prime, false otherwise.

    return false; // Placeholder return, to be modified by students
}

int main() {
    const int NUM_PRIMES = 50; // Number of prime numbers to display
    int count = 0; // Count of prime numbers found
    int number = 2; // Starting number for checking primes

    cout << "The first " << NUM_PRIMES << " prime numbers are:" << endl;

    // TODO: Implement a loop to find and display the first 50 prime numbers.
    // Use the isPrime function within this loop to check if a number is prime.
    // Display each prime number and increment the count.
    // You may use nested loops if required.

    return 0;
}
```

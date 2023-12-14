# Chapter 7: Single-Dimensional Arrays and C-Strings
## Objectives
- Understand why arrays are necessary in programming.
- Learn to declare, initialize, and access single-dimensional arrays.
- Implement common array operations such as display, summing elements, finding min/max, random shuffling, and shifting elements.
- Apply arrays in application development through examples like LottoNumbers and DeckOfCards.
- Define and invoke functions with array arguments.
- Use const to define non-modifiable array parameters.
- Learn about returning arrays from functions.
- Count occurrences of letters in an array of characters (CountLettersInArray).
- Explore linear and binary search algorithms.
- Understand and implement selection sort.
- Learn about C-strings and their functions.

#

## 7.1 Introduction to Single-Dimensional Arrays
- An array is a collection of data items of the same type.
- Each data item is called an element.
- Elements are accessed by their position, or index.
- Arrays are useful for storing data items that are related.
- Efficient for managing large collections of data.

Example: Storing and analyzing 100 numbers:
```cpp
#include <iostream>
using namespace std;

int main() {
    const int NUMBER_OF_ELEMENTS = 100;
    double numbers[NUMBER_OF_ELEMENTS];
    double sum = 0;

    for (int i = 0; i < NUMBER_OF_ELEMENTS; i++) {
        cout << "Enter a new number: ";
        cin >> numbers[i];
        sum += numbers[i];
    }

    double average = sum / NUMBER_OF_ELEMENTS;
    int count = 0;
    for (int i = 0; i < NUMBER_OF_ELEMENTS; i++)
        if (numbers[i] > average)
            count++;

    cout << "Average is " << average << endl;
    cout << "Number of elements above the average: " << count << endl;

    return 0;
}
```

#


## 7.2 Array Basics
Declare arrays with a specified type and size.
```cpp
int main() {
    int numbers[5];
    double values[100];
    char characters[200];
    return 0;
}
```
Access array elements using indexes (0-based).
```cpp
int main() {
    int numbers[5];
    numbers[0] = 1;
    numbers[1] = 2;
    numbers[2] = 3;
    numbers[3] = 4;
    numbers[4] = 5;
    return 0;
}
```
Initialize arrays with initial values.
```cpp
int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    return 0;
}
```

### Common Operations on Arrays
- Initializing with Input Values: Fill arrays with user input.
```cpp
int main() {
    int numbers[5];
    for (int i = 0; i < 5; i++) {
        cout << "Enter a new number: ";
        cin >> numbers[i];
    }
    return 0;
}
```
- Summing Elements: Calculate the total of array elements.
```cpp
int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    int sum = 0;
    for (int i = 0; i < 5; i++)
        sum += numbers[i];
    return 0;
}
```

- Finding the Minimum/Maximum: Find the minimum/maximum value in an array.
```cpp
int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    int min = numbers[0];
    for (int i = 1; i < 5; i++)
        if (numbers[i] < min)
            min = numbers[i];
    return 0;
}
```

- Random Shuffling: Randomly shuffle the elements in an array.
```cpp
int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    srand(time(0));
    for (int i = 0; i < 5; i++) {
        int index = rand() % 5;
        int temp = numbers[i];
        numbers[i] = numbers[index];
        numbers[index] = temp;
    }
    return 0;
}
```

- Displaying Arrays: Output array contents.
```cpp
int main() {
    int numbers[5] = {1, 2, 3, 4, 5};
    for (int i = 0; i < 5; i++)
        cout << numbers[i] << " ";
    return 0;
}
```

### Array Errors and Tips
- Array indexes must be integers.
- Array indexes must be in the range 0 to size - 1.
- Array indexes can be variables.
- Avoid out-of-bounds errors: Ensure indexes are within array size.
- Initialize arrays properly to prevent unpredictable behavior.


#


## 7.3 Practical Applications with Arrays
### LottoNumbers and DeckOfCards Examples
- LottoNumbers: Generate random numbers for a lottery.
```cpp
int main() {
    const int SIZE = 10;
    int numbers[SIZE];
    srand(time(0));
    for (int i = 0; i < SIZE; i++)
        numbers[i] = rand() % 100;
    return 0;
}
```
- DeckOfCards: Shuffle and deal a deck of cards.
```cpp
int main() {
    const int NUMBER_OF_CARDS = 52;
    int deck[NUMBER_OF_CARDS];
    srand(time(0));
    for (int i = 0; i < NUMBER_OF_CARDS; i++)
        deck[i] = i;
    for (int i = 0; i < NUMBER_OF_CARDS; i++) {
        int index = rand() % NUMBER_OF_CARDS;
        int temp = deck[i];
        deck[i] = deck[index];
        deck[index] = temp;
    }
    return 0;
}
```

#


## 7.4 Passing Arrays to Functions
- Arrays are passed to functions by reference.
- Arrays are not copied when passed to functions.
- Array size is not passed to functions.
- Array size must be passed to functions as a separate parameter.

Example: Passing an array to a function.
```cpp
void printArray(int list[], int size) {
    for (int i = 0; i < size; i++)
        cout << list[i] << " ";
}

int main() {
    const int SIZE = 5;
    int list[SIZE] = {1, 2, 3, 4, 5};
    printArray(list, SIZE);
    return 0;
}
```

#

## 7.5 Searching Arrays
### Linear Search
- Linear search is a simple search algorithm.
- It sequentially searches for a target value in an array.
- It returns the index of the target value if found, or -1 if not found.

Example: Linear search.
```cpp
int linearSearch(const int list[], int key, int arraySize) {
    for (int i = 0; i < arraySize; i++)
        if (key == list[i])
            return i;
    return -1;
}

int main() {
    const int SIZE = 5;
    int list[SIZE] = {1, 2, 3, 4, 5};
    cout << linearSearch(list, 3, SIZE);
    return 0;
}
```

#

## 7.6 C-Strings
- C-strings are character arrays that are terminated by a null character '\0'.
- C-strings are used to represent strings in C++.
- C-strings are stored in contiguous memory locations.
- C-strings are passed to functions by reference.
- C-strings are not copied when passed to functions.
- C-strings are not bounds-checked by the compiler.

Example: Declaring and initializing C-strings.
```cpp
int main() {
    char city[6] = {'P', 'a', 'r', 'i', 's', '\0'};
    char city[6] = {'P', 'a', 'r', 'i', 's'};
    char city[] = {'P', 'a', 'r', 'i', 's', '\0'};
    char city[] = {'P', 'a', 'r', 'i', 's'};
    char city[] = "Paris";
    return 0;
}
```

#

## 7.7 Case Studies
### CountLettersInArray
- Count the occurrences of each letter in an array of characters.
```cpp
int main() {
    const int SIZE = 100;
    char chars[SIZE];
    cout << "Enter the characters: ";
    cin.getline(chars, SIZE);
    int counts[26];
    for (int i = 0; i < 26; i++)
        counts[i] = 0;
    for (int i = 0; chars[i] != '\0'; i++)
        if (isalpha(chars[i]))
            counts[toupper(chars[i]) - 'A']++;
    for (int i = 0; i < 26; i++)
        if (counts[i] != 0)
            cout << (char)('A' + i) << " appears " << counts[i] << ((counts[i] == 1) ? " time" : " times") << endl;
    return 0;
}
```

### Checking Palindromes (Exercise)
Implement a function to check if a C-string is a palindrome.

### CountLettersInArray (Exercise)
Count the occurrences of each letter in a text.

#

## Conclusion
- Arrays and C-strings are foundational in C++ programming.
- Understanding these concepts is crucial for effective data handling and manipulation.





# Introduction to algorithms and data structures

### Objectives

1. Understand - algorithms and abstract data types (ADT)
2. Explain how asymptotic notation quantifies the performance of algorithms
3. Recursive methods/functions - How are they executes in a computer program.
4. Analyze complex code containing simple conditional, iterative, and recursive statements.

---

## 1. Understand - algorithms an abstract data types

### What is an algorithm?

A set of instructions designed to perform a task or solve a problem.
Think of **Recipe**: cook a dish step-by-step. Algorithm tells computer step-by-step
Ex: find max number in a list

1. make first num = max
2. iterate & compare with next elements in list
3. if next num == larger, update the max
4. continue checking entire list
5. return max num

**Pseudo Code:**
`function findMax(list):
    max = List[0] // Assume first element is max
    for each element in list:
      if element is greater than max:
        update the max
      return max`

### What is an ADT?

Defines a data structure by the operations it supports and the rules governing these operations, but not how these operations are implemented.
Ex: a bag of tennis balls, a stack of plates = LIFO stack ADT - operations: push(x) ~ adds element x to top of stack
pop() ~ removes and returns op element from stack
isEmpty() ~ check if stack is empty, bool
waiting in line = FIFO queue ADT

**Pseudo Code for Stack**
`class Stack:
    initialize:
      stack = []
    function push(x):
      stack.append(x)
    function pop():
      if not isEmpty():
        stack.remove()
      else:
        throw "Stack is empty"
    function isEmpty():
      return length of stack == 0
`

## Asymptotic notation and Algorithm performance

### Understand [Big-O notation](https://www.bigocheatsheet.com)

Simplest definition for Big Oh notation =

**Big Oh notation is a relative representation of the complexity of an algorithm**

Key words:

- Relative ~ compare apples to apples. Arithmetic multiplication algorithm != integer sorting algorithm. But comparing two algos that do arithmetic operations (multiplication and other addition) is valid and will tell you something meaningful.
- Representation ~ Big O reduces the comparisons between algos to a single variable. Var is chosen based on observations/assumptions.
  Ex: sorting algorithms are compared based on comparison operations(comparing nodes to determine relative ordering). What if the comparison is cheap but swapping is expensive? Comparison changes.
- Complexity ~ 1 sec to sort 10k elements, how long does it take to sort 1 mil. Complexity in this instance is a relative measure to something else.

Basic arithmetic teaches us: add, sub, multiplication, and div.
THESE are OPERATIONS. Method of solving THESE is an ALGORITHM.
Algorithm for addition: line the numbers up to the right and add digits in column writing the last number of that addition in the result. The 'tens' part of the algorithm is carried over to the next column.
input = two 100 digit numbers
algorithm complexity = 100 additions
input = two 10k digit numbers
algorithm complexity = 10k additions
The **complexity** (being the num of operations) is directly proportional to the number of digits n in the larger number.
O(n) or linear complexity

Subtraction is similar except you may need to borrow instead of carry.

Algorithm for multiplication: line the numbers up, multiply the first bottom digit against each digit in the top number.
input = two 6 digit numbers
algorithm complexity in operations = 36 multiplications and may need 10-11 column adds
input = two 100 digit numbers
algorithm complexity = 10k multiplications and 200 column adds.
input = two 1 million digit numbers
algorithm complexity = 1 trillion (10^12) and two million adds
The **complexity**, as the algorithm scales with n-squared, is O(n^2) or quadratic complexity. We **ONLY CARE** about the most significant portion of complexity.
The algorithm can be expressed as n^2 + 2n but the second term becomes insignificant the larger the input size (see our two 1 mil digits the 2n accounts for 0.0002%)

Big Oh Notation is about the Worst-case scenario of an algorithm.
Focus on growth rate of runtime and space complexity requirements as the input size increases.
Provides a way to describe the efficiency of an algorithm; how does it scale with larger input sizes?

### Common Big-O notations:

1. O(1): Constant Time ~ The runtime does not change regardless of input size.
   Ex: Accessing elements in an array
   1 item = 1 operations
   100 items = 1 operations
2. O(n): Linear Time ~ The runtime grows linearly with input size.
   Ex: Iterating through a list of size n, num of items scales by a factor of 10? O(n)'s scaling factor is 10.
   1 item = 1 operations
   100 items = 100 operations
3. O(n^2): Quadratic Time ~ The runtime grow quadratically with the input size.
   Ex: A nested loop that processes pairs of elements
   1 item = 1 operations
   10 items = 100 operations
   100 items = 10k operations
4. O(log n): Logarithmic Time ~ The runtime is divided and conquered.
   Ex: Binary Search
   1 item = 1 operations
   10 items = 2 operations
   100 items = 3 operations
   1000 items = 4 operations
5. O(n!): Factorial/Combinatorial Time ~ The runtime grows
   Ex: Traveling Salesman - if you have 3 towns and want to find the shortest tour that visits each town, A,B,C, with roads between pairs:
   A -> B -> C | A -> C -> B | B -> C -> A There could be 6 paths but some paths use the same roads just in reverse.
   But if you wanted to tour 4 towns, this becomes 12 possibilities. With 5 its 60. 6 becomes 360.
   5! = 5 x 4 x 3 x 2 x 1 = 120
   6! = 6 x 5 x 4 x 3 x 2 x 1 = 360

### Polynomial Time

Any algorithm that has a complexity of O(n^a) is said to have polynomial complexity or is solvable in polynomial time.
O(n), O(n^2) etc. are all polynomial time. Some problems cannot be solved in this time. Certain things, like [Public Key Cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography), are used in the world because of this. It is computationally hard to find two prime factors of a very large number. If it wasn't, we couldn't use the public key systems we use.

Example: Summing all elements in a list
**Pseudo Code**
`function sumList(list):
  total = 0 
  for each element in list:
    total = total + element
    end
  return total
  end`
Time Complexity: O(n), the runtime grows linearly with the number of elements in the list(n)

### Identify Algorithm Complexity

To determine an algorithm's time complexity:

1. Identify Basic operations: Affect runtime i.e; loops and recursive calls
2. Count operations: Determine if number of operations increases with input size.
3. Express in Big-O: Simplify the growth rate to the most significant term. Ex: if runtime grows as 3n^2 +5n -> O(n^2)

---

## Understand Recursion

### What is recursion?

When a function calls itself to solve smaller parts o a problem.
Typically has steps:

1. Base case: condition where calls to function stop
2. Recursive case: function calls itself with modified arguments

Example: Calculating (n!) factorial
**Pseudo Code**
`function factorial(n):
    if n == 0:
      return 1    // base case: factorial of 0 is 1
    else:
      return n * factorial(n - 1)
`
Execution: init call ~ factorial(5) calls factorial(4)
recursive call ~ each call makes further recursive calls until reaching...
base case ~ when n is 0, recursion stops, values start returning

### How recursive methods are executed

When recursive function is called:

1. The function's state(vars and curr pos) is saved on the call stack.
2. Call creates new stack frame
3. Base case hit? function call returns result, stack frames removed

## Analyzing Complexity of Code Snippets

Algorithm complexity = Measurement of an algorithm's performance in terms of time and space as the input size increases.
While abstracting specific hardware and implementation details, the goal is to estimate the run time with larger inputs.

Key concepts:

1. Basic operations ~ Identify the fundamental operations that the algorithm performs repeatedly. These determine time.
2. Counting operations ~ How many times are basic operations executed as input size increases.

[source1](https://stackoverflow.com/questions/487258/what-is-a-plain-english-explanation-of-big-o-notation)

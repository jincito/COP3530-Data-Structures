# Introduction to algorithms ad data structures

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

### Understand Big-O notation

Focus on growth rate of runtime and space complexity requirements as the input size increases.
Provides a way to describe the efficiency of an algorithm; how does it scale with larger input sizes?

Common Big-O notations:

1. O(1): Constant Time ~ The runtime does not change regardless of input size.
   Ex: Accessing elements in an array
2. O(n): Linear Time ~ The runtime grows linearly with input size.
   Ex: Iterating through a list of size n
3. O(n^2): Quadratic Time ~ The runtime grow quadratically with the input size.
   Ex: A nested loop that processes pairs of elements

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

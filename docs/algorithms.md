# An Introduction to Algorithms

## Introduction

In my previous talk, I gave an general overview and introduction to the basic
Data Structures that every Software Engineer should be familiar with. These
included the classic data structures like Arrays, Linked Lists, Records, Hash
Tables, Graphs, Stacks, Queues, and Trees. By investigating the essential
features of these Data Structures, we hopefully have gained a further
understanding and appreciation for the way raw Data is organized and formalized
for processing of a Computer Program.

As mentioned in the Conclusion of that talk, I indicated that these Data
Structures, while essential to understanding how Data is interpreted by Computer
Programs, is only one part of writing efficient Software Architecture. While
technically there are many different practices and paradigms to writing
efficient Software Architecture such as Software Design Patterns and Software
Design Principles, the focus of today's follow up talk on Data Structures will
focus more on the complementary subject of Algorithms.

### What Is An Algorithm?

An Algorithm is nothing more or less than a procedure, commonly used within the
fields of Mathematics and Computer Science, which establishes a finite set of
mathematically rigorous instructions to solve a specific problem or perform a
computation. An Algorithm establishes a specification or set of speficiations
for performing calculations and also to process data. Unlike Heuristics,
Algorithms are fully specified and can guarantee correct or optimal results
through established Analytical processes, otherwise known as Analysis of
Algorithms. In a historical context, Algorithms originated as a series of
recorded step-by-step procedures for solving mathematical problems. Evidence of
the earliest use of Algorithms can be found in records left by the ancient
Babylonians.

### Use Of Algorithms In Modern Software Development

The use of Algorithms in Software Development is predominant, even if we as
Computer Users or even beginner Software Engineers are unaware of them. Modern
day Digital Computers as tools are a natural extension of mankind's desire to
calculate and express mathematical abstractions in a way that is efficiently
calculated and provides some real world value to the end user based off of
passed parameters, and expected results.

Modern day Computer Programmers and Software Developers utilize Algirithms in
conjunction with Data Structures in order to efficiently compute a particular
calculation or solve a particular problem. Unlike Data Structures, Algorithms
are not classified based off the particular organization of Data, but rather
through differentiating strategies that are most suited to the arriving at the
desired solution to a problem or calculation. Examples of these strategies
include:

- By Implementation
- By Design
- By Optimization

With this in mind, however, coding and interview preparation platforms such as
LeetCode will often organize their various coding puzzles/problems into
categories based off of Data Structures, but it is important to note that this
is not a traditional way of categorizing Algorithms, and oftentimes thinking
about Algorithmic problems in accordance with one of the three aforementioned
strategies helps to facilitate a more Programmatic way of thinking about given
problems.

### Two Sum: The "Hello World!" Of Algorithms

While many might contest that the more elementary
[FizzBuzz](https://en.wikipedia.org/w/index.php?title=Fizz_buzz) puzzle is the
true "Hello World!" of Algorithms, I'd argue that this problem is far too simple
in scope to get a good idea of how Algorithms might play a role in Software
Development, as FizzBuzz is ultimately closer to a basic math problem than a
rigorous mathematical computation. That said, Two Sum is not too complicated and
is a good introduction to how Algorithms can still solve a problem, but be
inefficient, as well as how a simple change in thinking on the problem can solve
said problem in a far more efficient pattern.

Here is the Two Sum problem as presented on LeetCode:

```md
1. Two Sum Easy Topics Companies Hint

Given an array of integers nums and an integer target, return indices of the two
numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not
use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9 Output: [0,1] Explanation: Because
nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6 Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6 Output: [0,1]

Constraints:

    2 <= nums.length <= 104
    -109 <= nums[i] <= 109
    -109 <= target <= 109
    Only one valid answer exists.
```

**The Naive Approach:**

Let's take the time to solve this problem naively. As a general rule of thumb
when approaching an Algorithmic problem is to try your best not to overthink it.
That said, look at the problem, try to solve it without code at first
(oftentimes on a whiteboard or a small notebook) so that you visualize the logic
and data before expressing it in code.

To clarify, this problem is asking us to develop a function and/or method that
can take <em>any</em> array and <em>any</em> target number, and find the indices
within the given array that, when taking the numbers that exist at those
indices, will add up to the target number.

Let's take their first example and utilize that to think through our first pass
of the solution:

```md
Input: nums = [2, 7, 11, 15], target = 9
```

At first glance we can see that to get to nine, we would have to add 2 and 7,
giving us the indices, 0, and 1. But how do we express that to a computer
program?

Well we could take the target 9 and then subtract it from each element in the
array. Then we could check to see if that result number exists within the
<em>remaining</em> elements of the array. If it does, then we could return those
two numbers. This means we'll have to loop through the array twice for each
number in the array, like so:

```js
const twoSum = (nums, target) => {
  let result = [];

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === complement) {
        result = [i, j];
        return result;
      }
    }
  }

  return result;
};

let nums = [2, 7, 11, 15];
let target = 9;
console.log(`twoSum([${nums}], ${target}) :=>`, twoSum(nums, target));
// Returns:
// twoSum([2,7,11,15], 9) :=> [ 0, 1 ]
```

This gives us our result correctly. A naive beginner programmer would look at
this solution, slap his hands together and call it a night, but anyone who has
written a program that has to iterate over a substantially large array knows
that this solution is probably not ideal. We are iterating over each element in
our array, and then iterating again for every remaining element in the array we
have not checked. This is what is known as a "nested for loop", and we are
implementing what is known as a "Brute Force Solution", in which we check every
element in our data set and pass it through a conditional to find out if it
passes the condition or not.

So how can we optimize this? Well this is where familiarity with one of our Data
Structures can help us. We have already established the use of an array here,
the most basic of Data Structures. How can we keep track of which elements we've
visited without having to loop over every other element in the array
<em>again</em>? In other words, how can we pass over each element in the array
<em>only once</em>?

This is where familiarity with our Data Structures is going to help us
immensely. If the answer is not apparent to you, don't worry about it. It would
not apparent to me either had I not solved this problem multiple times in the
past. That said, the indication that we need to keep some <em>record</em> of our
previously visited elements in the array should give you an inclination as to
which data structure to use.

**A More Efficient Solution:**

As I hinted earlier, using a Record Data Structure can help us understand how we
might more efficiently solve this problem. If you recall from our previous talk
on Data Structures, a Record is simply a series of key/value pairs that
establisha relationship between a defined property name and it's corresponding
value or method.

Let's think logically how this data structure might help us in the context of
this problem. Let's first establish a JavaScript Map structure at the beginning
of our new solution:

```js
const twoSum = (nums, target) => {
  const numMap = new Map();
  //...
};
```

The Map data structure is an underutilized Data Structure in JavaScript that can
be used almost interchangably with an JavaScript Object, but has a multitude of
benefits over Object such as more performant iterability. That said, for the
purposes of this exercise, you can think of it more as a standard JavaScript
Object or Python Dictionary.

We have now established a `numMap` Record to hold onto all previously indexes
and their corresponding values! To reiterate, this means we can record all
previously visited indexes and numbers:

```js
const twoSum = (nums, target) => {
  const numMap = new Map();
  for (let i = 0; i < nums.length; i++) {
    // Sets the nums Array value as the numMap index,
    // and the index of the num Array as the numMap Value
    numMap.set(nums[i], i);
  }
  return numMap;
};

let nums = [2, 7, 11, 15];
let target = 9;

console.log(`twoSum([${nums}], ${target}) :=>`, twoSum(nums, target));
```

If we run the above, the numMap will simply be populated with the indexes and
values within the array, with the values being the keys, and the indices being
the values of the `numMap`:

```js
// Returns:
twoSum([2,7,11,15], 9) => Map(4) { '2' => 0, '7' => 1, '11' => 2, '15' => 3 }
```

But think on this, we now have a record of all previously visited elements in
the array, as well as their indices. This means that as we iterate through the
array, we can check if the corresponding complement already exists within the
Map, and if that exists, we can then return the current index of the array we
are at, as well as the index returned from the Map. Let's complete this more
efficient algorithm to demonstrate:

```js
const twoSum = (nums, target) => {
  const numMap = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    if (numMap.has(complement)) {
      return [numMap.get(complement), i];
    }

    // Sets the nums Array value as the numMap index,
    // and the index of the num Array as the numMap Value
    numMap.set(nums[i], i);
  }

  return [];
};
```

Instead of simply setting the index and the value of the `nums` array in the
`numMap`, we first check to see if the `numMap` already has the complement in
it. If it does, then we have found the complement to the number we are currently
visiting. Thusly we simply return the value that lives at the complement key
within the Map, which if you recall correctly is the index visited. Again, for
reiteration to be absolutely clear, our Map, has keys that represent the values
found at the `nums[i]` on each iteration, and the value stored at it represents
the index itself `i`:

```js
// map key => map value, map key => map value, map key => map value, map key => map value
//  array value => array index,  array value => array index, array value => array index, array value => array index
Map(4) { '2' => 0, '7' => 1, '11' => 2, '15' => 3 }
```

So why go through all of this? Didn't our first solution work well enough? Well
not exactly, let's scale this up considerably...and time each solution to see
what problems might arise:

```js
// Brute Force Solution
const twoSumBruteForce = (nums, target) => {
  let result = [];

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === complement) {
        result = [i, j];
        return result;
      }
    }
  }

  return result;
};

// Hash Map Solution
const twoSumHashMap = (nums, target) => {
  const numMap = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    if (numMap.has(complement)) {
      return [numMap.get(complement), i];
    }

    numMap.set(nums[i], i);
  }

  return [];
};

// Generate a large array
const generateLargeArray = (size) => {
  return Array.from({ length: size }, () => Math.floor(Math.random() * size));
};

// Example array size
const arraySize = 1000000; // Make an array with 1 million elements
const nums = generateLargeArray(arraySize);

// Set target to be the sum of the last two elements
const target = nums[arraySize - 1] + nums[arraySize - 2];

// Time the Brute Force solution
console.time("Brute Force Time");
twoSumBruteForce(nums, target);
console.timeEnd("Brute Force Time");

// Time the Hash Map solution
console.time("Hash Map Time");
twoSumHashMap(nums, target);
console.timeEnd("Hash Map Time");
```

If we run this program using NodeJS, we get an output with approximately these
results:

```
Brute Force Time: 6.836ms
Hash Map Time: 0.693ms
```

Note that the times on this can vary somewhat, but at 1_000_000 elements in our
array, and with always having our target be found <em>at the very end of the
array</em>, we will always find the target in the <em>Worst Case Scenario</em>.
Note that our Brute Force Solution takes roughly <em>ten times</em> more time to
execute and find the solution than our Hash Map Solution. And this only gets
worse the larger the data set becomes, the disparity between these two solutions
only grows larger, the larger the data set becomes.

Hopefully this simple demonstration gives you an idea of how thinking
programatically can affect the efficiency, or lack thereof, of a Software
Product. The affect of Software Developer's implementations of algorithms
ultimately affects the use of time, money, and resources. In other words, the
way we as software developers implement algorithms affects <em>real world
metrics</em> that have <em>real world consequences</em>! Let's now analyze our
two different solutions using different metrics to see what these consequences,
might be.

### Analysis of Algorithms

Let's leverage one of Node's native tools to see other metrics about our
solutions:

```js
// Brute Force Solution
const twoSumBruteForce = (nums, target) => {
  let result = [];
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === complement) {
        result = [i, j];
        return result;
      }
    }
  }

  return [];
};

// Hash Map Solution
const twoSumHashMap = (nums, target) => {
  const numMap = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    if (numMap.has(complement)) {
      return [numMap.get(complement), i];
    }

    numMap.set(nums[i], i);
  }

  return [];
};

// Generate a large array
const generateLargeArray = (size) => {
  return Array.from({ length: size }, () => Math.floor(Math.random() * size));
};

// Example array size
const arraySize = 1000000; // 1_000_000 elements in the array
const nums = generateLargeArray(arraySize);
const target = nums[arraySize - 1] + nums[arraySize - 2]; // Target is the sum of the last two elements

// Function to measure performance
const measurePerformance = (func, nums, target) => {
  const initialMemoryUsage = process.memoryUsage();
  const initialCpuUsage = process.cpuUsage();

  console.time("Execution Time");
  const result = func(nums, target);
  console.timeEnd("Execution Time");

  const finalMemoryUsage = process.memoryUsage();
  const finalCpuUsage = process.cpuUsage(initialCpuUsage);
  console.log("Result:", result);
  console.log("Memory Usage:");
  console.log(`RSS: ${finalMemoryUsage.rss - initialMemoryUsage.rss} bytes`);
  console.log(
    `Heap Total: ${
      finalMemoryUsage.heapTotal - initialMemoryUsage.heapTotal
    } bytes`,
  );
  console.log(
    `Heap Used: ${
      finalMemoryUsage.heapUsed - initialMemoryUsage.heapUsed
    } bytes`,
  );
  console.log("CPU Usage:");
  console.log(`User CPU Time: ${finalCpuUsage.user / 1000} ms`);
  console.log(`System CPU Time: ${finalCpuUsage.system / 1000} ms`);
};

// Measure performance of Brute Force
console.log("Brute Force Performance:");
measurePerformance(twoSumBruteForce, nums, target);

console.log("------------------------");

// Measure performance of Hash Map
console.log("Hash Map Performance:");
measurePerformance(twoSumHashMap, nums, target);
```

I won't go into here the various aspects of how we're leveraging the native
tools available in NodeJS which allow us to monitor these processes, but instead
let's focus more on the results:

```
Brute Force Performance:
Execution Time: 4.867ms
Result: [ 1, 317449 ]
Memory Usage:
RSS: 262144 bytes
Heap Total: 262144 bytes
Heap Used: 27080 bytes
CPU Usage:
User CPU Time: 7.4 ms
System CPU Time: 1.038 ms
------------------------
Hash Map Performance:
Execution Time: 0.258ms
Result: [ 1149, 3105 ]
Memory Usage:
RSS: 0 bytes
Heap Total: 0 bytes
Heap Used: 157208 bytes
CPU Usage:
User CPU Time: 0.35 ms
System CPU Time: 0 ms
```

As per expected after taking a look at our results from the previous section,
the Execution Time is significatnly more for the Brute Force Solution. Of
interest, however, is when we monitor the total amount of RAM utilized reflected
in how much memory was allocated to the Heap throughout the lifecycle of each
solution.

Our more Time Efficient Solution, The Hash Map Soltuion, consumes more RAM
because it utilizes the Record Data Structure, which if you recall from our
previous talk does not allocate memory in a contiguous set of memory addresses
like an Array does.

Because of this, through for loop iteration, when we check the contents of our
Map, the CPU must check the registry of the RAM by reference (see
[Pointers](https://en.wikipedia.org/wiki/Pointer_(computer_programming))),
rather than the way it does with our Brute Force Solution, which simply checks
the next memory address because it utilizes the Array data structure. So
ultimately, our Hash Map Solution is actually less efficient if you're talking
purely in the realm of utilizing RAM. This is what is known as Space Efficiency
in Analysis of Algorithms. Let's break down each metric further:

```
Brute Force Performance:
Memory Usage:
RSS: 262144 bytes
Heap Total: 262144 bytes
Heap Used: 27080 bytes
CPU Usage:
User CPU Time: 7.4 ms
System CPU Time: 1.038 ms
------------------------
Hash Map Performance:
Memory Usage:
RSS: 262144 bytes
Heap Total: 237568 bytes
Heap Used: 157208 bytes
Usage:
User CPU Time: 0.35 ms
System CPU Time: 0 ms
```

The RSS field refers to the Resident Set Size and is used to show how much
memory(RAM) is allocated to that process at the time of initialization.

Note that, in this case, our Brute Force Performance allocates 262_144 bytes for
use throughout the lifecycle of our program execution. This is the amount of
memory needed to account for the updating of our counting variable `i`, as well
as to hold onto the memory addresses of each element in our `nums` array, as
well as redeclaring the value of `complement`. By the end of the program
execution, the amount of memory used is 27_080 bytes, which reflects the amount
of memory cleaned up by the NodeJS garbage collector.

Notice that the amount of memory utilized by the Hash Map Solution is higher
than our Brute Force Solution. This is because our `numMap` had to continually
be resized as we iterated through our array and checked it against each key in
our `numMap`, ultimately requiring NodeJS to continually reassign values within
the `numMap` array every time it needed to add a new key/value pair to our
`numMap`.

This continually occurs until our `if` condition returns true(i.e. we found our
`target`), or we reached the end of the `nums` array. In the end we took up more
space in RAM. In fact, if we scale up our `nums` array to include 10_000_000
elements, we can see that the amount of RAM used scales upwards with these
elements in our Hash Map Solution, but not with our Brute Force Solution:

```
// With 10_000_000 elements in the nums array:
Brute Force Performance:
Memory Usage:
RSS: 262144 bytes
Heap Total: 262144 bytes
Heap Used: 22496 bytes
CPU Usage:
User CPU Time: 9.393 ms
System CPU Time: 0.001 ms
-------------------------
Hash Map Performance:
Memory Usage:
RSS: 262144 bytes
Heap Total: 237568 bytes
Heap Used: 468072 bytes
CPU Usage:
User CPU Time: 0.238 ms
System CPU Time: 0.965 ms
```

Again, this new output shows us that our Hash Map Solution is actually somewhat
inefficient on terms of taking up more RAM. In other words, our Hash Map
Solution takes up more <em>Space</em>. That said, ultimately our Hash Map
Solution is also much <em>faster</em>. In other words, our Hash Map Solution
also takes up far less <em>Time</em>. Time and Space are the name of the
Analysis of Algorithms Game, it is ultimately the two metrics by which all
Algorithms are analyzed and judged for whether or not they are a better or worse
solution to a particular problem.

You can always add more computational power to a problem, either in more CPU
power and RAM space. This solution manifests in the form of a bigger badder
Server or simply More Servers. But that ultimately costs more money in the long
run, as it also requires more power to run and maintain those costly servers. If
you invest the time and thought up front to creating more efficient solutions to
your problems, you ultimately save time and money for everyone from the user to
the product manager.

All this talk of RAM and CPU cycles can get a bit clunky at times though, don't
you think? Maybe when talking to our System Administrators or our Product
Managers, we'll need to go into such details, but what about when discussing
these problems with other <em>Programmers</em>?

We'll need to be able to express how our program is or is not time/space
efficient. We'll need a way to talk about our programs in generalities that get
across the idea quickly in a way that other programmers will immediately
understand. For that, we'll need to know how to express Time and Space
Complexity in Big O Notation.

### Big O Notation

Big O notation, also known as asymptotic notation, is a mathematical notation
that describes the limiting behavior of a function when the argument tends
towards a particular value or infinity. The letter O was chosen by Big O's
inventor, Paul Bauchmann, for standing for the German word "Ordnung", meaning
"order of approximation".

In the realm of computer science, big O notation is used to classify algorithms
according to how their run time or space requirements grow as the input size
grows. While there are several other related notations to big O, ultimately big
O is the most commonly utilized mathematical notation when approximating the
Time and Space Complexity of Algorithms within the Software Development and
Software Engineering Ecosystems.

So what does this big O notation look like? Let's take a look at a few examples:

$$ O(1) $$

This is $O(1)$. Pronounced as "O of one". In terms of Time complexity, this
notation is analogous to meaning "instant". I was able to reference and retrieve
this data in exactly 1 iteration. In terms of space complexity, this means it
took up exactly 1 order of magnitude in RAM. In the programming language C, for
example, we learn that when we assign an integer to a variable:

```c
int c = 1;
```

That integer takes up exactly 32 bits, or 4 bytes, of memory (i.e. 32 bits of
RAM). This is still expressed as $O(1)$ in big O notation because fixed numbers
are always reduced to the largest iterable amount, which is a fixed number in
this case. This will make more sense as we move through this subject.

Let's move onto a more commonly seen notation:

$$ O(n) $$

This is pronounced "O of n", and is one of the most common specifications you
will see when using big O notation. In terms of Time Complexity, this notation
means "This will take <em>n</em> amount of iterations to finish". Consider this
classic for loop in javascript:

```js
let n = 10;
for (let i = 0; i < n; i++) {
  console.log(i);
}
```

This is a classic for loop that simply counts from 0 to 10. How long will this
take? Ten iterations, i.e. `n` iterations. The reason this is expressed as
$O(n)$ in big O notation is because `n` is unknown, it could be 10, it could be
1, it could be 1_000_000, we don't know, but we have to express it somehow. Now
let's say we had a nested for loop:

```js
let n = 5;
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    console.log(j);
  }
}
```

To be very clear about what's happening here, let's actually print out the
results:

```
0
1
2
3
4
0
1
2
3
4
0
1
2
3
4
0
1
2
3
4
0
1
2
3
4
```

We count up to n twice over. For each time we count one cycle of `n` with the
variable `i`, we then iterate again up to `n` with the variable `j`, resulting
in an exponent of `n` amount of times we go over (since we use `n` to count in
the inner `for` loop as well). Specifically we count up to n n^2 times. This is
expressed in big O notation like so:

$$ O(n^2) $$

Spoken as "O of n squared". Generally speaking when you see two double for loops
in a programming project, you should be a bit suspicious that something is
wrong. Looping through a data set using a nested for loop means that as our data
set increases (n goes up), the amount of time to parse through and "do
something" with that data also goes up, and contributes to longer wait times for
our user and potentially costs more money to our employers. This continues to
get worse as it goes on, consider this nested for loop:

```js
let n = 5;
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    for (let k = 0; k < n; k++) {
      console.log(k);
    }
  }
}
```

This would be considered:

$$ O(n^3) $$

Or "O of n cubed", etc. What is the inverse of this, what could be better than
$O(n)$?

Well let's consider this big O notation:

$$ O(log(n))$$

Those of you who recall high school mathematics might recall Logirithms, which
are the inverse function of exponentiation. What this means in laymans terms is
that we are <em>dividing</em> the data set. In this particular form of the
notation, we are dividing the data set <em>in half</em> per iteration. Consider
the following example:

```js
const binarySearch = (arr, target) => {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    // Get the middle index of the array
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid; // Target found
    } else if (arr[mid] < target) {
      left = mid + 1; // Target is in the right half
    } else {
      right = mid - 1; // Target is in the left half
    }
  }

  return -1; // Target not found
};

// Example usage
const sortedArray = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19];
const target = 11;
const index = binarySearch(sortedArray, target);

console.log(`Target ${target} found at index: ${index}`);
```

In this classic example of a Binary Search Algorithm, we establish a sorted
Array to look for a target number.

Note: This algorithm relies on us passing a sortedArray to it.

We establish two "pointers", one that is the index of the beginning of the array
called left, which holds the value representing an index of 0. We then create a
corresponding right pointer, which olds the value representing the last index of
the array.

We instantiate a while loop that checks for whether or not left has "passed or
met" the right index (this will make sense in a moment). We then calculate the
middle of the array. If the target lives in the middle of the array, we return
that index as our solution. Otherwise, we then check if the number found at that
index is less than the target. If it is, then we reassign the left to the middle
index (+1 so we don't use that number again). If it is NOT, then we reassign the
right to the mid index (-1 so we don't use that number again).

Note that in either case, (i.e. whether the number at the middle index is
greater than or less than the target or NOT), we move one of the pointers (left
or right) to the middle of the array so that we can only search either the left
hand side or the right hand side of the array that remains on the next iteration
through the `while` loop. Effectively, our strategy cuts our data set "in half"
every iteration. Instead of vastly increasing the amount of time it takes for us
to find our solution like in our nested for loop examples from before, in this
example we are actually decreasing the amount of time it takes for us to find
our solution on each iteration, accomplishing a faster time complexity than
$O(n)$. We have effectively accomplished a logarithmic solution, i.e.
$O(log(n))$

There are even more expressions of big O notations, but these are the essentials
that you should become familiar with as a beginner.
[Here](https://en.wikipedia.org/w/index.php?title=Big_O_notation#Orders_of_common_functions)
is a full list of other notations should you wish to know other forms, and as
you progress in your knowledge, I highly recommend you do so.

### Big O Of Our Two Sum Solutions

**Brute Force Solution:**

Let's now annotate the Time and Space Complexity of our two different Two Sum
solutions. Let's first recall our original double for loop solution:

```js
const twoSumBruteForce = (nums, target) => {
  let result = [];
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === complement) {
        result = [i, j];
        return result;
      }
    }
  }

  return [];
};
```

Knowing what we know now, we can probably easily deduce that the time complexity
of our Brute Force Solution to Two Sum is $O(n^2)$. We iterate through the
`nums` array twice in a nested for loop. But what about our Space complexity?
Space complexity is a bit trickier to deduce, as it requires us to have a deeper
understanding of how our various Data Structures interplay with RAM and how our
usage of iteration over the input affects this. Consider this adjustment to our
Brute Force Solution:

```js
const twoSumBruteForce = (nums, target) => {
  let result = [];
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    const bigArray = new Array.from(1000);

    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === complement) {
        result = [i, j];
        return result;
      }
    }
  }

  return [];
};
```

Now, with this adjustment, for each iteration of our `nums` array, we create a
random new array called `bigArray` that has 1000 empty `undefined` elements in
it. Although the array is empty, we have told the JavaScript runtime to allocate
enough memory for 1000 contiguous addresses in memory that all contain
`undefined`. This is obviously a huge waste of memory, but it demonstrates how
every declaration of a new Data Structure, or even Data Primitives (i.e. basic
variables), can drastically increase the amount of memory utilized for our
program. So what does that mean the space comlexity is for our original solution
before we did all this undefined Array ridiculousness:

```js
const twoSumBruteForce = (nums, target) => {
  let result = [];
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    for (let j = i + 1; j < nums.length; j++) {
      if (nums[j] === complement) {
        result = [i, j];
        return result;
      }
    }
  }

  return [];
};
```

Well, we only instantiate one result array, and ultimately we don't instantiate
anything other than a new number to keep track of the index for each iteration
of the loop. In terms of space complexity, the amount of memory the iterators
have is <em>negligible</em>, i.e. it does NOT contribute in any significant way
to getting a general idea of how our program scales in terms of RAM usage with
the input (the `nums` array's size). Thusly only the amount of memory to
allocate for the `result` array matters, and this is of a <em>fixed</em> size.
Whenever our Time or Space complexity is of a fixed size (i.e. it does not rely
on the size of the input), then it can be said to be of "constant" time. This
means it can be expressed in big O notation like so:

$$ O(1) $$

Thusly our Time Complexity for our Brute Force Solution to the Two Sum Problem
is:

$$ O(n^2) $$

And the Space Complexity for our Brute Force Solution to the Two Sum Problem is:

$$ O(1) $$

Let's now ramp up the difficulty a bit and re analyze our Time and Space
Complexity of our Hash Map Solution to Two Sum:

**Hash Map Solution:**

Let's recall our Hash Map Solution to Two Sum now:

```js
const twoSum = (nums, target) => {
  const numMap = new Map();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];

    if (numMap.has(complement)) {
      return [numMap.get(complement), i];
    }

    numMap.set(nums[i], i);
  }

  return [];
};
```

Right off the bat, we can easily deduce that the time complexity is greatly
reduced, there is a single iteration through our input, the `nums` array. This
indicates that we will only take as much time as there exists for how many
elements exist in the `nums` array, which we could of course, express as having
`n` elements. Thusly the time complexity of our Hash Map Solution can be
expressed in big O notation as:

$$ O(n) $$

But as we discussed much earlier in this talk, the Space Complexity is a bit
more difficult to deduce. Again, we have to think on how memory is allocated and
how it is tied to the size of our input. Unlike the Brute Force Solution, we
actually DO create new key/value pairs in our `numMap` on every iteration of the
`nums` array. Thusly we require more memory to allocate a new key/value pair to
our `numMap` on each iteration of our `nums` array until we find the
`complement` number to our `target`. Thusly we could potentially iterate through
the entire array, continuing to add more key/value pairs to our `numMap` until
the very end (if we never find a `complement` to our `target`), and thusly our
space complexity corresponds directly with the size of our `nums` array. This
result in our Space complexity for the Hash Map Solution to Two Sum also being:

$$ O(n) $$

## Conclusion

In my original plan to address an Introduction to Algorithms, it was actually my
intention to cover far more problems from LeetCode than simple Two Sum, but it
occurred to me that understanding how to think Programatically when it comes to
Algorithms would be far more important than simply banging our heads around
trying to figure out various puzzles, especially since we are all beginners
here.

I want to take a moment here at the end that these fundamental concepts we have
covered today are actually of greater importance than your ability to solve
LeetCode and other similar coding puzzle problems. The subjects we've covered
today are heavily related to those sorts of platforms, but without some of these
basic building blocks under your belt, it is very hard to progress towards
thinking in a more pragmatic and programatic way when creating software.

Oftentimes when we're creating software as beginners, so much of the
abstractions we work with hide these things from us, and so we think they don't
really matter. Ultimately the job of understanding how much CPU cycles or RAM
allocation is the job for those other "smarter" people. But that's not true. If
you've ever wondered why your application is running slowly, or you've run out
of hard disk or RAM space on your computer because you automated a process using
a `for` loop, `while` loop, or God forbid you've used recursion improperly, you
have probably experienced the painful consequences of not understanding how your
program actually works.

Conversely, if you've ever made your program significantly faster or more
efficient by utilizing these tools properly, you have probably saved your
company time and money and ultimately you are a much better programmer for it.
It is my hope that this short talk has instilled in you both a respect for, and
a desire to learn more about, this complex and fascinating topic.

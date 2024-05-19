# Greedy-Algorithm
 A simple explanation on the Greedy Algorithm

### Introduction
Greedy algorithms are a category of algorithms that solve optimisation problems by making a series of choices that are locally optimal, aiming for a globally optimal solution. These algorithms operate by always choosing the best immediate option, without taking future outcomes into account. 


### Benefits and Challenges of the Greedy Algorithm
Greedy algorithms are simple to implement and efficient, making them ideal for solving problems where finding the optimal solution is not necessary. They are often used in scenarios where a quick, satisfactory solution is more important than an optimal one. However, greedy algorithms can be challenging to design and validate, as ensuring their correctness can be complex. Despite these challenges, greedy algorithms are widely used in various applications, such as scheduling, data compression, and network routing.

#### **Benefits:**
- **Simplicity:** Developing greedy algorithms is typically straightforward.
- **Ease of Analysis:** Analysing their runtime is often simpler than methods like divide and conquer, which involve complex recursion and numerous subproblems.
  
#### **Challenges:**
- **Correctness:** Verifying the correctness of greedy algorithms can be complex and requires deep understanding and inventive thinking. Proving their validity is often more intricate than their initial design.

### Key Characteristics of Greedy Algorithms

- **Simplicity:** They are straightforward and accessible, ideal for beginners. They make the most immediate beneficial choice, avoiding complexities found in more convoluted algorithms.
- **Speed:** They quickly find sufficiently good solutions, making them suitable for scenarios where a rapid response is more valuable than an optimal one.
- **Effectiveness:** In some cases, they can yield the best possible outcome. For example, finding the shortest route on a grid by consistently choosing the nearest point can result in the shortest path.

The following image is an example of a greedy algorithm in action. The algorithm aims to find the shortest path from the start to the end point by always choosing the nearest point. This method is simple, fast, and effective, making it an excellent example of a greedy algorithm.

![Alt Text](/Figures/sub_problem.png)

### An Example of the Greedy Algorithm

A great way to understand the greedy algorithm is through an example. Let's consider a classic problem that can be solved using this approach: the coin change problem. The full code for this including numerous examples, as well as comparing how well Dynamic Programming does the same problem can be found at: [Coin Change Problem](coin_change.ipynb)

A simple summary of this is shown below with one example:

#### **Problem Statement**

Given a list of coin denominations and an amount, determine the minimum number of coins needed to make up that amount. For simplicity, we'll assume the denominations allow for an exact solution under all circumstances.

**Example**
- Denominations: 1, 5, 10, 25
- Amount to make change for: 63 cents
  
#### **Greedy Approach**
The greedy approach to this problem is to always use the largest denomination that does not exceed the remaining amount until the entire amount is paid. Here’s how you would solve the problem for 63 cents using the denominations provided:
- Start with the largest coin and use as many as you can without exceeding the amount.
- Move to the next largest coin and repeat until the amount is reduced to zero.

#### **Step-by-Step Calculation**
- 25 cents: Use two 25 cent coins to make 50 cents. Remaining amount: 63 - 50 = 13 cents.
- 10 cents: Use one 10 cent coin to make 10 cents. Remaining amount: 13 - 10 = 3 cents.
- 5 cents: No 5 cent coins used because they exceed the remaining amount.
- 1 cent: Use three 1 cent coins to cover the remaining 3 cents.

#### Code Structure

The [Coin Change Problem](coin_change.ipynb) file uses this simple function for the Greedy Algorithm. The function takes a list of coin denominations and an amount as input and returns the minimum number of coins needed to make up that amount. The function also returns the coins used to make up the amount.

```py
def find_min_coins(denominations, amount):
    denominations.sort(reverse=True)
    coin_count = 0
    coin_used = []

    for coin in denominations:
        while amount >= coin:
            amount -= coin
            coin_count += 1
            coin_used.append(coin)

    return coin_count, coin_used
```

While the greedy algorithm can be effective and efficient in scenarios where larger denominations can be repeatedly subtracted from the amount without passing over smaller but more optimal combinations, its effectiveness is contingent on the specific set of denominations provided. It is not universally optimal and can fail to find the minimal coin solution in certain cases, illustrating its fundamental limitation in handling all possible coin change scenarios.

### Comparison with Dynamic Programming

Greedy algorithms are often compared with other optimisation algorithms, such as dynamic programming and divide and conquer. While each method has its strengths and weaknesses, greedy algorithms are particularly well-suited for problems where a series of choices leads to an optimal solution. Here are some key differences between greedy algorithms and other optimisation techniques:

#### **Dynamic Programming Approach**

The greedy approach works for the denominations provided, but it doesn’t work for all denominations. For example, if the denominations were 1, 3, and 4, the greedy approach would fail for 6 cents. The greedy approach would use 4, then 1, and then 1, for a total of 3 coins. However, the optimal solution is to use 3 coins of denomination 2. This is where dynamic programming comes in. We can solve this problem using dynamic programming by following these steps:
- Create a list to store the minimum number of coins needed to make up each amount from 0 to the target amount.
- Initialise the list with infinity for all amounts except 0, which is initialised to 0.
- For each amount from 1 to the target amount, iterate through all the denominations and update the minimum number of coins needed to make up that amount.
- The minimum number of coins needed to make up the target amount is the value at the target amount in the list.
- Return the minimum number of coins needed.

In [Coin Change Problem](coin_change.ipynb), a dynamic programming function is also used and then compared against the greedy algorithm. The dynamic programming function is as follows:

```py
def find_min_coins_dp(denominations, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    coins_used = [0] * (amount + 1)

    # Iterate over each amount from 1 to the target amount
    for i in range(1, amount + 1):
        for coin in denominations:
            if i >= coin and dp[i - coin] + 1 < dp[i]:
                dp[i] = dp[i - coin] + 1
                coins_used[i] = coin

    # Reconstruct the solution
    if dp[amount] == float('inf'):
        return float('inf'), []  # No solution found

    result = []
    while amount > 0:
        result.append(coins_used[amount])
        amount -= coins_used[amount]

    return len(result), result
```

To view the results and comparison, check the [Coin Change Problem](coin_change.ipynb) file.

### Another Example of the Greedy Algorithm

Another example of the greedy algorithm is the memory allocation problem, where the goal is to allocate memory blocks to processes in a way that minimises wasted space. The full code for this example can be found at: [Memory Allocation Problem](memory_allocation.ipynb), where the Greedy Algorithm and Dynamic Programming Algorithm are compared.

**Problem Statement**

Given a set of memory blocks of different sizes and a set of processes each requiring a certain amount of memory, allocate memory to the processes in such a way that minimises the wasted space. The "First Fit" algorithm places each process in the first block of memory that is large enough to accommodate it.

#### **Greedy Approach**
The Greedy Algorithm places each process in the first block of memory that is large enough to accommodate it. This algorithm is simple and efficient, but it may not always produce the optimal solution. It does the following process:
1. Sort the memory blocks in ascending order of size.
2. For each process, find the first memory block that is large enough to accommodate it.
3. Allocate the process to that memory block and update the memory block size.
4. Repeat steps 2 and 3 for all processes.
5. Calculate the wasted space by summing the difference between the memory block size and the process size for each process.
6. Return the total wasted space.
7. The time complexity of this algorithm is $O(n \log n)$ due to the sorting step.

```py
def first_fit(memory_blocks, processes):
    allocation = [-1] * len(processes)
    wasted_space = 0

    for i, process in enumerate(processes):
        for j, block in enumerate(memory_blocks):
            if block >= process:
                allocation[i] = j
                memory_blocks[j] -= process
                wasted_space += block - process
                print(f"Process {process} allocated to block {block} (index {j})")
                break

    print(f"Total wasted space: {wasted_space}")
    return allocation
```

#### **Dynamic Programming Approach**
The Dynamic Programming approach attempts to find the optimal allocation of processes to memory blocks by considering all possible ways to allocate memory and choosing the one that minimises wasted space. It does the following process:
1. Create a 2D array dp of size $(n+1) x (m+1)$, where n is the number of processes and m is the number of memory blocks.
2. Initialise `dp[i][j]` to be the minimum wasted space when allocating the first `i` processes to the first `j` memory blocks.
3. For each process i and memory block `j`, calculate the wasted space if process `i` is allocated to memory block `j` and update `dp[i][j]` accordingly.
4. Return the minimum wasted space from the last row of the dp array.
5. The time complexity of this algorithm is $O(n*m)$ where n is the number of processes and m is the number of memory blocks.

```py
def dynamic_fit(memory_blocks, processes):
    allocation = [-1] * len(processes)
    wasted_space = 0
    
    for i, process in enumerate(processes):
        best_idx = -1
        for j, block in enumerate(memory_blocks):
            if block >= process:
                if best_idx == -1 or memory_blocks[best_idx] > block:
                    best_idx = j
        if best_idx != -1:
            allocation[i] = best_idx
            memory_blocks[best_idx] -= process
            print(f"Process {process} allocated to block {memory_blocks[best_idx] + process} (index {best_idx})")
    
    print(f"Total wasted space: {wasted_space}")
    return allocation
``` 
The results of the Greedy Algorithm and Dynamic Programming Algorithm are then compared in the [Memory Allocation Problem](memory_allocation.ipynb) file.

### Applications of Greedy Algorithms
Greedy algorithms are employed in a variety of practical scenarios due to their straightforward nature and efficiency. Here are some notable applications:
- **Minimum Spanning Tree (MST):** Used in creating a spanning tree that connects all vertices in a graph with the minimum possible total weight of edges.
- **Dijkstra's Shortest Path Algorithm:** Finds the shortest path between a starting vertex and all other vertices in a weighted graph, useful for routing and navigation.
- **Travelling Salesman Problem (TSP):** Although not always yielding the most optimal solution, it approximates the shortest possible route that visits each city once and returns to the origin.
- **Huffman Coding:** Assigns shorter codes to more frequently occurring symbols, optimising data encoding efficiency.
  
### Advantages of Using Greedy Algorithms
Greedy algorithms are straightforward to implement and intuitive to understand. They are known for their computational efficiency, often exhibiting a time complexity of $O(N log⁡N)$. These characteristics make them highly effective for solving optimisation problems where solutions need to be found quickly, and the goal is to either maximize or minimize a given value.

### Disadvantages and Limitations of Greedy Algorithms
While greedy algorithms are advantageous for their simplicity and efficiency, they do have limitations:
- **Sub-Optimality:** Greedy algorithms may not always provide the best solution possible, especially in complex optimisation scenarios where a global optimum is needed.
- **Single-Run Limitation:** Greedy algorithms typically run once and make decisions based solely on current available data without revisiting or revising previous decisions. This can lead to issues in accuracy and reliability because they do not verify the correctness of the output after execution.
  
### Conclusion
Greedy algorithms provide a straightforward and often efficient method for solving complex problems where a series of choices leads to an optimal solution. Their implementation varies widely across different types of problems, from simple activity selection to complex data compression algorithms like Huffman Coding. The choice of using a greedy algorithm depends on the problem's characteristics and the need for quick, often good-enough solutions.

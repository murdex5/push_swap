<h1 align="center">
  Push_swap
</h1>

<p align="center">
  <em>Sorting a stack of integers with a limited set of operations using the Mechanical Turk algorithm.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-C-blue.svg?style=for-the-badge" alt="Language C">
  <img src="https://img.shields.io/badge/School-42-black.svg?style=for-the-badge" alt="42 School Project">
</p>

## 📖 Table of Contents
- [About The Project](#-about-the-project)
- [The Challenge](#-the-challenge)
- [Allowed Operations](#-allowed-operations)
- [The Algorithm: Mechanical Turk](#-the-algorithm-mechanical-turk)
- [How To Use](#-how-to-use)
- [Example](#-example)
- [Author](#-author)

## 📝 About The Project

`push_swap` is a classic algorithm project from the 42 school curriculum. The goal is to sort a stack of unique integers using a limited set of instructions and a second, auxiliary stack. The challenge is not just to sort the numbers, but to do so in the minimum number of moves.

This project tests your understanding of algorithms, data structures (stacks), and optimization. The program (`push_swap`) takes a list of integers as input and outputs a sequence of operations to sort them.

## 🎯 The Challenge

You are given two stacks, `a` and `b`:
-   **Stack `a`**: Contains a random list of unique integers.
-   **Stack `b`**: Is initially empty.

The goal is to sort stack `a` in ascending order (with the smallest number at the top) using the allowed operations. The program should be efficient and use the fewest possible instructions.

## ✨ Allowed Operations

Only the following operations are permitted to manipulate the stacks:

| Operation | Description                                                               |
| :-------: | ------------------------------------------------------------------------- |
|    `sa`   | **Swap a**: Swaps the first two elements at the top of stack `a`.           |
|    `sb`   | **Swap b**: Swaps the first two elements at the top of stack `b`.           |
|    `ss`   | Performs `sa` and `sb` at the same time.                                  |
|    `pa`   | **Push a**: Takes the top element from stack `b` and moves it to stack `a`.|
|    `pb`   | **Push b**: Takes the top element from stack `a` and moves it to stack `b`.|
|    `ra`   | **Rotate a**: Shifts all elements of stack `a` up by one. The first becomes the last. |
|    `rb`   | **Rotate b**: Shifts all elements of stack `b` up by one. The first becomes the last. |
|    `rr`   | Performs `ra` and `rb` at the same time.                                  |
|    `rra`  | **Reverse rotate a**: Shifts all elements of stack `a` down by one. The last becomes the first. |
|    `rrb`  | **Reverse rotate b**: Shifts all elements of stack `b` down by one. The last becomes the first. |
|    `rrr`  | Performs `rra` and `rrb` at the same time.                                |

## 🧠 The Algorithm: Mechanical Turk

This project implements the **Mechanical Turk algorithm**, an efficient strategy for solving the `push_swap` problem.

1.  **Initial Push to B**: All numbers from stack `a` are pushed to stack `b`, except for the last three. This leaves stack `a` with three numbers, which can be easily sorted.

2.  **Sort the Trio**: The three remaining numbers in stack `a` are sorted using a simple, optimal set of instructions. This creates a small, sorted base to build upon.

3.  **Cost Calculation**: For each number in stack `b`, the algorithm calculates the "cost" of moving it to its correct position in stack `a`. The cost is the total number of rotations required to:
    -   Bring the target number to the top of stack `b`.
    -   Rotate stack `a` so that the number can be inserted in the correct sorted position.
    The algorithm intelligently checks for combined rotations (`rr` and `rrr`) to find the most efficient path.

4.  **Find the Cheapest Move**: The algorithm identifies the number in stack `b` that has the lowest cost to move.

5.  **Execute and Repeat**: The cheapest set of rotations is executed, followed by a `pa` to move the number from `b` to `a`. This process is repeated until stack `b` is empty.

6.  **Final Rotation**: Once all numbers are sorted in stack `a`, a final series of rotations may be needed to bring the smallest element to the very top.

This method ensures that every move is the most efficient one possible at that moment, leading to a low total instruction count.

## 🚀 How To Use

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/murdex5/push_swap.git
    cd push_swap
    ```

2.  **Compile the project:**
    The project includes `ft_printf` as a dependency. The `Makefile` will handle its compilation.
    ```sh
    make
    ```

3.  **Run the program:**
    Execute `push_swap` with a list of numbers as arguments.
    ```sh
    ./push_swap 4 67 3 8 2
    ```

4.  **Check the output (Optional):**
    The project may include a `checker` program to verify the sorting instructions. You can pipe the output of `push_swap` into the `checker`.
    ```sh
    ARG="4 67 3 8 2"; ./push_swap $ARG | ./checker $ARG
    ```
    If the output is `OK`, the stack was sorted correctly. If `KO`, there was an error. You can also see the number of instructions with `wc -l`.
    ```sh
    ./push_swap $ARG | wc -l
    ```

## 💡 Example

```sh
# Generate a list of numbers and run push_swap
$ ARG="8 5 3 9 2 1"; ./push_swap $ARG
pb
pb
rrb
pb
ra
sa
rra
pa
ra
pa
pa
rra
rra
rra

# Check if the output correctly sorts the stack
$ ./push_swap $ARG | ./checker $ARG
OK

# Count the number of instructions
$ ./push_swap $ARG | wc -l
      14
```

## ✍️ Author

**murdex5** - [GitHub Profile](https://github.com/murdex5)
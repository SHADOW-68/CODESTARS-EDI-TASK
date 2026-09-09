# Tab Overflow

**Time Limit:** 1 second | **Memory Limit:** 256 megabytes

## Story

It is 2:14 AM. Your submission for the Data Structures assignment is due at 9:00 AM, and you have opened your laptop with the noble intention of "just quickly checking one thing."

Four hours later, you are still checking things.

Your Chrome window now has $N$ tabs open, laid out left to right in the order you opened them. Somewhere in there is a lecture recording you were supposed to watch two weeks ago, at least one StackOverflow thread titled "Why is this simple loop not working???, a food delivery tab you opened out of despair around hour two, and a tab comparing the specs of a laptop you are not going to buy, because misery loves shopping.

Each tab is, in its own way, a small monument to a decision you made. Each tab is also consuming a fixed and specific amount of memory, because your laptop only cares about RAM.

Your laptop's fan is spinning like it's about to fly out of your laptop. A little research (three more tabs) reveals the grim truth: Chrome is allowed a budget of $X$ MB before your system starts throttling everything, including critically the compiler you need to actually finish the assignment.

You briefly consider closing tabs one at a time, carefully curating your browser like a bonsai tree. You reject this idea immediately. It is 2 AM. You do not have the emotional bandwidth for careful curation. You want *one decisive motion* — grab a single unbroken stretch of tabs, left to right, no gaps, no exceptions, and slam it shut. If, by some miracle, your current setup is already within budget, you get to do nothing and simply feel good about yourself for the first time tonight.

But you are not reckless. You are, after all, still a computer engineering student, even at 2 AM. You want to close the *fewest* tabs possible — sacrificing the smallest, most contiguous chunk of your browsing history necessary to make your laptop stop sounding like it's preparing for orbit.

Somewhere in that string of $N$ tabs is your answer. Find it before your laptop finds its limit.

## Problem

You are given $N$ tabs, indexed $1$ through $N$ from left to right. Tab $i$ consumes $A_i$ MB of memory.

You are allowed to close **at most one contiguous segment** of tabs that is, a range $[l, r]$ with $1 \le l \le r \le N$ or close nothing at all. After closing, the total memory used by all *remaining* tabs must not exceed $X$ MB.

Determine the **minimum number of tabs** you must close to achieve this.

It is guaranteed that a valid choice of segment (possibly empty) always exists.

## Input

The first line contains a single integer $T$ — the number of test cases.

Each test case is given on two lines:
- The first line contains two integers $N$ and $X$.
- The second line contains $N$ integers $A_1, A_2, \dots, A_N$ — the memory used by each tab, in order.

## Constraints

- $1 \le T \le 10^4$
- $1 \le N \le 2 \times 10^5$
- $1 \le A_i \le 10^9$
- $1 \le X \le 10^{14}$
- $\sum N \le 2 \times 10^5$ across all test cases

## Output

For each test case, output a single integer on its own line: the minimum number of tabs that must be closed.

## Sample Input

```
4
5 10
4 2 7 3 1
6 12
3 4 2 6 1 5
5 20
5 1 1 1 1
7 10
8 2 2 2 2 2 2
```

## Sample Output

```
1
3
0
2
```

## Example

In the first test case, closing just the single tab worth $7$ MB is enough no need to sacrifice your food delivery tab *and* the lecture recording when one clean cut will do.

In the third test case, your browser was already within budget the whole time. Sometimes the crisis was in your head. Close nothing, and go finish the assignment.

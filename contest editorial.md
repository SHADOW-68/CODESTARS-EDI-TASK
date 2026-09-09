CodeChef Starters 254 — Selected Editorial

Problems covered:

* REACH WEIGHT
* MAXIMUM SUM
* GOOD SUBSET(EASY)

**1.Reach Weight:**

Rating: ~800
Tags: Math, Greedy

Hint 1:

You can buy either 1 kg for 20 or 2 kg for 30.
What happens if you need exactly 2 kg?

Hint 2:

Compare the cost of:
* two 1 kg weights
* one 2 kg weight

Which one is cheaper?

**Observation:**

Two 1 kg weights cost:20+20=40,while one 2 kg weight costs only 30.
Therefore, whenever possible, we should use a 2 kg weight. There is never a reason for an optimal solution to contain two 1 kg weights.
So:

* if N is even, use N/2 two-kg weights;
* if N is odd, use (N-1)/2 two-kg weights and one one-kg weight.

**Approach:**

The answer is therefore:

30 * (N / 2) + 20 * (N % 2) 

We can calculate this directly for every test case.

**Why does this work?**

If a solution contains two 1 kg weights, replacing them with one 2 kg weight keeps the total weight unchanged while reducing the cost from 40 to 30.
Hence an optimal solution contains at most one 1 kg weight.
The formula uses exactly that optimal combination, so it gives the minimum cost.

**Complexity:**

* Time: O(1)
* Space: O(1)

**CODE:**
#include <bits/stdc++.h>
using namespace std;

int main() {
    int T;
    cin >> T;

    while (T--) {
        long long N;
        cin >> N;

        cout << 30 * (N / 2) + 20 * (N % 2) << '\n';
    }

    return 0;
}

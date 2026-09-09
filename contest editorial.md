CodeChef Starters 254 — Selected Editorial

Problems covered:

* REACH WEIGHT
* MAXIMUM SUM

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

**2.MAXIMUM SUM**

Rating: ~900
Tags: Prefix Sum, Sliding Window

**Hint:**

Instead of thinking about which elements to remove, think about which elements remain after exactly K removals.

**Observation**

Suppose we remove x elements from the left and K-x elements from the right.
The remaining elements are always a contiguous subarray.
Also, exactly K elements are removed, so the remaining subarray has length: N-K
Therefore, the problem becomes finding the maximum sum of a subarray of fixed length N-K.
This can be done using a sliding window.

**Approach**

Let length = N-K.
First calculate the sum of the first length elements.
Then move the window one position at a time.

When the window moves:

* subtract the element leaving the window
* add the new element entering the window
* update the maximum sum

This checks every possible subarray of length N-K.

**Why does this work?**

After K removals, if x elements are removed from the left, then K-x elements are removed from the right. Hence the remaining elements form one contiguous subarray of length N-K.

Every such subarray can be obtained by choosing an appropriate number of removals from the left.

Therefore checking all windows of length N-K checks every possible final state. The maximum window sum is consequently the answer.

Complexity

Time: O(N)
Space: O(N)

#include <bits/stdc++.h>
using namespace std;

int main() {
    int T;
    cin >> T;

    while (T--) {
        int N, K;
        cin >> N >> K;

        vector<long long> A(N);

        for (auto &x : A)
            cin >> x;

        int len = N - K;

        long long window = 0;

        for (int i = 0; i < len; i++)
            window += A[i];

        long long ans = window;

        for (int i = len; i < N; i++) {
            window += A[i];
            window -= A[i - len];

            ans = max(ans, window);
        }

        cout << ans << '\n';
    }

    return 0;
}

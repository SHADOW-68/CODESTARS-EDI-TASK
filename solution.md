# Tab Overflow — Editorial


At first glance, the problem seems to ask: *which tabs should remain open?* This framing is unhelpful. Instead, consider the complement: *which tabs must be closed?*

Let `total` denote the sum of memory used by all tabs. If `total ≤ X`, the browser is already within budget and no tabs need to be closed — the answer is `0`.

Otherwise, closing tabs must free up at least
```
need = total - X
```
memory. The problem therefore reduces to a well-known form:

> **Find the shortest contiguous segment of tabs whose combined memory is at least `need`.**

This is the key observation.

## Approach: Two-Pointer / Sliding Window

Since every element is strictly positive (`A_i ≥ 1`), the prefix sum over any window is monotonic with respect to both endpoints — extending the window on the right can only increase the sum, and shrinking it from the left can only decrease it. This monotonicity is precisely what allows a linear-time sliding window.

The approach:

1. Maintain two pointers, `left` and `right`, both initialized to the start of the array, along with a running `windowSum`.
2. Advance `right` one step at a time, adding `memoryUsed[right]` to `windowSum`.
3. Whenever `windowSum ≥ need`, the current window is a valid candidate. Advance `left` forward — shrinking the window and subtracting from `windowSum` — for as long as the window remains valid, recording the minimum window length observed at each step.
4. After `right` has traversed the entire array, the recorded minimum is the answer.

Because each index is added to the window exactly once (by `right`) and removed exactly once (by `left`), no index is processed more than a constant number of times.

## Correctness

For a fixed right endpoint, shrinking the window from the left as far as the sum permits yields the shortest valid window ending at that position,shrinking further would violate the `≥ need` condition, and any position considered was already validated at that boundary. Since every right endpoint is examined, and the shortest window overall must end at some right endpoint, the global minimum recorded across all endpoints is guaranteed to be optimal.

## Complexity

- **Time:** O(N) per test case, since each pointer traverses the array at most once.
- **Space:** O(N), to store the input array.

## Note

With `N` up to `2 × 10^5` and each `A_i` up to `10^9`, `total` can reach up to `2 × 10^14` — well beyond the range of a 32-bit integer. All relevant quantities (`total`, `X`, `need`, `windowSum`) must be stored as `long long` to avoid overflow.

## Code(C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int T;
    cin >> T;

    while (T--) {
        int N;
        long long X;
        cin >> N >> X;

        vector<long long> memoryUsed(N);
        long long total = 0;

        for (auto &mem : memoryUsed) {
            cin >> mem;
            total += mem;
        }

        // Already within budget — no tabs need to be closed
        if (total <= X) {
            cout << 0 << '\n';
            continue;
        }

        long long need = total - X;
        long long windowSum = 0;
        int left = 0;
        int answer = N; // worst case: close every tab

        for (int right = 0; right < N; right++) {
            windowSum += memoryUsed[right];

            // Shrink from the left while the window remains valid
            while (windowSum >= need) {
                answer = min(answer, right - left + 1);
                windowSum -= memoryUsed[left];
                left++;
            }
        }

        cout << answer << '\n';
    }

    return 0;
}
```

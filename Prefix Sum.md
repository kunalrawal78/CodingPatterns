

## 🔹 What is Prefix Sum?

For an array `arr` of size `n`:

```cpp
prefix[i] = arr[0] + arr[1] + ... + arr[i];
```

Using prefix sum, **subarray sum [l..r]** can be calculated in **O(1)**:

```cpp
sum(l, r) = prefix[r] - (l > 0 ? prefix[l - 1] : 0);
```

---

## 🧠 When to Use Prefix Sum?

Use Prefix Sum when a problem involves:

* Arrays / Subarrays
* Range sum queries
* Sum equals `K`
* Sum ≥ `K`
* Left sum == Right sum
* Presence of **negative numbers**

---

# 🔑 Prefix Sum Sub-Patterns

---

## 1️⃣ Basic Range / Subarray Sum

### 📌 When to Use

* Multiple range sum queries
* Static array (no updates)

### ✅ C++ Implementation

```cpp
#include <vector>
using namespace std;

vector<int> buildPrefix(vector<int>& arr) {
    vector<int> prefix(arr.size());
    prefix[0] = arr[0];

    for (int i = 1; i < arr.size(); i++)
        prefix[i] = prefix[i - 1] + arr[i];

    return prefix;
}

int rangeSum(vector<int>& prefix, int l, int r) {
    return prefix[r] - (l > 0 ? prefix[l - 1] : 0);
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/range-sum-query-immutable/](https://leetcode.com/problems/range-sum-query-immutable/)

---

## 2️⃣ Pivot / Equilibrium Index

### 📌 When to Use

* Left sum == Right sum problems

### ✅ C++ Implementation

```cpp
#include <vector>
#include <numeric>
using namespace std;

int pivotIndex(vector<int>& nums) {
    int totalSum = accumulate(nums.begin(), nums.end(), 0);
    int leftSum = 0;

    for (int i = 0; i < nums.size(); i++) {
        if (leftSum == totalSum - leftSum - nums[i])
            return i;
        leftSum += nums[i];
    }
    return -1;
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/find-pivot-index/](https://leetcode.com/problems/find-pivot-index/)

---

## 3️⃣ Subarray Sum = K (Negative Numbers Allowed)

### 📌 When to Use

* Count subarrays with exact sum `K`
* Array contains negative numbers

❌ Sliding Window fails

✅ Prefix Sum + HashMap

### ✅ C++ Implementation

```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int subarraySum(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    freq[0] = 1;

    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;
        if (freq.count(sum - k))
            count += freq[sum - k];
        freq[sum]++;
    }
    return count;
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/subarray-sum-equals-k/](https://leetcode.com/problems/subarray-sum-equals-k/)

---

## 4️⃣ Shortest Subarray with Sum ≥ K

### 📌 When to Use

* Find shortest subarray with sum ≥ `K`
* Negative numbers present

❌ Sliding Window fails

✅ Prefix Sum + Deque

### ✅ C++ Implementation

```cpp
#include <vector>
#include <deque>
#include <climits>
using namespace std;

int shortestSubarray(vector<int>& nums, int k) {
    int n = nums.size();
    vector<long long> prefix(n + 1, 0);

    for (int i = 0; i < n; i++)
        prefix[i + 1] = prefix[i] + nums[i];

    deque<int> dq;
    int ans = INT_MAX;

    for (int i = 0; i <= n; i++) {
        while (!dq.empty() && prefix[i] - prefix[dq.front()] >= k) {
            ans = min(ans, i - dq.front());
            dq.pop_front();
        }
        while (!dq.empty() && prefix[i] <= prefix[dq.back()])
            dq.pop_back();

        dq.push_back(i);
    }

    return ans == INT_MAX ? -1 : ans;
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/)

---

## 5️⃣ Count of Range Sum (Lower ≤ Sum ≤ Upper)

### 📌 When to Use

* Count subarrays with sum in a range
* Large constraints

✅ Prefix Sum + Merge Sort

### ✅ C++ Implementation

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    int countRangeSum(vector<int>& nums, int lower, int upper) {
        vector<long long> prefix(nums.size() + 1, 0);
        for (int i = 0; i < nums.size(); i++)
            prefix[i + 1] = prefix[i] + nums[i];

        return mergeSort(prefix, 0, prefix.size(), lower, upper);
    }

    int mergeSort(vector<long long>& sum, int left, int right, int lower, int upper) {
        if (right - left <= 1) return 0;

        int mid = (left + right) / 2;
        int count = mergeSort(sum, left, mid, lower, upper)
                  + mergeSort(sum, mid, right, lower, upper);

        int j = mid, k = mid, t = mid;
        vector<long long> temp;

        for (int i = left; i < mid; i++) {
            while (k < right && sum[k] - sum[i] < lower) k++;
            while (j < right && sum[j] - sum[i] <= upper) j++;
            while (t < right && sum[t] < sum[i]) temp.push_back(sum[t++]);
            temp.push_back(sum[i]);
            count += j - k;
        }
        copy(temp.begin(), temp.end(), sum.begin() + left);
        return count;
    }
};
```

### 🔗 LeetCode

* [https://leetcode.com/problems/count-of-range-sum/](https://leetcode.com/problems/count-of-range-sum/)

---

# 🧭 Prefix Sum Flowchart (Markdown)

```
Arrays / Subarrays
        |
        v
   Prefix Sum
        |
        +---------------------+
        |                     |
  Pivot Index         Subarray Problems
        |                     |
     Direct Check      Negative Numbers?
                           /     \
                         Yes      No
                          |        |
                Prefix + HashMap   Sliding Window
                    (Sum = K)
                          |
                Sum ≥ K / Shortest?
                          |
                Prefix + Deque
                          |
                Range Sum Count
                          |
            Prefix + Merge Sort
```

---

# 🚀 Quick Cheat Sheet

| Problem Type     | Technique           |
| ---------------- | ------------------- |
| Range Sum Query  | Prefix Sum          |
| Pivot Index      | Prefix Sum          |
| Subarray Sum = K | Prefix + HashMap    |
| Shortest Sum ≥ K | Prefix + Deque      |
| Range Sum Count  | Prefix + Merge Sort |

---

### ⭐ Tip

If a problem involves **subarrays + sum**, always think **PREFIX SUM first**.

---

✅ **This file is fully GitHub-ready.**
Just name it `README.md` and push 🚀

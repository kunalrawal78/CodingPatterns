
## 🔹 What is Binary Search?

Binary Search is an optimization technique used when:

* The **search space is sorted**
* OR the **answer space is monotonic** (true → false or false → true)

Time Complexity:

```
O(log N)
```

---

## 🧠 When to Think of Binary Search?

Ask yourself:

* Is the array **sorted**?
* Can I **discard half** of the search space?
* Is the answer dependent on a **monotonic condition**?

If YES → Binary Search

---

# 🧩 Binary Search Sub-Patterns

---

## 1️⃣ Classic Binary Search (Search in Sorted Array)

### 📌 Use When

* Array is fully sorted
* Need to find exact element / position

### 🧪 Problems Covered

* Binary Search to find X
* Search Insert Position

### ✅ C++ Template

```cpp
int binarySearch(vector<int>& arr, int target) {
    int low = 0, high = arr.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/)
* [https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)

---

## 2️⃣ Lower Bound / Upper Bound Pattern

### 📌 Use When

* Need **first / last position**
* Count occurrences
* Floor / Ceil problems

### 🧪 Problems Covered

* Implement Lower Bound
* Implement Upper Bound
* First & Last Occurrence
* Count Occurrences

### ✅ C++ Template (Lower Bound)

```cpp
int lowerBound(vector<int>& arr, int target) {
    int low = 0, high = arr.size();
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] < target) low = mid + 1;
        else high = mid;
    }
    return low;
}
```
✅ Custom C++ Implementation (Upper Bound)
```cpp
int upperBound(vector<int>& arr, int target) {
    int low = 0, high = arr.size();

    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] <= target)
            low = mid + 1;
        else
            high = mid;
    }
    return low;
}
```
⚡ STL Shortcut Functions

```cpp
int lb = lower_bound(arr.begin(), arr.end(), target) - arr.begin();
int ub = upper_bound(arr.begin(), arr.end(), target) - arr.begin();
```

🎯 Applications
```cpp
// First occurrence
int firstIndex = lb;

// Last occurrence
int lastIndex = ub - 1;

// Count of occurrences
int count = ub - lb;
```

### 🔗 LeetCode

* [https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

---

## 3️⃣ Binary Search on Rotated Sorted Array

### 📌 Use When

* Sorted array rotated at unknown pivot

### 🧪 Problems Covered

* Search in Rotated Sorted Array I
* Search in Rotated Sorted Array II
* Find Minimum
* Count Rotations

### ✅ C++ Template

```cpp
int search(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;

    while (low <= high) {
        int mid = (low + high) / 2;
        if (nums[mid] == target) return mid;

        if (nums[low] <= nums[mid]) {
            if (nums[low] <= target && target < nums[mid])
                high = mid - 1;
            else
                low = mid + 1;
        } else {
            if (nums[mid] < target && target <= nums[high])
                low = mid + 1;
            else
                high = mid - 1;
        }
    }
    return -1;
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/search-in-rotated-sorted-array/](https://leetcode.com/problems/search-in-rotated-sorted-array/)
* [https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

---

## 4️⃣ Single Element / Peak Element Pattern

### 📌 Use When

* One element appears once, others twice
* Peak element problems

### 🧪 Problems Covered

* Single Element in Sorted Array
* Find Peak Element

### ✅ C++ Template

```cpp
int singleNonDuplicate(vector<int>& nums) {
    int low = 0, high = nums.size() - 1;

    while (low < high) {
        int mid = low + (high - low) / 2;
        if (mid % 2 == 1) mid--;

        if (nums[mid] == nums[mid + 1])
            low = mid + 2;
        else
            high = mid;
    }
    return nums[low];
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/single-element-in-a-sorted-array/](https://leetcode.com/problems/single-element-in-a-sorted-array/)
* [https://leetcode.com/problems/find-peak-element/](https://leetcode.com/problems/find-peak-element/)

---

## 5️⃣ Binary Search on Answers (Search Space Reduction)

### 📌 Use When

* Answer lies in a range
* Feasibility function is monotonic

### 🧪 Problems Covered

* Square Root
* Nth Root
* Koko Eating Bananas
* Book Allocation
* Aggressive Cows
* Painter's Partition

### ✅ C++ Template

```cpp
bool isPossible(vector<int>& arr, int mid, int k) {
    int cnt = 1, sum = 0;
    for (int x : arr) {
        if (sum + x > mid) {
            cnt++;
            sum = x;
        } else sum += x;
    }
    return cnt <= k;
}

int binarySearchOnAnswer(vector<int>& arr, int k) {
    int low = *max_element(arr.begin(), arr.end());
    int high = accumulate(arr.begin(), arr.end(), 0);
    int ans = high;

    while (low <= high) {
        int mid = (low + high) / 2;
        if (isPossible(arr, mid, k)) {
            ans = mid;
            high = mid - 1;
        } else low = mid + 1;
    }
    return ans;
}
```

### 🔗 LeetCode

* [https://leetcode.com/problems/koko-eating-bananas/](https://leetcode.com/problems/koko-eating-bananas/)
* [https://leetcode.com/problems/book-allocation/](https://leetcode.com/problems/book-allocation/)
* [https://leetcode.com/problems/aggressive-cows/](https://leetcode.com/problems/aggressive-cows/)
* [https://leetcode.com/problems/painters-partition-problem/](https://leetcode.com/problems/painters-partition-problem/)

---

# 🧭 Binary Search Decision Flow (Markdown)

```
Is data sorted?
     |
     v
 Classic Binary Search
     |
Duplicates present?
     |
Lower / Upper Bound
     |
Array rotated?
     |
Rotated Binary Search
     |
Single / Peak element?
     |
Index parity check
     |
Answer in range?
     |
Binary Search on Answer
```

---

# 🚀 Binary Search Cheat Sheet

| Problem Type            | Pattern             |
| ----------------------- | ------------------- |
| Search element          | Classic BS          |
| First / Last Occurrence | Lower / Upper Bound |
| Rotated array           | Rotated BS          |
| Single / Peak           | Index parity        |
| Min / Max optimization  | BS on Answer        |

---

⭐ **Golden Rule**:

> If you can answer **YES/NO** for a given `mid`, you can apply **Binary Search on Answers**.

---

✅ **This README is fully GitHub-ready**
Save as `README.md` and push 🚀

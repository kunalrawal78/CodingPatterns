# 🔄 Array Rotation in C++

This repository contains C++ implementations for rotating an array using different approaches.

---

## 📌 Problem

Given an array `arr[]` of size `n` and an integer `k`:

- **Left Rotation**: Move the first `k` elements to the end  
- **Right Rotation**: Move the last `k` elements to the front  

---

## ⏱️ Complexity

| Approach | Time | Space |
|--------|------|-------|
| Extra Space | O(n) | O(n) |
| Reversal Algorithm | O(n) | O(1) |

---

## 1️⃣ ----Left Rotation (Extra Space)

```cpp
#include <bits/stdc++.h>
using namespace std;

void leftRotate(vector<int>& arr, int k) {
    int n = arr.size();
    k = k % n;
    vector<int> temp(n);

    for (int i = 0; i < n; i++) {
        temp[i] = arr[(i + k) % n];
    }
    arr = temp;
}
## ----right Rotation (Extra Space)
#include <bits/stdc++.h>
using namespace std;

void rightRotate(vector<int>& arr, int k) {
    int n = arr.size();
    k = k % n;
    vector<int> temp(n);

    for (int i = 0; i < n; i++) {
        temp[(i + k) % n] = arr[i];
    }
    arr = temp;
}
```
3️⃣ Left Rotation (Reversal Algorithm – No Extra Space)
```cpp
#include <bits/stdc++.h>
using namespace std;

void reverseArray(vector<int>& arr, int start, int end) {
    while (start < end) {
        swap(arr[start], arr[end]);
        start++;
        end--;
    }
}

void leftRotate(vector<int>& arr, int k) {
    int n = arr.size();
    k = k % n;

    reverseArray(arr, 0, k - 1);
    reverseArray(arr, k, n - 1);
    reverseArray(arr, 0, n - 1);
}

```
4️⃣ Right Rotation (Reversal Algorithm – No Extra Space)
```cpp
#include <bits/stdc++.h>
using namespace std;

void reverseArray(vector<int>& arr, int start, int end) {
    while (start < end) {
        swap(arr[start], arr[end]);
        start++;
        end--;
    }
}

void rightRotate(vector<int>& arr, int k) {
    int n = arr.size();
    k = k % n;

    reverseArray(arr, 0, n - 1);
    reverseArray(arr, 0, k - 1);
    reverseArray(arr, k, n - 1);
}

```

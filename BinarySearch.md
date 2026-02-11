# 📘 Binary Search Notes

---

# 🔎 Problem 1: Search Insert Position

## 📌 Problem Statement

Given a sorted array of distinct integers and a target value,  
return the index if the target is found.

If not, return the index where it would be inserted in order.

You must write an algorithm with **O(log n)** runtime complexity.

---

## 🧠 First Thoughts

- The array is sorted.
- Brute force will work in O(n).
- Since sorted, we can eliminate half each step.
- We need the first index where value >= target.

---

# 🐢 Phase 1 — Brute Force

## 💡 Idea

Traverse the array:
- If nums[i] == target → return i
- If nums[i] > target → return i
- If loop ends → return nums.size()

## ⏱ Time Complexity
O(n)

## 💾 Space Complexity
O(1)

---

## 💻 C++ Code — Brute Force

```cpp
int searchInsert(vector<int>& nums, int target) {
    for(int i = 0; i < nums.size(); i++) {
        if(nums[i] >= target) {
            return i;
        }
    }
    return nums.size();
}
```

---

# 🚀 Phase 2 — Optimal (Binary Search)

## 💡 Key Insight

We are finding:

> First index where nums[mid] >= target

This is exactly **Lower Bound**.

Pattern:
F F F F T T T T  
We search for **First True**.

---

## ⚡ Binary Search Logic

1. left = 0  
2. right = nums.size() - 1  
3. answer = nums.size()

While left <= right:
- mid = left + (right - left) / 2
- If nums[mid] >= target:
    - answer = mid
    - right = mid - 1
- Else:
    - left = mid + 1

Return answer.

---

## ⏱ Time Complexity
O(log n)

## 💾 Space Complexity
O(1)

---

## 💻 C++ Code — Optimal

```cpp
int searchInsert(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;
    int answer = nums.size();

    while(left <= right) {
        int mid = left + (right - left) / 2;

        if(nums[mid] >= target) {
            answer = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }

    return answer;
}
```

---

# 🧩 Edge Cases

- Empty array
- Target smaller than all elements
- Target greater than all elements
- Single element array

---

# 🎯 Pattern Recognition

Use Binary Search when:

- Array is sorted
- O(log n) is required
- We need insertion position
- We are finding first valid index

---

# 🏁 Final Takeaway

This problem teaches:

- Modified Binary Search
- Finding first valid index
- Lower Bound concept
- Binary Search on condition

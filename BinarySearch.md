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

# 🔎 Problem: Find in Mountain Array

## 📌 Problem Statement

A mountain array is defined as:

- Strictly increasing until a peak
- Then strictly decreasing

Given a mountain array and a target value,
return the index of target.
If not found, return -1.

Time complexity must be O(log n).

---

# 🧠 First Thoughts

- Array is not fully sorted.
- But it has structure.
- There is a peak element.
- Left side is sorted ascending.
- Right side is sorted descending.

So we can:

1️⃣ Find peak  
2️⃣ Binary search left  
3️⃣ Binary search right  

---

# 🐢 Phase 1 — Brute Force

## 💡 Idea

Traverse entire array and return index if found.

## ⏱ Time Complexity
O(n)

## 💾 Space Complexity
O(1)

---

# 🚀 Phase 2 — Optimal Approach

## 🔥 Step 1: Find Peak Element

Peak is the element where:

nums[mid] > nums[mid + 1]

Binary Search logic:

If nums[mid] < nums[mid + 1]
→ Peak is on right side

Else
→ Peak is on left side (including mid)

This works because peak always exists.

---

## ⏱ Time Complexity (Peak)
O(log n)

---

## 🔍 Step 2: Binary Search on Left (Ascending)

Normal binary search.

---

## 🔍 Step 3: Binary Search on Right (Descending)

Binary search but reverse comparison:

If nums[mid] > target
→ Move right (since decreasing)

If nums[mid] < target
→ Move left

---

# ⚡ Complete Algorithm

1. Find peak index
2. Search in [0, peak]
3. If not found, search in [peak+1, n-1]

---

# 💻 C++ Code — Optimal

```cpp
class Solution {
public:
    
    int findPeak(vector<int>& arr) {
        int left = 0;
        int right = arr.size() - 1;
        
        while(left < right) {
            int mid = left + (right - left) / 2;
            
            if(arr[mid] < arr[mid + 1]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return left; // peak index
    }
    
    int binarySearchAsc(vector<int>& arr, int left, int right, int target) {
        while(left <= right) {
            int mid = left + (right - left) / 2;
            
            if(arr[mid] == target)
                return mid;
            
            if(arr[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        
        return -1;
    }
    
    int binarySearchDesc(vector<int>& arr, int left, int right, int target) {
        while(left <= right) {
            int mid = left + (right - left) / 2;
            
            if(arr[mid] == target)
                return mid;
            
            if(arr[mid] > target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        
        return -1;
    }
    
    int findInMountainArray(vector<int>& arr, int target) {
        
        int peak = findPeak(arr);
        
        int leftResult = binarySearchAsc(arr, 0, peak, target);
        if(leftResult != -1)
            return leftResult;
        
        return binarySearchDesc(arr, peak + 1, arr.size() - 1, target);
    }
};
```

---

# ⏱ Time Complexity

Peak: O(log n)  
Left Search: O(log n)  
Right Search: O(log n)

Total: **O(log n)**

---

# 🧩 Edge Cases

- Target is peak
- Target only on right side
- Target only on left side
- Target not present

---

# 🎯 Pattern Recognition

Use this approach when:

- Array increases then decreases
- Asked for O(log n)
- Structure is partially sorted

---

# 🏁 Final Takeaway

This problem teaches:

- Binary search on structure
- Finding peak efficiently
- Handling increasing + decreasing arrays
- Breaking problem into smaller searches


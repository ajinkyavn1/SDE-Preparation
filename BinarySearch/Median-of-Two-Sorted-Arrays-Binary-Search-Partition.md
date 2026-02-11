# Median of Two Sorted Arrays

---

## 1️⃣ Problem Summary

We are given two sorted arrays.

We must find the median of the combined sorted array.

Constraints:
- Arrays are already sorted.
- Required time complexity: O(log(m + n)).

---

## 2️⃣ Brute Force Approach

### Idea 1 — Combine and Sort

- Merge both arrays into one.
- Sort the combined array.
- Compute median.

Time Complexity: O((m+n) log(m+n))  
Space Complexity: O(m+n)

Not optimal.

---

### Idea 2 — Merge Using Two Pointers

Since arrays are sorted:

- Use two pointers.
- Merge like merge-sort.
- Stop once median position is reached.

Time Complexity: O(m + n)  
Space Complexity: O(m + n)

Still not acceptable because we need O(log(m+n)).

---

## 3️⃣ Key Observation

Median splits the combined array into:

- Left half
- Right half

Left half size:

(m + n + 1) / 2

We will:

- Pick some elements from array1 for the left half.
- Remaining elements must come from array2.

If we take:

elementsFromFirst = x

Then:

elementsFromSecond = leftHalfSize - x

We must ensure:

max(left side) <= min(right side)

That means:

firstLeftValue  <= secondRightValue  
AND  
secondLeftValue <= firstRightValue  

If this condition is true, partition is correct.

---

## 4️⃣ Why Binary Search Works

We binary search on how many elements we take from the first array.

If:

firstLeftValue > secondRightValue  
→ we took too many from first array  
→ move left

If:

secondLeftValue > firstRightValue  
→ we took too few from first array  
→ move right

This removes half the search space each time.

Time Complexity: O(log(min(m, n)))

---

## 5️⃣ Final Implementation (Clean & Readable)

```cpp
double findMedianSortedArrays(vector<int>& firstArray,
                              vector<int>& secondArray) {
    
    // Always binary search on smaller array
    if (firstArray.size() > secondArray.size()) {
        return findMedianSortedArrays(secondArray, firstArray);
    }

    int size1 = firstArray.size();
    int size2 = secondArray.size();

    int low = 0;
    int high = size1;

    while (low <= high) {

        int elementsFromFirst  = low + (high - low) / 2;
        int elementsFromSecond = (size1 + size2 + 1) / 2 - elementsFromFirst;

        int firstLeftValue  = (elementsFromFirst == 0)
                                ? INT_MIN
                                : firstArray[elementsFromFirst - 1];

        int firstRightValue = (elementsFromFirst == size1)
                                ? INT_MAX
                                : firstArray[elementsFromFirst];

        int secondLeftValue  = (elementsFromSecond == 0)
                                ? INT_MIN
                                : secondArray[elementsFromSecond - 1];

        int secondRightValue = (elementsFromSecond == size2)
                                ? INT_MAX
                                : secondArray[elementsFromSecond];

        // Correct partition
        if (firstLeftValue <= secondRightValue &&
            secondLeftValue <= firstRightValue) {

            if ((size1 + size2) % 2 == 0) {
                return (max(firstLeftValue, secondLeftValue) +
                        min(firstRightValue, secondRightValue)) / 2.0;
            } else {
                return max(firstLeftValue, secondLeftValue);
            }
        }

        // Too many elements taken from first array
        else if (firstLeftValue > secondRightValue) {
            high = elementsFromFirst - 1;
        }

        // Too few elements taken from first array
        else {
            low = elementsFromFirst + 1;
        }
    }

    return 0.0; // Safety return
}
```

---

## 6️⃣ What This Problem Teaches

- Binary search on partition, not values
- Careful boundary handling
- Thinking in terms of halves
- Controlling search space logically

---

## 7️⃣ Pattern Recognition

Use this idea when:

- Two sorted arrays
- Asked for median
- Required O(log(m+n))
- Problem involves dividing into equal halves

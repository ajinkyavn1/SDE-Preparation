# DSA Algorithm Templates – C++ (With Comments)

Clean C++ templates with explanation comments.

---

# 1️⃣ Kadane’s Algorithm

### 🔹 Use When:

* Maximum / Minimum subarray sum
* Contiguous subarray problems

### ⏱ Time: O(n) | Space: O(1)

```cpp
// Maximum Subarray Sum
int kadane(vector<int>& nums) {
    int maxSum = INT_MIN;   // Stores final answer
    int currentSum = 0;     // Running sum

    for (int num : nums) {
        // Either extend previous subarray or start new
        currentSum = max(num, currentSum + num);
        
        // Update global maximum
        maxSum = max(maxSum, currentSum);
    }

    return maxSum;
}
```

---

# 2️⃣ Moore’s Voting Algorithm

### 🔹 Use When:

* Majority element (> n/2 times)
* Majority is guaranteed

### ⏱ Time: O(n) | Space: O(1)

```cpp
int majorityElement(vector<int>& nums) {
    int candidate = -1;
    int count = 0;

    for (int num : nums) {
        if (count == 0) {
            candidate = num;   // Choose new candidate
        }
        
        // Increase if same, decrease if different
        count += (num == candidate) ? 1 : -1;
    }

    return candidate;  // Do second pass if majority not guaranteed
}
```

---

# 3️⃣ Dutch National Flag Algorithm

### 🔹 Use When:

* Array contains only 0,1,2
* 3-way partitioning

### ⏱ Time: O(n)

```cpp
void sortColors(vector<int>& nums) {
    int low = 0, mid = 0;
    int high = nums.size() - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums[low], nums[mid]);
            low++;
            mid++;
        }
        else if (nums[mid] == 1) {
            mid++;  // Already in correct region
        }
        else {
            swap(nums[mid], nums[high]);
            high--;
        }
    }
}
```

---

# 4️⃣ Binary Search

## A) Vanilla Binary Search

### 🔹 Use When:

* Sorted array
* Exact element search

```cpp
int binarySearch(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;  // Prevent overflow

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return -1;  // Not found
}
```

---

## B) Binary Search on Answer Space

### 🔹 Use When:

* Minimize maximum
* Maximize minimum
* Feasible / Not feasible pattern

```cpp
bool feasible(vector<int>& arr, int mid) {
    // Define problem-specific feasibility logic
    return true;
}

int binarySearchAnswer(vector<int>& arr) {
    int low = 1, high = 1e9;
    int answer = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (feasible(arr, mid)) {
            answer = mid;
            high = mid - 1;   // Try smaller answer
        } else {
            low = mid + 1;
        }
    }

    return answer;
}
```

---

# 5️⃣ Two Pointers

### 🔹 Use When:

* Sorted arrays
* Pair sum problems

```cpp
pair<int,int> twoPointers(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target)
            return {left, right};
        else if (sum < target)
            left++;      // Need bigger sum
        else
            right--;     // Need smaller sum
    }

    return {-1, -1};
}
```

---

# 6️⃣ Sliding Window

## A) Fixed Size Window

### 🔹 Use When:

* Subarray of size K

```cpp
int maxSumK(vector<int>& nums, int k) {
    int windowSum = 0;

    // First window
    for (int i = 0; i < k; i++)
        windowSum += nums[i];

    int maxSum = windowSum;

    // Slide window
    for (int i = k; i < nums.size(); i++) {
        windowSum += nums[i] - nums[i - k];
        maxSum = max(maxSum, windowSum);
    }

    return maxSum;
}
```

---

## B) Variable Size Window

### 🔹 Use When:

* Longest substring
* Sum <= K

```cpp
int variableWindow(vector<int>& nums, int k) {
    int left = 0;
    int sum = 0;
    int maxLen = 0;

    for (int right = 0; right < nums.size(); right++) {
        sum += nums[right];  // Expand window

        while (sum > k) {    // Shrink window
            sum -= nums[left];
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```

---

# 7️⃣ Prefix Sum

### 🔹 Use When:

* Range sum queries
* Subarray sum = K

```cpp
vector<int> buildPrefix(vector<int>& nums) {
    vector<int> prefix(nums.size() + 1, 0);

    for (int i = 0; i < nums.size(); i++)
        prefix[i + 1] = prefix[i] + nums[i];

    return prefix;
}
```

### Subarray Sum = K

```cpp
int subarraySum(vector<int>& nums, int k) {
    unordered_map<int,int> freq;
    freq[0] = 1;

    int prefixSum = 0;
    int count = 0;

    for (int num : nums) {
        prefixSum += num;

        if (freq.count(prefixSum - k))
            count += freq[prefixSum - k];

        freq[prefixSum]++;
    }

    return count;
}
```

---

# 🔥 Combination Guide

| Problem Type      | Best Technique       | Can Combine With |
| ----------------- | -------------------- | ---------------- |
| Max Subarray      | Kadane               | Prefix Sum       |
| Majority Element  | Moore                | HashMap          |
| 3-way Partition   | Dutch Flag           | Two Pointers     |
| Search in Sorted  | Binary Search        | Two Pointers     |
| Optimization      | Binary Search Answer | Greedy           |
| Pair Sum          | Two Pointers         | Binary Search    |
| Subarray size K   | Fixed Window         | Prefix Sum       |
| Longest Substring | Variable Window      | HashMap          |
| Range Query       | Prefix Sum           | Sliding Window   |

---

# 🎯 Quick Interview Decision Tree

1. Is array sorted? → Binary Search / Two Pointers
2. Is subarray contiguous? → Sliding Window / Kadane
3. Is it optimization (min/max)? → Binary Search on Answer
4. Is majority element? → Moore
5. Exactly 3 categories? → Dutch Flag
6. Multiple range queries? → Prefix Sum

---

End of C++ Template Collection ✅

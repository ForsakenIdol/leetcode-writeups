# Rotate Array

This question was not numbered. It can be found [**here**](https://leetcode.com/explore/featured/card/top-interview-questions-easy/92/array/646/).

## Solution 1 - Naive Iteration (C++)

```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        for (int r = 0; r < k % nums.size(); r++) {
            int temp = nums[0];
            for (int i = 1; i < nums.size(); i++) {
                swap(temp, nums[i]);
            }
            nums[0] = temp;
        }
    }
};
```

This solution executes a full singular rotation on the vector, `k % nums.size()` times. We do not need to perform the full `k` rotations since after `nums.size()` rotations, the vector is back to its original state.

This solution times out on extremely long inputs because of the double `for` loop. If the length of the vector is `N`, it has a time complexity of `O(N ^ N)` (where the worst case is achieved when `k = nums.size()`), but a space complexity of `O(1)` since all rotations are happening in-place with a single external `temp` variable.

## Solution 2 - Reversal (C++)

```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        k = k % nums.size();
        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + k);
        reverse(nums.begin() + k, nums.end());
    }
};
```

This solution works by combining 2 known facts about the state of `nums` after `k` rotations (again, assuming we've calculated `k % nums.size()`).

- There are 2 subvectors in the final, rotated vector. The first subvector is comprised of the last `k` integers from the back of the original vector. The second subvector is the first `nums.size() - k` integers.
- The order of elements in each subvector is preserved.

By reversing the elements in the entire vector, we guarantee that the last `k` integers are moved to the front, and vice versa, although their relative ordering has been reversed. To fix the ordering we reverse the first subvector (which consists of `k` integers), then we reverse the second subvector independently.
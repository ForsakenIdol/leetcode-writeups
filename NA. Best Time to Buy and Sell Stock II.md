# Best Time to Buy and Sell Stock II

This question was not numbered. It can be found [**here**](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/564/).

## My Solution (C++)

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int start = 0, end = 0, profit = 0;
        while (end < prices.size() - 1) {
            end++;
            if (prices[end - 1] > prices[end]) {
                profit += (prices[end - 1] - prices[start]);
                start = end;
            }
        }
        if (start != end) profit += prices[end] - prices[start];
        return profit;
    }
};
```

We adopt a dynamic sliding window approach, looking for contiguous subsequences of numbers in the vector which are in ascending order.

Everytime `end` is incremented, we check to see if the value at the index it has been incremented to is smaller than the previous value. If this is so, the ascending contingency has been broken (and so the current window is invalid), so we calculate the previous window's profit as `prices[end - 1] - prices[start]`, add this value to `profit`, and reset the window by moving `start` up to where `end` is.

If the final vector is constantly incrementing, `start` will not only be before the `end` of the vector, but the profit from this most recent contiguous sequence will not yet have been recorded in `profit`, which means this will have to be added outside the main `while` loop.
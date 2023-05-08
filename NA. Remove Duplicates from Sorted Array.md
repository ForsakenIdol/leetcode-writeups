# Remove Duplicates from Sorted Array

This question was not numbered. It can be found [**here**](https://leetcode.com/explore/featured/card/top-interview-questions-easy/92/array/727/).

## My Solution (C++)

```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        auto it = nums.begin() + 1;
        while (it != nums.end()) {
            *it == *(it - 1) ? nums.erase(it) : it++;
        }
        return nums.size();
    }
};
```

The reason why we use an **iterator** (declared with the `auto` keyword instead of `std::vector<int>::iterator` since the latter is much too long and this is a type that can be inferred) and not a plain `int i` index is down to 2 reasons.

1. The question explicitly states to  remove the duplicates **in-place**. For this, C++ exposes a vector `erase` public method.
2. The `erase` method takes an iterator argument - not an index argument - to specify which element is to be removed from the vector.

Remember that in C++, an iterator is a pointer to the object at the location over which the iterator object is iterating. Therefore, to find the object that is at the iterator's location, we need to [**dereference**](https://www.w3schools.com/cpp/cpp_pointers_dereference.asp) the pointer with the `*` symbol.
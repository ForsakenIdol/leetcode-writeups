# Miscellaneous Notes

- C++ vectors can be explicitly declared simply with `{ item1, item2, item3, ... }` for a return statement.
- C++ has a `goto label` feature.

```C++
for (int i = 0; i < arbitrary_end; i++) {
    do_something();
    if (condition_is_met) goto label1;
}

label1:
    do_something_else();
    return something;
```
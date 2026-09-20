# Reverse Degree of a String

## Problem

Given a string `s`, calculate its **reverse degree**.

For each character:

* `'a' = 26`
* `'b' = 25`
* ...
* `'z' = 1`

Multiply the character's **reverse alphabet value** by its **1-indexed position** in the string.

Return the sum of all products.

## Approach

The main idea is to calculate the **reverse alphabet value** of each character and multiply it by its position.

### 1. Find the reverse alphabet value

Normally:

```text
'a' = 1
'b' = 2
...
'z' = 26
```

For the reverse alphabet:

```text
'a' = 26
'b' = 25
...
'z' = 1
```

We can calculate it using:

```cpp
26 - (s[i] - 'a')
```

For example:

```text
s[i] = 'a'

'a' - 'a' = 0

26 - 0 = 26
```

For `'c'`:

```text
'c' - 'a' = 2

26 - 2 = 24
```

### 2. Find the position in the string

The problem uses **1-indexed positions**.

But C++ loops are **0-indexed**:

```cpp
i = 0, 1, 2, ...
```

So the string position is:

```cpp
i + 1
```

### 3. Calculate the product

For every character:

```cpp
reverse_value * (i + 1)
```

Then add it to `sum`.

## Code

```cpp
class Solution {
public:
    int reverseDegree(string s) {

        int sum = 0;
        int n = s.size();

        for(int i = 0; i < n; i++) {

            // Find reverse alphabet value
            int reverse_value = 26 - (s[i] - 'a');

            // String position is 1-indexed
            int position = i + 1;

            // Calculate product
            int product = reverse_value * position;

            // Add to answer
            sum += product;
        }

        return sum;
    }
};
```

## Example

For:

```text
s = "abc"
```

| Character | Reverse Value | Position | Product |
| --------- | ------------: | -------: | ------: |
| `a`       |            26 |        1 |      26 |
| `b`       |            25 |        2 |      50 |
| `c`       |            24 |        3 |      72 |

Therefore:

```text
26 + 50 + 72 = 148
```

## Key Idea

```text
Character
    ↓
Find Reverse Alphabet Value
    ↓
Multiply by (i + 1)
    ↓
Add to sum
```

The formula is:

```cpp
reverse_value = 26 - (s[i] - 'a');
```

and:

```cpp
sum += reverse_value * (i + 1);
```

## Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`

where `n` is the length of the string.

## Revision Shortcut

**Reverse Value → Position → Multiply → Add**

### Important

Remember:

```text
C++ index     → i
String position → i + 1
```

And:

```text
Normal alphabet:
'a' = 1

Reverse alphabet:
'a' = 26
```

So:

```cpp
26 - (s[i] - 'a')
```

gives the reverse alphabet value.

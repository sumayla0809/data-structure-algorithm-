# Remove Duplicates from Sorted Array

## Problem

Given an integer array `nums` sorted in **non-decreasing order**, remove duplicates **in-place** so that each unique element appears only once.

Return the number of unique elements `k`.

After removing duplicates:

* The first `k` elements of `nums` must contain the unique elements.
* The elements after index `k - 1` can be ignored.
* The relative order must remain the same.

## Approach

Since the array is **sorted**, all duplicate elements are next to each other.

We can use the **Two Pointer** technique.

We use:

* `i` → points to the position where the next unique element should be placed.
* `j` → scans the array to find new unique elements.

### 1. Initialize the first unique element

The first element is always unique:

```cpp
int i = 0;
```

### 2. Traverse using `j`

Start `j` from index `1`.

For every element:

```cpp
if(nums[j] != nums[i])
```

it means we found a **new unique element**.

Move `i` forward and put the new element there:

```cpp
i++;
nums[i] = nums[j];
```

If:

```cpp
nums[j] == nums[i]
```

then it is a duplicate, so we simply ignore it.

### 3. Return the number of unique elements

`i` is the index of the last unique element.

Therefore, the number of unique elements is:

```cpp
i + 1
```

## Code

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {

        int i = 0;

        for(int j = 1; j < nums.size(); j++) {

            // Found a new unique element
            if(nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }

        return i + 1;
    }
};
```

## Example

For:

```text
nums = [0,0,1,1,1,2,2,3,3,4]
```

Initially:

```text
i = 0
     ↓
[0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
```

`j` scans the array.

When `j` finds `1`:

```text
nums[j] != nums[i]
```

so move `i` and place `1`:

```text
[0, 1, 1, 1, 1, 2, 2, 3, 3, 4]
   ↑
   i
```

Continue the same process.

Finally:

```text
[0,1,2,3,4,_,_,_,_,_]
```

and:

```text
k = 5
```

## Key Idea

Because the array is sorted:

```text
Duplicates → adjacent
```

So we only need to compare the current element with the **last unique element**.

```text
i → last unique element
j → current element
```

```text
j finds a new element
        ↓
      i++
        ↓
nums[i] = nums[j]
```

## Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`

We modify the array directly, so no extra array is required.

## Revision Shortcut

**Sorted Array → Two Pointers → Compare → Move Unique**

Remember:

```text
i = position for unique elements
j = scanner
```

### Important

The answer is:

```cpp
return i + 1;
```

because `i` is an **index**, while `k` is a **count**.

```text
Index:  0  1  2  3  4
Array: [0, 1, 2, 3, 4]

i = 4
k = i + 1 = 5
```

### Pattern to Remember

```cpp
if(nums[j] != nums[i]) {
    i++;
    nums[i] = nums[j];
}
```

This is a very common **Two Pointer + In-place modification** pattern.

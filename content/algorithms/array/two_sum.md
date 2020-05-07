+++
title = "Two Sum"
date = 2020-05-06
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Raymond Sheng"]
+++

## To solve this problem

1. Create a hashmap that will map number => index. Alternatively, map complement => index.
2. Enumerate across the array, checking if the number's complement or the number is in the map.
    * If so return the current number's index and the mapped index.
    * Else add the number or complement to the hashmap
3. Return an empty array if a match was not found.

## Complexity analysis

### Time: O(N)

The program does a single pass through the array.

### Space: O(N)

The program stores a dictionary that in the worst case (no two sum is found) will have a key value pair of every single number and its index.

## Python solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        num_to_index = {}

        for i, num in enumerate(nums):
            if target - num in num_to_index:
                return [num_to_index[target-num], i]
            else:
                num_to_index[num] = i

        return []
```

## Go solution

```go
func twoSum(nums []int, target int) []int {

    num_to_index := make(map[int]int)

    for i, num := range nums {
        compliment_index, present := num_to_index[target-num]
        if present {
            return []int{compliment_index, i}
        } else {
            num_to_index[num] = i
        }
    }
    return []int{}
}
```

## Rust solution

```rust
use std::collections::HashMap;

impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {

        let mut num_to_index = HashMap::with_capacity(nums.len());

        for (i, num) in nums.iter().enumerate() {
            if let Some(&complement_index) = num_to_index.get(&(target-num)) {
                return vec![complement_index as i32, i as i32];
            } else {
                num_to_index.insert(num, i);
            }
        }
        vec![]
    }
}
```

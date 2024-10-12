# LEETCODE-Arrays-2406
Let's do a dry run of the `minGroups` function for a better understanding.

### Function Description:
- The problem is to find the minimum number of groups required so that no intervals overlap within the same group. 
- The function uses a **min-heap** (priority queue) to keep track of the end (`right`) times of the intervals.

### Key Steps:
1. **Sort the intervals** based on their start times.
2. Iterate over each interval:
   - If the current interval starts after the smallest end time in the heap (i.e., no overlap), we can reuse the same group by removing the smallest end time (`minHeap.poll()`).
   - In either case (whether or not we reuse a group), we add the current interval's end time to the heap (`minHeap.offer(interval[1])`).
3. The size of the heap at the end will represent the minimum number of groups required.

### Dry Run Example:

Assume the input intervals are: `[[1, 5], [2, 3], [4, 6]]`.

#### Step-by-step Execution:

1. **Sorting the intervals by start time:**
   ```
   [[1, 5], [2, 3], [4, 6]]
   ```

2. Initialize `minHeap` as an empty priority queue.

3. **First interval: [1, 5]**
   - `minHeap` is empty, so add `5` to the heap.
   - `minHeap = [5]`.

4. **Second interval: [2, 3]**
   - The start time `2` is less than the smallest end time `5` in `minHeap`. This means there is an overlap, so we need a new group.
   - Add `3` to the heap.
   - `minHeap = [3, 5]`.

5. **Third interval: [4, 6]**
   - The start time `4` is greater than the smallest end time `3` in `minHeap`, which means no overlap. We can reuse the group, so remove `3` from the heap.
   - Add `6` to the heap.
   - `minHeap = [5, 6]`.

6. **Result:**
   - At the end of the loop, the size of `minHeap` is `2`, meaning two groups are needed to accommodate the intervals.

### Final Output:
The function will return `2` as the minimum number of groups.

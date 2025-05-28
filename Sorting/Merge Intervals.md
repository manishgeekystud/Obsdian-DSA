# 🧾 Merge Intervals
## 🔍 Problem Statement

You're given an array of intervals, where each interval is represented as `[start, end]`. Your task is to **merge all overlapping intervals**.

### 🧪 Example:

**Input**: `[[1,3], [2,6], [8,10], [15,18]]`  
**Output**: `[[1,6], [8,10], [15,18]]`

Explanation:

- `[1,3]` and `[2,6]` overlap → merge to `[1,6]`
    
- Others do not overlap
    

---

## 🧠 Intuition

1. If intervals are **not sorted**, it's hard to tell which ones overlap.
    
2. So, **first sort** intervals based on the start value.
    
3. Then iterate over them:
    
    - If current interval **overlaps with the previous**, merge them.
        
    - Otherwise, add the current interval as a new entry.
        

---

## 🔑 Key Ideas

- **Sorting is essential** to bring overlapping intervals next to each other.
    
- Overlap condition: `current.start <= previous.end`
    
- Merging means: update `previous.end = max(previous.end, current.end)`
    

---

## ⚙️ Algorithm Steps

1. Sort intervals by starting time.
    
2. Initialize an empty list `result` and add the first interval to it.
    
3. For each remaining interval:
    
    - If current interval overlaps with the last one in result → merge.
        
    - Else, add it to the result as a separate interval.
        
4. Return the result.
    

---

## ✅ Java Code

```java
import java.util.*;

class MergeIntervals {
    public static int[][] merge(int[][] intervals) {
        // Step 1: Edge case
        if (intervals.length <= 1)
            return intervals;

        // Step 2: Sort intervals based on start time
        Arrays.sort(intervals, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return a[0] - b[0]; // Sort by starting point
            }
        });

        // Step 3: Create result list
        List<int[]> result = new ArrayList<>();
        
        // Initialize current interval
        int[] current = intervals[0];
        result.add(current);

        // Step 4: Traverse remaining intervals
        for (int i = 1; i < intervals.length; i++) {
            int[] next = intervals[i];

            // Check for overlap: current.end >= next.start
            if (next[0] <= current[1]) {
                // Merge by updating current interval's end
                current[1] = Math.max(current[1], next[1]);
            } else {
                // No overlap: add new interval
                current = next;
                result.add(current);
            }
        }

        // Step 5: Convert result list to 2D array
        return result.toArray(new int[result.size()][]);
    }
}

```
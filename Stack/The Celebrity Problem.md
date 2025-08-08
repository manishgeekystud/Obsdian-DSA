A celebrity is a person who is known to all but **does not know** anyone at a party. A party is being organized by some people. A square matrix **mat[][]** (n*n) is used to represent people at the party such that if an element of **row i and column j is set to 1** it means **ith person knows jth person**. You need to return the **index of the celebrity** in the party, if the celebrity does not exist, return **-1**.

**Note:** Follow **0-based** indexing.

**Examples:**

**Input:** mat[][] = [[1, 1, 0], [0, 1, 0], [0, 1, 1]]
**Output:** 1
**Explanation:** 0th and 2nd person both know 1st person. Therefore, 1 is the celebrity person. 

**Input:** mat[][] = [[1, 1], [1, 1]]
**Output:** -1
**Explanation:** Since both the people at the party know each other. Hence none of them is a celebrity person.

**Input:** mat[][] = [[1]]
**Output:** 0

**Constraints:**  
1 ≤ mat.size() ≤ 1000  
0 ≤ mat[i][j] ≤ 1  
mat[i][i] == 1

---------------------------------------------------------------------

### **Problem Statement**

A celebrity at a party is a person:

1. **Known by everyone** else.
    
2. **Knows no one** in the party.
    

We are given a **n × n** matrix `mat[][]` where:

- `mat[i][j] = 1` → person `i` knows person `j`.
    
- `mat[i][j] = 0` → person `i` does **not** know person `j`.
    

We need to **find the index** of the celebrity or return **-1** if none exists.

---

### **Example 1**

#### **Input**

`mat = [   [1, 1, 0],   
           [0, 1, 0],  
           [0, 1, 1] ]`

#### **Matrix Table**

|Person i \ Person j|0|1|2|
|---|---|---|---|
|**0**|1|1|0|
|**1**|0|1|0|
|**2**|0|1|1|

#### **Understanding**

- Person 0 → Knows 1, doesn’t know 2. ❌ (knows someone → cannot be celebrity)
    
- Person 1 → Knows no one except themselves ✅, everyone else knows 1 ✅ → Celebrity found.
    
- Person 2 → Knows 1, ❌ (knows someone → cannot be celebrity)
    

**Output:** `1`

---

### **Example 2**

csharp

CopyEdit

`mat = [   [1, 1],   [1, 1] ]`

- Both know each other → ❌ No celebrity.
    

**Output:** `-1`

---

### **Example 3**

ini

CopyEdit

`mat = [   [1] ]`

- Only one person, they are trivially a celebrity.
    

**Output:** `0`

---

## **Brute Force Approach**

### **Idea**

For each person `i`:

1. Check that they **don’t know anyone** (`mat[i][j] == 0` for all `j ≠ i`).
    
2. Check that **everyone knows them** (`mat[j][i] == 1` for all `j ≠ i`).  
    If both are true → return `i`.
    

---

### **Algorithm**

1. Loop through all people `i` from 0 to n-1.
    
2. For each `i`, check **row** and **column**.
    
3. If they satisfy both conditions → celebrity.
    
4. Else → continue.
    
5. If no celebrity → return -1.
    

---

### **Time Complexity**

- Checking one person takes `O(n)` for row + `O(n)` for column → `O(2n)`.
    
- Doing it for `n` people → **O(n²)**.
    

---

### **Brute Force Code**

java

CopyEdit

`int celebrityBruteForce(int[][] mat, int n) {     for (int i = 0; i < n; i++) {         boolean knowsSomeone = false;         boolean everyoneKnows = true;                  for (int j = 0; j < n; j++) {             if (i != j && mat[i][j] == 1) knowsSomeone = true;             if (i != j && mat[j][i] == 0) everyoneKnows = false;         }                  if (!knowsSomeone && everyoneKnows) return i;     }     return -1; }`

---

## **Optimal Approach — Stack Method (Your Solution)**

### **Idea**

Instead of checking everyone individually, we can **eliminate non-celebrities** in pairs until only one candidate remains.

---

### **Steps**

1. Push all people (0 to n-1) onto a stack.
    
2. While more than 1 person in stack:
    
    - Pop two persons `A` and `B`.
        
    - If `A` knows `B` → `A` cannot be celebrity → push `B` back.
        
    - Else → `B` cannot be celebrity → push `A` back.
        
3. Now we have **one candidate** left.
    
4. Verify the candidate:
    
    - Candidate knows no one.
        
    - Everyone knows candidate.
        
5. If both true → return candidate, else → `-1`.
    

---

### **Why It Works**

- In each comparison, we remove **one non-celebrity**.
    
- At the end, only **possible celebrity** remains.
    
- Verification ensures correctness.
    

---

### **Time Complexity**

- **Finding candidate:** `O(n)` comparisons.
    
- **Verification:** `O(n)` checks.
    
- **Total:** `O(n)` → much better than brute force `O(n²)`.
    

---

### **Your Code with Comments**

java

CopyEdit

`class Solution {     int celebrity(int mat[][], int n) {         Stack<Integer> st = new Stack<>();                  // Step 1: Push all people into stack         for (int i = 0; i < n; i++) {             st.push(i);         }                  // Step 2: Eliminate non-celebrities         while (st.size() > 1) {             int A = st.pop();             int B = st.pop();                          if (mat[A][B] == 1) {                 // A knows B → A cannot be celebrity                 st.push(B);             } else {                 // A does not know B → B cannot be celebrity                 st.push(A);             }         }                  // Step 3: Possible celebrity         int candidate = st.pop();                  // Step 4: Verify candidate         for (int i = 0; i < n; i++) {             if (i != candidate) {                 if (mat[candidate][i] == 1 || mat[i][candidate] == 0) {                     return -1; // Fails condition                 }             }         }                  return candidate; // Celebrity found     } }`

---

### **Dry Run for Example**

**Input:**

ini

CopyEdit

`mat = [   [1, 1, 0],   [0, 1, 0],   [0, 1, 1] ] n = 3`

**Step-by-step:**

- Stack = `[0, 1, 2]`
    
- Pop 2 & 1 → `mat[2][1] == 1` → 2 knows 1 → remove 2, push 1 → Stack = `[0, 1]`
    
- Pop 1 & 0 → `mat[1][0] == 0` → 1 does not know 0 → remove 0, push 1 → Stack = `[1]`
    
- Candidate = 1
    
- Verify:
    
    - Row of 1 → knows no one ✅
        
    - Column of 1 → everyone knows 1 ✅
        

**Output:** `1`

---

### **Key Takeaways**

- Brute force is easy to understand but slow (`O(n²)`).
    
- Stack elimination reduces to `O(n)`.
    
- Always verify the last candidate.
    
- Matrix table helps in understanding who knows whom.
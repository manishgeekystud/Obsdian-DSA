
Given an array **arr[]** of size **N** where every element is in the range from **0 to n-1**. Rearrange the given array so that the transformed array **arrT[i]** becomes **arr[arr[i]]**.

**NOTE:** **arr** and **arrT** are both same variables, representing the array before and after transformation respectively.

**Example 1:  
**

**Input:**
N = 2
arr[] = [1,0]
**Output:** 0 1
**Explanation:** 
arr[arr[0]] = arr[1] = 0
arr[arr[1]] = arr[0] = 1  
So, arrT becomes {0, 1}

**Example 2:**

**Input:**
N = 5
arr[] = [4,0,2,1,3]
**Output:** 3 4 2 0 1
**Explanation:** 
arr[arr[0]] = arr[4] = 3
arr[arr[1]] = arr[0] = 4  
arr[arr[2]] = arr[2] = 2  
arr[arr[3]] = arr[1] = 0  
arr[arr[4]] = arr[3] = 1  
and so on  
So, arrT becomes {3, 4, 2, 0, 1}

**Constraints:**  
1 <= N <= 105  
0 <= arr[i] < N



## 💡 Problem Recap (Desi Style)

> Bhai, tere paas ek array hai `arr[]`, jismein har number ek index ko point karta hai.  
> Tujhe ye karna hai ki:  
> **`arr[i] = arr[arr[i]]`**  
> Par **bina kisi extra memory ke** — sirf usi array ke andar **jugaad** se karna hai.

---

## 🔧 Constraints (Soch samajh ke):

     - All values in `arr[]` are from `0` to `n-1`
     - You **can’t use any extra array** (O(1) space)
     - You must do this in-place and in O(n) time**
    

---

**Brute Force**
 void arrange(long long arr[], int n) {
        // Your code here
        int i;
        int temp[n];
        for(i=0;i<n;i++)
            temp[i] = arr[arr[i]];
        for(i=0;i<n;i++)
            arr[i] = temp[i];
    }

**Efficient /Actual Solution** 
## 🧠 Desi Jugaad Idea: Store Two Values in One

> Bhai, jab kisi cheez mein jagah kam ho, toh **ek hi dabbe (array cell)** mein **do cheezen chipka de**.

And that’s the **magic trick here**.

---

## 🎩 The Trick (Desi Explanation):

Imagine this:

- Har `arr[i]` mein tum **do values** chipka rahe ho:
    
    - **Old value** → `arr[i] % n`
        
    - **New value** → `(arr[arr[i]] % n) * n`
        

So final value:
`arr[i] = old + new * n`

To get new value later:

`arr[i] = arr[i] / n`

💥 Ye hai **desi jugaad**! Ek hi number mein dono value, original bhi aur naya bhi.

---

## 🛠 Code with Comments:

```
static void arrange(long arr[], int n) {
    // Step 1: Encode new value into current element
    for (int i = 0; i < n; i++) {
        // Store: old + (new % n) * n
        arr[i] = arr[i] + (arr[(int)(arr[i])] % n) * n;
    }

    // Step 2: Decode new value by dividing with n
    for (int i = 0; i < n; i++) {
        arr[i] = arr[i] / n;
    }
}

```

---

## 🔄 Dry Run Example:
Let’s take:
arr = [4, 0, 2, 1, 3]
n = 5
**Step 1: Encoding**

i = 0 → arr[0] = 4 + (arr[4] % 5) * 5 = 4 + 3*5 = 19
i = 1 → arr[1] = 0 + (arr[0] % 5) * 5 = 0 + 4*5 = 20
i = 2 → arr[2] = 2 + (2 % 5) * 5     = 2 + 2*5 = 12
i = 3 → arr[3] = 1 + (0 % 5) * 5     = 1 + 0   = 1
i = 4 → arr[4] = 3 + (1 % 5) * 5     = 3 + 5   = 8

Encoded arr: [19, 20, 12, 1, 8]
**Step 2: Decoding**

arr[0] = 19 / 5 = 3
arr[1] = 20 / 5 = 4
arr[2] = 12 / 5 = 2
arr[3] = 1 / 5  = 0
arr[4] = 8 / 5  = 1
✅ Final Answer:
[3, 4, 2, 0, 1]


---

## 🧠 How to Remember This (Desi Style Recap)

> Bhai yaad rakh — **naya value leke usko bada bana aur chipka de**  
> `"arr[i] = old + new % n * n"`  
> Phir baad mein `"arr[i] / n"` se **naya value nikaal le**  
> Ek hi dabbe mein dono kaam ho gaya — Desi jugaad zindabad 😎
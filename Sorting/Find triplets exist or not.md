### Problem Statement:

> Given an array `arr[]`, check if there exists a triplet `(i, j, k)` such that `arr[i] + arr[j] + arr[k] == 0`.

---

## 🧠 Intuition

- Sort the array.
    
- Fix one element at a time (say `arr[i]`) and use **two pointers** to find the remaining two elements such that their sum is `-arr[i]`.
    

---

## ✅ Java Code
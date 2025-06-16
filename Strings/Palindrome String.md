Check for Palindrome in Java

---

A string is said to be a palindrome if it is the same if we start reading it from left to right or right to left. So let us consider a string “**str”**, now the task is just to find out with its reverse string is the same as it is. 

**Example:**

**Input :** str = "abba" 
**Output:** Yes

**Input :** str = "geeks"
**Output:** No


// Java Program to check Whether the String is Palindrome
// or Not

// Main class
class GFG {

	// Method 1
	// Returns true if string is a palindrome
	static boolean isPalindrome(String str)
	{

		// Pointers pointing to the beginning
		// and the end of the string
		int i = 0, j = str.length() - 1;

		// While there are characters to compare
		while (i < j) {

			// If there is a mismatch
			if (str.charAt(i) != str.charAt(j))
				return false;

			// Increment first pointer and
			// decrement the other
			i++;
			j--;
		}

		// Given string is a palindrome
		return true;
	}
}


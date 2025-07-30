### 

Difficulty: **Easy**Accuracy: **76.51%**Submissions: **23K+**Points: **2**

You are given string **s**. You need to remove the consecutive duplicates from the given string using a Stack.  

**Examples:**

**Input**: s = "aaaaaabaabccccccc"
**Output**: ababc
**Explanation**: The order is in the following way 6->a, 1->b, 2->a, 1->b, 7->c. So, only one element from each group will remain and rest all are removed. Therefore, final string will be:- ababc.

**Input**: s = "abbccbcd"
**Output**: abcbcd
**Explanation**: The order is in the following way 1->a, 2->b, 2->c, 1->b, 1->c, 1->d. So, only one element from each group will remain and rest all are removed. Therefore, final string will be:- abcbcd.

-------------------------------------------------------------------

```java
 public static String removeConsecutiveDuplicates(String s) {
        // Your code here
        Stack<Character> st= new Stack<>();
       if(s.length()==0 || s==null)
       return "";
       st.push(s.charAt(0));
        for(int i=1;i<s.length();i++)
        {
            if(st.peek()!=s.charAt(i))
              st.push(s.charAt(i));
        }
        StringBuilder sb=new StringBuilder();
        for(char ch:st)
        {
            sb.append(ch);
        }
        return sb.toString();
    }
```
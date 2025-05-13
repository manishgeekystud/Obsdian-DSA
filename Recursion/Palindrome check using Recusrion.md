public class Palindrome {
    
    // Recursive method to check if a string is a palindrome
    public static boolean isPalindrome(String str, int start, int end) {
        // Base case: If the start index is greater than or equal to the end index, it's a palindrome
        if (start >= end) {
            return true;
        }
        
        // If characters at start and end are not the same, it's not a palindrome
        if (str.charAt(start) != str.charAt(end)) {
            return false;
        }
        
        // Recursively check the next inner substring
        return isPalindrome(str, start + 1, end - 1);
    }
    
    public static void main(String[] args) {
        // Example string to check
        String str = "madam";
        
        // Check if the string is a palindrome using recursion
        boolean result = isPalindrome(str, 0, str.length() - 1);
        
        // Output the result
        if (result) {
            System.out.println(str + " is a palindrome.");
        } else {
            System.out.println(str + " is not a palindrome.");
        }
    }
}

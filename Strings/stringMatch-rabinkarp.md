# (GFG) Search Pattern (Rabin-Karp Algorithm)

Given two strings, one is a text string and other is a pattern string. The task is to print the indexes of all the occurences of pattern string in the text string. For printing, Starting Index of a string should be taken as 1. The strings will only contain lowercase English alphabets ('a' to 'z').

Example 1:

Input: 
text = "birthdayboy"
pattern = "birth"
Output: 
[1]
Explanation: 
The string "birth" occurs at index 1 in text.
Example 2:

Input:
text = "geeksforgeeks"
pattern = "geek"
Output: 
[1, 9]
Explanation: 
The string "geek" occurs twice in text, one starts are index 1 and the other at index 9.
Your Task:
You don't need to read input or print anything. Your task is to complete the function search() which takes the string text and the string pattern as input and returns an array denoting the start indices (1-based) of substring pattern in the string text. 

Expected Time Complexity: O(|text| + |pattern|).
Expected Auxiliary Space: O(1).

Constraints:
1<=|text|<=5*105
1<=|pattern|<=|text|

# Solution 

```java

class Solution
{
    
    int hash(String s) {
        int value = 0;
        for (int i = 0; i < s.length(); i++) {
            value += (int)s.charAt(i);
        }
        
        return value;
    }
    
    int hashText(int prevH, int prevCh, int newCh, String s) {
        prevH -= (int)s.charAt(prevCh);
        prevH += (int)s.charAt(newCh);
        
        return prevH;
    } 
    
    ArrayList<Integer> search(String pattern, String text)
    {
        // your code here
        ArrayList<Integer> ans = new ArrayList<>();
        int hashP= hash(pattern);
        int n = pattern.length();
        
        int prevHashT = 0;
        int hashT = 0;
        for (int i = 0; i <= text.length() - n; i++) {
            if (i == 0) hashT = hash(text.substring(i, n + i));
            else {
                prevHashT = hashT;
                hashT = hashText(prevHashT, i - 1, n + i - 1, text);
            }
            
            if (hashT == hashP) {
                if (pattern.equals(text.substring(i, n + i))) ans.add(i + 1);
            }
        }  
        
        return ans;
    }
}

```

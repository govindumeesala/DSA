# (GFG) maximum index

Given an array a of n positive integers. The task is to find the maximum of j - i subjected to the constraint of a[i] < a[j] and i < j.

Example 1:

Input:
n = 2
a[] = {1, 10}
Output:
1
Explanation:
a[0] < a[1] so (j-i) is 1-0 = 1.
Example 2:

Input:
n = 9
a[] = {34, 8, 10, 3, 2, 80, 30, 33, 1}
Output:
6
Explanation:
In the given array a[1] < a[7] satisfying the required condition(a[i] < a[j]) thus giving the maximum difference of j - i which is 6(7-1).
Your Task:
The task is to complete the function maxIndexDiff() which finds and returns maximum index difference. Printing the output will be handled by driver code. 

Expected Time Complexity: O(N)
Expected Auxiliary Space: O(N)

Constraints:
1 ≤ n ≤ 106
0 ≤ a[i] ≤ 109

# solution

```java

class Solution{
    
    // Function to find the maximum index difference.
    static int maxIndexDiff(int arr[], int n) { 
        if(n==1){
            return 0;
        }
        int RMax[] = new int[n]; 
        int LMin[] = new int[n]; 
        
        //Constructing LMin[] such that LMin[i] stores the minimum value 
        //from (arr[0], arr[1], ... arr[i]).
        LMin[0] = arr[0];
        for (int i = 1; i < n; ++i) 
            LMin[i] = Integer.min(arr[i], LMin[i - 1]);
            
        //Constructing RMax[] such that RMax[j] stores the maximum value 
        //from (arr[j], arr[j+1], ..arr[n-1]). 
        RMax[n - 1] = arr[n - 1]; 
        for (int j = n - 2; j >= 0; --j)
            RMax[j] = Integer.max(arr[j], RMax[j + 1]); 
            
        int i = 0, j = 0, maxDiff = -1; 
        //Traversing both arrays from left to right to find optimum j-i.
        //This process is similar to merge() of MergeSort.
        while (j < n && i < n) { 
            if (LMin[i] <= RMax[j]) { 
                //Updating the maximum difference.
                maxDiff = Integer.max(maxDiff, j - i); 
                j++; 
            } else
                i++;
        }
        //returning the maximum difference.
        return maxDiff; 
    }
}

``` 

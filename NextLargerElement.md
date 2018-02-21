## Problem setting

Given an array A [ ] having distinct elements, the task is to find the next greater element for each element of the array in order of their appearance in the array. If no such element exists, output -1 

Input:
The first line of input contains a single integer T denoting the number of test cases.Then T test cases follow. Each test case consists of two lines. The first line contains an integer N denoting the size of the array. The Second line of each test case contains N space separated positive integers denoting the values/elements in the array A[ ].
 
Output:
For each test case, print in a new line, the next greater element for each array element separated by space in order.

Constraints:
1<=T<=200
1<=N<=1000
1<=A[i]<=1000

Example:

```
Input
1
4
1 3 2 4 

Output
3 4 4 -1
```

Explanation
In the array, the next larger element to 1 is 3 , 3 is 4 , 2 is 4 and for 4 ? since it doesn't exist hence -1.

## Solution
Using a stack, in decreasing order.

```java
/*package whatever //do not write package name here */

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {
	public static void main (String[] args) {
		//code
		
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		for (int i = 0; i < n; i++) {
		    int k = scan.nextInt();
		    int[] array = new int[k];
		    for (int j = 0; j < k; j++) {
		        array[j] = scan.nextInt();
		    }
		    nextGreatNumber(array);
		}
	}
	//1 3 2 4 
	//3 4 4 -1
	public static void nextGreatNumber(int[] nums) {
	    Stack<Integer> s = new Stack<>();
	    int[] result = new int[nums.length];
	    int l;
	    for (int i = 0; i < nums.length; i++) {
	        while (!s.isEmpty() && nums[s.peek()] < nums[i]) {
	            l = s.pop();
	            result[l] = nums[i];
	        }
	        s.push(i);
	    }
	    
	    while (!s.isEmpty())
	        result[s.pop()] = -1; 
	    
	    for (int i = 0; i < result.length; i++)
	        System.out.printf("%d ", result[i]);
	}
}
```

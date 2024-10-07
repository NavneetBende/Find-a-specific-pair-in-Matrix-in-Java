Find a specific pair in Matrix in Java
Here, in this page we will discuss the program to find a specific pair in matrix in Java Programming language. Given an n x n matrix mat[n][n] of integers, find the maximum value of mat(c, d) – mat(a, b) over all choices of indexes such that both c > a and d > b.

Find a specific pair in Matrix in C++
Method Discussed :
Method 1 : Naive Approach
Method 2 : Efficient Approach
Let’s discuss them one by one in brief,

Method 1:
For all values mat(a, b) in the matrix
Find mat(c, d) that has maximum value such that c > a and d > b.
Keeps on updating maximum value found so far.
Finally return the maximum value.
Time and Space Complexity :
Time complexity: O(N*N)
Space complexity: O(1)
Method 1 : Code in Java
Run
import java.io.*;
import java.util.*;
  
class Main
{
    static int findMaxValue(int N,int mat[][])
    {
        int maxValue = Integer.MIN_VALUE;
      
        for (int a = 0; a < N - 1; a++)
          for (int b = 0; b < N - 1; b++)
             for (int d = a + 1; d < N; d++)
               for (int e = b + 1; e < N; e++)
                  if (maxValue < (mat[d][e] - mat[a][b]))
                      maxValue = mat[d][e] - mat[a][b];
      
        return maxValue;
    }
      
    public static void main (String[] args)
    {
        int N = 5;
 
        int mat[][] = {
                      { 1, 2, -1, -4, -20 },
                      { -8, -3, 4, 2, 1 },
                      { 3, 8, 6, 1, 3 },
                      { -4, -1, 1, 7, -6 },
                      { 0, -4, 10, -5, 1 }
                   };
 
        System.out.print("Maximum Value is " + findMaxValue(N,mat));
    }
}
Output :
Maximum Value is 18
Method 2:
In this method we pre-process the matrix such that index(i, j) stores max of elements in matrix from (i, j) to (N-1, N-1) and in the process keeps on updating maximum value found so far. Then finally return the maximum value.

Method 2 : Code in Java
Run
import java.io.*;
import java.util.*;
  
class Main
{
    static int findMaxValue(int N,int mat[][])
    {

        int maxValue = Integer.MIN_VALUE;
      
        int maxArr[][] = new int[N][N];
      
        maxArr[N-1][N-1] = mat[N-1][N-1];
      
        int maxv = mat[N-1][N-1];  
        for (int j = N - 2; j >= 0; j--)
        {
            if (mat[N-1][j] > maxv)
                maxv = mat[N - 1][j];
            maxArr[N-1][j] = maxv;
        }
      
        maxv = mat[N - 1][N - 1]; 
        for (int i = N - 2; i >= 0; i--)
        {
            if (mat[i][N - 1] > maxv)
                maxv = mat[i][N - 1];
            maxArr[i][N - 1] = maxv;
        }
      
        for (int i = N-2; i >= 0; i--)
        {
            for (int j = N-2; j >= 0; j--)
            {
                
                if (maxArr[i+1][j+1] - mat[i][j] > maxValue)
                    maxValue = maxArr[i + 1][j + 1] - mat[i][j];
      
                maxArr[i][j] = Math.max(mat[i][j],Math.max(maxArr[i][j + 1], maxArr[i + 1][j]) );
            }
        }
      
        return maxValue;
    }
     
    // Driver code
    public static void main (String[] args)
    {
        int N = 5;
 
        int mat[][] = {
                      { 1, 2, -1, -4, -20 },
                      { -8, -3, 4, 2, 1 },
                      { 3, 8, 6, 1, 3 },
                      { -4, -1, 1, 7, -6 },
                      { 0, -4, 10, -5, 1 }
                   };
 
        System.out.print("Maximum Value is " + findMaxValue(N,mat));
    }
}
Output :
Maximum Value is 18

## Leetcode Problem 1267 Solution Sample

### Approach 1: Counting servers at each row and column

__Intuition__

The server that can communicate with any other server means there is at least one another server at this server's row or column. For each server, if there is another server at current row and column, we can say this server can communicate with each other. 

__Algorithms__

To implement this intution, we need to traverse the matrix twice. 

The first traversal is to figure out the number of servers at each row and each column. For ```A[i][j] = 1```, means a server occurs at the position ```(i, j)```, which will cause the number of servers at the ```i-th``` row plus 1 (```countRow[i]++```) and the number of servers at ```j-th``` column plus 1 (```countCol[j]```). The array ```countRow[i]``` represents the number of servers at the ```i-th``` row and ```countCol[j]``` represents the number of servers at ```j-th``` column.

The second traversal is to judge if a server at postion ```(i, j)``` can communicate with each other or not. Obviously, if ```i-th``` row has more than one server or ```j-th``` has more than one server, the current server can communicate with another server and the result plus one.

```
class Solution {
    public int countServers(int[][] grid) {
        int m = grid.length, n = grid[0].length, res = 0;
        int[] countRow = new int[m], countCol = new int[n];
        for(int i = 0;i < m;i++){
            for(int j = 0;j < n;j++){
                if(grid[i][j] == 0) continue;
                countRow[i]++;
                countCol[j]++;
            }
        }
        for(int i = 0;i < m;i++){
            for(int j = 0;j < n;j++){
                if(grid[i][j] == 0) continue;
                if(countRow[i] > 1 || countCol[j] > 1) res++;
            }
        }
        return res;
    }
}
```
__Complexity Analysis__

- Time Complexity:_O(M * N)_, where _M_ is the length of grid, _N_ is the length of ```grid[0]```.
The reason is that we traverse the matrix twice, the matrix has _M * N_ numbers.
- Space Complexity:_O(M + N)_.
The reason is that we need two arrays. One stores the number of servers at each row, which size is _M_. Another stores the number of servers at each column, which size is _N_.

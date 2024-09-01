## Array  
### Problem: [Next Permutation](https://leetcode.com/problems/next-permutation/description/)
A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.

Solution : 
1. STL library function can be used : 
A= vector<int>
next_permutation(A.begin(),A.end())

2. algo :
       [video](https://www.youtube.com/watch?v=JDOXKqF60RQ)

   example :
    [2,1,5,4,3,0,0]

    1. check the trend change in lexicographic order
    2. the trend change point is the breakpoint
    3. The left part or break point will be unaltered
    4. the breakpoint index should be replaced by a value that will be just greater than it which should be available right to it.
    5. after swapping the right part trend will be the same as the previous which is an increasing order from right to left.
    6. the right section should be replaced by the minimum possible value which can be possible by placing the number in increasing order from left to right.
    7. So reverse the right section.

function :
    void nextPermutation(vector<int>& nums) {
        
        int break_index=-1;
        int n=nums.size();
        
        //find break point
        for(int i=n-2;i>=0;i--)
        {
            if(nums[i]<nums[i+1])
            {
                break_index=i;
                break;
            }
        }

        //swap the break index to next possible larger value in right of break index

        if(break_index!=-1)
        {
            for(int i=n-1;i>break_index;i--)
            {
                if(nums[i]>nums[break_index])
                {
                    int temp=nums[break_index];
                    nums[break_index]=nums[i];
                    nums[i]=temp;
                    break;
                }
            }
        }

        //reverse the section right of break index
        reverse(nums.begin()+break_index+1,nums.end());

    }        

## Dynamic programming 
### Optimal Strategy For A Game ( recursion + memorisation ) 

#### problem : 
You are given an array A of size N. The array contains integers and is of even length. The elements of the array represent N coin of values V1, V2, ....Vn. You play against an opponent in an alternating way.

In each turn, a player selects either the first or last coin from the row, removes it from the row permanently, and receives the value of the coin.

You need to determine the maximum possible amount of money you can win if you go first.
Note: Both the players are playing optimally.

Example 1:

Input:
N = 4
A[] = {5,3,7,10}
Output: 15
Explanation: The user collects maximum
value as 15(10 + 5)
Example 2:

Input:
N = 4
A[] = {8,15,3,7}
Output: 22
Explanation: The user collects maximum
value as 22(7 + 15)
Your Task:
Complete the function maximumAmount() which takes an array arr[] (represent values of N coins) and N as number of coins as a parameter and returns the maximum possible amount of money you can win if you go first.

Expected Time Complexity : O(N*N)
Expected Auxiliary Space: O(N*N)

Constraints:
2 <= N <= 103
1 <= Ai <= 106

### solution : 
the twist is you can choose one of the option so sum of the array will give you choice of one and leaving of other 
basically logic says leave one of the value using sum.


    
    long long findMaxAmount(int arr[],vector<vector<long long>> &dp,int start, int end,long long sum)
    {
        if(dp[start][end]==0)
        {
            if(start==end)
            {
                dp[start][end]= arr[start];
            }
            else
            {
                long long option1=findMaxAmount(arr,dp,start+1,end,sum-arr[start]);
                long long option2=findMaxAmount(arr,dp,start,end-1,sum-arr[end]);
                dp[start][end]=sum-min(option1,option2);
            }
        }
        
        return dp[start][end];
    }




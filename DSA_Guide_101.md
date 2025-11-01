### guide web side : https://takeuforward.org/interviews/strivers-sde-sheet-top-coding-interview-problems

## BackTracking 
### find all permutation 
question link: https://leetcode.com/problems/permutations/submissions/1817514593/  
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.  
Example 1:  
Input: nums = [1,2,3]  
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]  
  
Example 2:  
Input: nums = [0,1]  
Output: [[0,1],[1,0]]  
  
Example 3:  
Input: nums = [1]  
Output: [[1]]  

#### trick  
every place should have each element. So swap index = 0, to each element possible, then repeat the same for each index and the choice element should be selected index to end of array   

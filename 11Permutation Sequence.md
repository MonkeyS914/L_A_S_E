###Permutation Sequence
The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

"123"
"132"
"213"
"231"
"312"
"321"
Given n and k, return the kth permutation sequence.

Note: Given n will be between 1 and 9 inclusive.    
##Solution
    class Solution {
    public:
    string getPermutation(int n, int k) {
        vector<int> nums(n);  
        int pCount = 1;  
        for(int i = 0 ; i < n; ++i) {  
            nums[i] = i + 1;  
            pCount *= (i + 1);  
        }  
  
        k--;  
        string res = "";  
        for(int i = 0 ; i < n; i++) {  
            pCount = pCount/(n-i);  
            int selected = k / pCount;  
            res += ('0' + nums[selected]);  
              
            for(int j = selected; j < n-i-1; j++)  
                nums[j] = nums[j+1];  
            k = k % pCount;  
        }  
        return res; 
    }
    };
##PS
1. 以某一数字开头的排列有(n-1)! 个。
例如： 123， 132， 以1开头的是 2！个
2. 所以第一位数字就可以用 （k-1） / (n-1)!  来确定 .这里K-1的原因是，序列号我们应从0开始计算，否则在边界时无法计算。
3. 第二位数字。假设前面取余后为m，则第二位数字是 第 m/(n-2)! 个未使用的数字。
4. 不断重复2，3，取余并且对(n-k)!进行除法，直至计算完毕
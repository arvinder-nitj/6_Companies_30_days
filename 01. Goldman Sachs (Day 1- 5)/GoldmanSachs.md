### 01. [Print Anagrams Together](https://practice.geeksforgeeks.org/problems/print-anagrams-together/1/)
```cpp
class Solution{
  public:
    vector<vector<string> > Anagrams(vector<string>& input) {
        
        vector<vector<string>> ans;
        unordered_map<string,int> mapping;
        //maps key (to sorted string) to group index
        // this will also solve ordering problem
        
        for(string cur:input){
            
            //generate key for group
            string key = cur;
            sort(key.begin(),key.end());
            
            // see if group already exist, if not create one
            if(mapping.find(key) == mapping.end()){
                mapping[key] = ans.size();
                ans.push_back(vector<string>());
            }
            
            //assign to correct group
            ans[mapping[key]].push_back(cur);
        }
        
        return ans;
    }
};  
```

### 02. [Overlapping rectangles](https://practice.geeksforgeeks.org/problems/overlapping-rectangles1924/1/)
```cpp
class Solution {
  public:
    int doOverlap(int L1[], int R1[], int L2[], int R2[]) {
        /*
            solution is 2 stage
            1. find overlap. 
               This will be done in a way which is independent of orientation of rectangles. 
	       It might be valid overlap or invalid overlap
            2. Check if overlap obtained is valid or not 
            
            Question: overlap area > 0 OR overlap area >=0
            
            Turns out common area (overlap area) = 0 is also comnsidered overlap, 
            i.e. tringles if touch each other are also overlapping
        
            How to find overlap?
            L1, L2 => x max and y min => L of overlap
            R1 and R2 => x min and y max => R of verlap
            
        */
        
        // find coordinates of overlap
        int LX = max(L1[0],L2[0]);
        int LY = min(L1[1],L2[1]);
        
        int RX = min(R1[0],R2[0]);
        int RY = max(R1[1],R2[1]);
        
        // is valid overlap
        bool validOverlap = (LX <= RX) && (LY >= RY);
        
        return validOverlap;      
        
    }
};
```

### 03. [Count the subarrays having product less than k ](https://practice.geeksforgeeks.org/problems/count-the-subarrays-having-product-less-than-k1708/1/#)
```cpp
class Solution{
  public:
    int countSubArrayProductLessThanK(const vector<int>& a, int n, long long k) {
        
        long long count     =   0;
        long long product   =   1;
        int start           =   0;
        int end             =  -1;
        
        // range at any instant => [start, end]
	// start == end+1 means empty range
        
        while(end<n-1){
            end++;
            product *= a[end];
            while(product >= k and start <= end){
                //caution: start<=end is necessay
                // if k = 1, and array 1 1 1 1 1 1 1 1
                // then product >= 1 will keep moving start, giving misleading range
                product/=a[start];
                start++;
            }
            count += (end-start+1);
        }
        
        return count;
    }

```

### 04. [Run Length Encoding](https://practice.geeksforgeeks.org/problems/run-length-encoding/1/#)
```cpp
string encode(string src)
{   
    string ans = "";
    int n = src.size();
    
    for(int i=0;i<n;){
        char cur = src[i];
        
        int cnt = 1;
        while(i+cnt < n and src[i+cnt] == cur) cnt++;
        
        ans.push_back(cur);
        string num = to_string(cnt);
        for(char i:num) ans.push_back(i);
        
        i+=cnt;
    }
    return ans;
}
```

### 05. [Ugly Numbers](https://practice.geeksforgeeks.org/problems/ugly-numbers2254/1/)
```cpp
class Solution{
public:	
	// #define ull unsigned long long
	/* Function to get the nth ugly number*/
	ull getNthUglyNo(int n) {
	    ull ugly[n];
        ull i2=0,i3=0,i5=0;
        ull next2=2, next3=3, next5=5;
        ugly[0]=1;
        for(int i=1; i<n; i++){
            ugly[i] = min(next2, min(next3, next5));
            if(ugly[i] == next2)
            {
                i2++;
                next2=2*ugly[i2];
            }
            if(ugly[i] == next3){
                i3++;
                next3=3*ugly[i3];
            }
            if(ugly[i] == next5){
                i5++;
                next5=5*ugly[i5];
            }
        }
        return ugly[n-1];
	}
};
```

### 06. [Greatest Common Divisor of Strings](https://leetcode.com/problems/greatest-common-divisor-of-strings/)
```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        int l = __gcd(str1.size(),str2.size());
        return (str1+str2 == str2+str1)?str1.substr(0,l):""; 
    }
};
```

### 07. [Find the position of M-th item](https://practice.geeksforgeeks.org/problems/find-the-position-of-m-th-item1723/1)
```cpp
class Solution {
  public:
    int findPosition(int N , int M , int K) {
        // we shift numbering from 1,2 3 ...n to 0,1,2,..... (n-1)
        // assume distribtion starts from 0, after finding last pos, we will add offset ie unshift
        // then [0,(n-1)] to [1,n] by +1
        
        /*
        // find last post if start from zero
        int last_pos = (M-1)%N;
        
        //unshift for K and for +1 for indexing
        last_pos = (last_pos+K-1)%N + 1;
        
        return last_pos;
        */
        
        
        //combining all
        return  (M+K-2)%N + 1;
    }
};
```

### 08. [Total Decoding Messages](https://practice.geeksforgeeks.org/problems/total-decoding-messages1235/1/#)
```cpp
class Solution {
	public:
		int CountWays(string s){
		    int n = s.size();
		    vector<long long> dp(n,0);
		    
		    for(int i=0;i<n;i++){
		        if(i==0){
		            if(s[i]=='0')
		                return 0;
		            dp[i] = 1;
		        }else{
		            int ones = s[i]-'0';
		            int tens = s[i-1]-'0';
		            
                    //single digit
		            if(ones!=0){
		                dp[i] = dp[i-1];
		            }else{
		                dp[i]=0;
		            }
		            
                    // as double digit
		            int twoD = tens*10 + ones;
		            if(twoD>=10 && twoD<=26){
		                dp[i]+= ((i>1)?dp[i-2]:1);
		            }
		        }
		        
		        dp[i]%=1000000007;
		    }
		    
		    return dp[n-1]%1000000007;
		}

};
```

### 09. [Number following a pattern](https://practice.geeksforgeeks.org/problems/number-following-a-pattern3126/1)
```cpp
class Solution{   
public:
    string printMinNumberForPattern(string S){
        int num = 1;
        stack<int> stack;
        string ans = "";
        stack.push(num);        
        int n = S.size();
        
        for(int i=0;i<=n;i++){
            if(i==n or S[i]=='I'){
               while(!stack.empty()){
                   ans.push_back(stack.top()+'0');
                   stack.pop();
               }
               num++;
               stack.push(num);
            }else if(S[i]=='D'){
                num++;
                stack.push(num);
            }
        }
        
        return ans;
    }
};
```

### 10. [K Largest Elements/10 Largest Elements](https://www.interviewbit.com/problems/k-largest-elements/)
```cpp
class Solution {
    vector<int>solve(vector<int> &nums, int k) {
        priority_queue<int,vector<int>,greater<int>> pq;
        for(int i:nums){
            if(pq.size()==B and pq.top()<i) pq.pop();
            if(pq.size()<B) pq.push(i);
        }

        vector<int> ans;
        while(!pq.empty()){
            ans.push_back(pq.top());
            pq.pop();
        }
        return ans;
    }
  public:
    vector<int> get10Largest(vector<int> nums){
        // using min heap
        return solve(nums,10);
    }
};
```

### 11. [Find Missing And Repeating](https://practice.geeksforgeeks.org/problems/find-missing-and-repeating2512/1/)
```cpp
vector < int >Solution::repeatedNumber (const vector < int >&arr) {
    /* Will hold xor of all elements and numbers from 1 to n */
    int xor1;

    /* Will have only single set bit of xor1 */
    int set_bit_no;

    int i;
    int x = 0; // missing
    int y = 0; // repeated
    int n = arr.size();

    xor1 = arr[0];

    /* Get the xor of all array elements */
    for (i = 1; i < n; i++)
        xor1 = xor1 ^ arr[i];

    /* XOR the previous result with numbers from 1 to n */
    for (i = 1; i <= n; i++)
        xor1 = xor1 ^ i;

    /* Get the rightmost set bit in set_bit_no */
    set_bit_no = xor1 & ~(xor1 - 1);

    /* Now divide elements into two sets by comparing a rightmost set bit
       of xor1 with the bit at the same position in each element.
       Also, get XORs of two sets. The two XORs are the output elements.
       The following two for loops serve the purpose */

    for (i = 0; i < n; i++) {
        if (arr[i] & set_bit_no)
            /* arr[i] belongs to first set */
            x = x ^ arr[i];

        else
            /* arr[i] belongs to second set */
            y = y ^ arr[i];
    }

    for (i = 1; i <= n; i++) {
        if (i & set_bit_no)
            /* i belongs to first set */
            x = x ^ i;

        else
            /* i belongs to second set */
            y = y ^ i;
    }

    // NB! numbers can be swapped, maybe do a check ?
    int x_count = 0;
    for (int i=0; i<n; i++) {
        if (arr[i]==x)
            x_count++;
    }
    
    if (x_count==0)
        return {y, x};
    
    return {x, y};
}
```

### 12. [Squares in N*N Chessboard](https://practice.geeksforgeeks.org/problems/squares-in-nn-chessboard1801/1#)
```cpp
class Solution {
  public:
    long long squaresInChessBoard(long long n) {
        /*
        
        in 8xb board
        
        Size    Cnt
        1 x 1: 8 * 8 = 64 squares.
        2 x 2: 7 * 7 = 49 squares.
        3 x 3: 6 * 6 = 36 squares.
        4 x 4: 5 * 5 = 25 squares.
        5 x 5: 4 * 4 = 16 squares.
        6 x 6: 3 * 3 = 9 squares.
        7 x 7: 2 * 2 = 4 squares.
        8 x 8: 1 * 1 = 1 square.
        
        => Ans = sum of sqaures = (1^2 + 2^2+ ...... n^2) => n(n+1)(2n+1) / 6  
        */
        
        return n*(n+1)*(2*n+1) / 6;
        
        //Note:
        // A better way to write n*(n+1)*(2n+1)/6 
        // return (n * (n + 1) / 2) * (2*n + 1) / 3; 
        
    }
};
```

### 13. [Decode the string](https://practice.geeksforgeeks.org/problems/decode-the-string2444/1)
```cpp
class Solution{
public:
    string decodedString(string s){
        stack<int> repeat;
        stack<string> word;
        word.push("");
        string ans = "";
        int n = s.size();
        
        int num = 0;
        
        for(int i=0;i<n;i++){
            if(s[i]>='0' and s[i]<='9'){
                num = num*10 + s[i]-'0';
            }else if(s[i]=='['){
                repeat.push(num);
                num = 0;
                
                word.push(ans);
                ans = "";
            }else if(s[i]==']'){
               int times = repeat.top();
               repeat.pop();
               
               string buffer = "";
               for(int cnt=0;cnt<times;cnt++){
                   for(char c:ans){
                       buffer.push_back(c);
                   }
               }
               
               string prev = word.top();
               word.pop();
               
               ans = prev + buffer;
               
            }else{
                ans.push_back(s[i]);
            }
        }
        
        return ans;
    }
};
```
### 14. [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        
        int ans     = INT_MAX;
        int start   = 0;
        int end     = -1;        
        //range => [start,end]
        long long sum = 0;
        int n = nums.size();
        
        while(end<n-1){
            end++;
            sum+= nums[end];            
            while(sum>=target and start<=end){
                int curAns = end - start + 1;
                ans = min(ans,curAns);                
                sum-=nums[start];
                start++;
            }
        }
        
        return ans==INT_MAX?0:ans;
        
    }
};
```

### 15. [Array Pair Sum Divisibility Problem](https://practice.geeksforgeeks.org/problems/array-pair-sum-divisibility-problem3257/1)
```cpp
class Solution {
  public:
    bool canPair(vector<int> nums, int k) {
        /*
            (a+b)%k == 0
        i.e. (a%k + b%k) % k == 0
        i.e. a%k and b%k will lie in range [0,k-1]
        
        for desired pair, a%k + b%k will be either 0 or k
        -> 0 when both a%k and b%k are 0
        -> k when both a%k and b%k are non zero (always +ve)
        
        */
        multiset<int> ms;
        
        for(int i:nums){
            int modified = i%k;
            int partner = (modified == 0)?0:k - modified;
            
            auto itr = ms.find(partner);
            if(itr!=ms.end()){
                //pair formed
                ms.erase(itr);
            }else{
                // pair not formed
                // hope will be formed in future
                ms.insert(modified);
            }
        }
        
        // empty multiset means all elements formed the pairs and no element is yet to form pair
        return ms.size()==0;
    }
};
```
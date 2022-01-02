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

```

### 01. []()

```cpp

```

### 01. []()

```cpp

```

### 01. []()

```cpp

```
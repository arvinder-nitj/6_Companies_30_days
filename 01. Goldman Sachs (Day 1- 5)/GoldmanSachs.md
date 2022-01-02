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
            2. This will be done in a way which is independent of orientation of rectangles. It might be valid overlap or invalid overlap
            2. Check if overlap obtained is valid or not 
            
            Question: overlap area > 0 OR overlap area >=0
            
            Turns out common area (overlap area) = 0 is also comnsidered overlap, 
            i.e. tringles if touch each other are also overlapping
        
            How?
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

### 01. []()

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

### 01. []()

```cpp

```

### 01. []()

```cpp

```
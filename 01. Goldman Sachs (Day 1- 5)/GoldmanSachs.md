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

### 01. []()

```cpp

```

### 01. []()

```cpp

```

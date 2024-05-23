## Subsets with duplicates

Iterative

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& S) {
        vector<vector<int>> totalset = {{}};
        sort(S.begin(),S.end());
        for(int i=0; i<S.size(); i ++){
            int previousN = totalset.size();
            for(int k=0; k<previousN; k++){
                vector<int> instance = totalset[k];
                instance.push_back(S[i]);
                totalset.push_back(instance);
            }
        }
        return totalset;
    }
};
```


## Subsets without duplicates

Iterative

```cpp
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int> &S) {
        vector<vector<int> > totalset = {{}};
        sort(S.begin(),S.end());
        int count = 0;
        for(int i=0; i<S.size(); i += count){
            count = 0;
            while(count + i<S.size() && S[count+i]==S[i])  
                count++;
            int previousN = totalset.size();
            for(int k=0; k<previousN; k++){
                vector<int> instance = totalset[k];
                for(int j=0; j<count; j++){
                    instance.push_back(S[i]);
                    totalset.push_back(instance);
                }
            }
        }
        return totalset;
      }
};
```

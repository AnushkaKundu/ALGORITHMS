## Permutations with duplicates (normal)

Recursive:

```
class Solution {
public:
    void backtrack(vector<int>& nums, vector<int>& v, vector<vector<int>>& output, vector<bool>& used) 
    {
        if (v.size() == nums.size())
        {
            output.push_back(v);
            return;
        }

        for (int i=0; i<nums.size(); i++)
        {
            if (used[i] == 1) continue;
            v.push_back(nums[i]);
            used[i] = 1;
            backtrack(nums, v, output, used);
            used[i] = 0;
            v.pop_back();
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> output;
        vector<int>v;
        int n = nums.size();
        vector<bool> used(n, 0);
        backtrack(nums, v, output, used);
        return output;
    }
};
```

## Permutations without duplicates
When a number has the same value with its previous, we can use this number only if his previous is used

Recursive:

```
class Solution {
public:
    void backtrack(vector<int>& nums, vector<int>& v, vector<vector<int>>& output, vector<bool>& used) 
    {
        if (v.size() == nums.size())
        {
            output.push_back(v);
            return;
        }

        for (int i=0; i<nums.size(); i++)
        {
            if (used[i] || (i > 0 and nums[i-1] == nums[i] and used[i-1])) 
                continue;
            v.push_back(nums[i]);
            used[i] = 1;
            backtrack(nums, v, output, used);
            used[i] = 0;
            v.pop_back();
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> output;
        vector<int>v;
        sort(nums.begin(), nums.end());
        int n = nums.size();
        vector<bool> used(n, 0);
        backtrack(nums, v, output, used);
        return output;
    }
};
```

Iterative:

(Like Next Permutation)

```
class Solution {
public:
	vector<vector<int>> permuteUnique(vector<int> &S) {
        vector<vector<int>> res;
		sort(S.begin(), S.end());		
		res.push_back(S);
		int j;
		int i = S.size()-1;
		while (1){
			for (i=S.size()-1; i>0; i--){
				if (S[i-1]< S[i]){
					break;
				}
			}
			if(i == 0){
				break;
			}

			for (j=S.size()-1; j>i-1; j--){
				if (S[j]>S[i-1]){
					break;
				}
			}					
			swap(S[i-1], S[j]);
			reverse(S, i, S.size()-1);
			res.push_back(S);
		}
		return res;
    }
	void reverse(vector<int> &S, int s, int e){		
		while (s<e){
			swap(S[s++], S[e--]);
		}
	}	
	vector<vector<int> > res;
};
```

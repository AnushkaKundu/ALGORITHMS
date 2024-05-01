```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root) 
            return {};
        vector<vector<int>>op;
        queue<TreeNode*> Q;
        Q.push(root);
        bool b = 1;
        while(!Q.empty()) {
            vector<int>t;
            int sz = Q.size();
            while(sz--) {
                auto node = Q.front();
                t.push_back(node->val);
                if (node->left)
                    Q.push(node->left);
                if (node->right)
                    Q.push(node->right);
                Q.pop();
            }
            op.push_back(t);
            b = 1-b;
        }
        return op;
    }
};
```

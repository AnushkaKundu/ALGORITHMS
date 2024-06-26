You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.


```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if (!root) 
            return {};
        queue<Node*> Q;
        Q.push(root);
        bool b = 1;
        while(!Q.empty()) {
            vector<Node*>t;
            int sz = Q.size();
            while(sz--) {
                auto node = Q.front();
                t.push_back(node);
                if (node->left)
                    Q.push(node->left);
                if (node->right)
                    Q.push(node->right);
                Q.pop();
            }
            int n = t.size();
            for (int i=0; i<n-1; i++) {
                t[i]->next = t[i+1];
            }
            t[n-1]->next = NULL;
        }
        return root;
    }
};
```

### Path Sum II
- https://leetcode.com/problems/path-sum-ii/

回溯

每次先push进去一个，之后进行线程发射，之后再pop出一个，以便于后续线程发射。

```c+++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> result;
        vector<int> one;
        helper(root,sum,one,result);
        return result;
    }
    void helper(TreeNode* root,int sum,vector<int> &path,vector<vector<int>> &paths)
    {
        if(!root)
            return;
        path.push_back(root->val);
        if(!(root->left)&&!(root->right)&&sum==root->val)
            paths.push_back(path);
        helper(root->left,sum-root->val,path,paths);
        helper(root->right,sum-root->val,path,paths);
        path.pop_back();
    }
    
};
```


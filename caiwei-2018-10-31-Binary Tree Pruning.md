### Binary Tree Pruning
- https://leetcode.com/problems/binary-tree-pruning/



递归

如果左右子树全是NULL，且该节点本身携带的是0，那么就返回一个NULL，



```c++
class Solution {
public:
    TreeNode* pruneTree(TreeNode* root) {
        if(root==NULL)
            return NULL;
        root->left=pruneTree(root->left);
        root->right=pruneTree(root->right);
        if(root->right==NULL&&root->left==NULL&&root->val==0)
            return NULL;
        return root;
    }
    
};
```


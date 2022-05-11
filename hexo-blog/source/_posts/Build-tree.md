---
title: 根据数组生成二叉树
categories: [算法]
tags: [二叉树生成]
---

# 



# 定义二叉树

```c++
struct TreeNode{
  	int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int _val):val(_val){};
};
```

# 层序遍历产生

```c++
#include <vector>
#include <queue>

int main(){
	vector<int> tree = {'1','#','1','#','1','#','1','#','1'};
    int length = tree.size();
	queue<TreeNode*> Q;
    TreeNode* root;
    if(tree[0]=='1'){
        root = new TreeNode(0);
    	Q.push(root);
    }
    int index = 0;
    while(!Q.empty()){
        int len = Q.size();
        for(int i=0;i<len;i++){
            TreeNode* temp = Q.front();
            Q.pop();
            index++;
            if(index<length&&tree[index]=='1'){
                temp->left = new TreeNode(0);
                Q.push(temp->left);
            }
            index++;
            if(index<length&&tree[index]=='1'){
                temp->right = new TreeNode(0);
                Q.push(temp->right);
            }
        }
    }
	return 0;
}
```


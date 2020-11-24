## 树的遍历

### N叉树的遍历

```js

/**
 * // Definition for a Node.
 * function Node(val,children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {Node} root
 * @return {number}
 */

// 前序遍历
var preorder = function(root) {

    let res = [];

    var traversal = function(root) {
        if (root !== null) {
            res.push(root.val);
            root.children.forEach((kids) => {
                traversal(kids);
            })
        }
    }

    traversal(root);
    return res;
}

// 后序遍历
var postorder = function(root) {

    let res = [];

    var traversal = function(root) {
        if (root !== null) {
            root.children.forEach((kids) => {
                traversal(kids);
            });
            res.push(root.val);
        }
    }

    traversal(root);
    return res;
}

```

### 二叉树的遍历

```js

/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
// 前序遍历
var preorderTraversal = function(root) {

    let res = [];

    var traversal = function(root) {
        if (root !== null) {
            res.push(root.val);
            traversal(root.left);
            traversal(root.right);
        }
    }

    traversal(root);
    return res;
}

// 中序遍历
var inorderTraversal = function(root) {
    let res = [];
    function traversal(root) {
        if(root !== null) {
            traversal(root.left);
            res.push(root.val);
            traversal(root.right);
        }
    };
    traversal(root);
    return res;
};

// 后序遍历
var postorderTraversal = function(root) {
    let res = [];

    function traversal(root){
        if (root !== null) {
            traversal(root.left);
            traversal(root.right);
            res.push(root.val);
        }
    }

    traversal(root);
    return res;
}

```

### 二叉树的节点数

1. 完全二叉树的节点个数

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var countNodes = function(root) {
    let count = 0;

    function traverse(root) {
        if(root !== null) {
            count++;
            traverse(root.left);
            traverse(root.right);
        }
    }

    traverse(root);
    return count;

};
```

### 树的最大深度

1. N叉树的最大深度

```js
var maxDepth = function(root) {

};
```

2. 二叉树的最大深度

```js
var maxDepth = function(root) {
    if(!root) return 0;

    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));

}
```
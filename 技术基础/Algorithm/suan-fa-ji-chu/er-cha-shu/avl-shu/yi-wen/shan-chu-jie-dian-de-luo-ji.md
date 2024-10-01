# 删除节点的逻辑

**删除节点的主要逻辑**：

* 首先执行普通的二叉搜索树删除操作。
* 如果节点有两个子节点，则找到右子树中的最小节点，替代被删除的节点。
* 删除后更新节点的高度，检查是否需要恢复平衡，并根据平衡因子的值进行相应的旋转操作。



以下是AVL树中删除节点的代码片段，专注于删除操作和恢复平衡的逻辑：

```c
// 删除节点
Node* deleteNode(Node* root, int data) {
    // 1. 执行普通的BST删除
    if (root == NULL) return root;

    if (data < root->data) {
        root->left = deleteNode(root->left, data);
    } else if (data > root->data) {
        root->right = deleteNode(root->right, data);
    } else {
        // 找到要删除的节点
        if (root->left == NULL || root->right == NULL) {
            Node* temp = root->left ? root->left : root->right;
            if (temp == NULL) {
                temp = root;
                root = NULL; // 该节点是叶子节点
            } else {
                *root = *temp; // 该节点有一个子节点
            }
            free(temp);
        } else {
            // 该节点有两个子节点
            Node* temp = minNode(root->right); //找到右子树中的最小节点
            root->data = temp->data; // 将最小节点的值赋值给root
            root->right = deleteNode(root->right, temp->data);  // 继续删除最小的节点
            // 将右子树最小节点的值覆盖掉root的值，然后继续删除这个最小值的节点
        }
    }

    // 如果树只有一个节点，则返回
    if (root == NULL) return root;

    // 2. 更新节点高度
    updateHeight(root);

    // 3. 检查不平衡状态并进行相应的旋转
    int balance = getBalance(root);

    // 左左情况
    if (balance > 1 && getBalance(root->left) >= 0) {
        return rightRotate(root);
    }

    // 右右情况
    if (balance < -1 && getBalance(root->right) <= 0) {
        return leftRotate(root);
    }

    // 左右情况
    if (balance > 1 && getBalance(root->left) < 0) {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    // 右左情况
    if (balance < -1 && getBalance(root->right) > 0) {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root; // 返回更新后的根节点
}
```

#### 关键点说明：

1. **普通BST删除逻辑**：首先通过递归找到并删除节点。
2. **更新节点高度**：在删除节点后，更新当前节点的高度。
3. **平衡检查与旋转**：
   * 根据节点的平衡因子判断是否需要右旋或左旋，恢复AVL树的平衡。
4. **返回根节点**：返回更新后的树的根节点。

#### 使用方法

将此片段集成到完整的AVL树实现中，确保有适当的辅助函数（如 `minNode`、`updateHeight`、`getBalance`、`rightRotate` 和 `leftRotate`），以支持完整的删除操作和树的平衡维护。

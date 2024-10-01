# 代码实现

下面是一个简单的C语言实现二叉搜索树（Binary Search Tree, BST）的示例，包括构建、插入、删除和查找等基本操作。

```c
#include <stdio.h>
#include <stdlib.h>

// 定义树节点结构
typedef struct Node {
    int data;
    struct Node *left;
    struct Node *right;
} Node;

// 创建新节点
Node* createNode(int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// 插入节点
Node* insert(Node* root, int data) {
    if (root == NULL) {
        return createNode(data);
    }
    if (data < root->data) {
        root->left = insert(root->left, data);
    } else if (data > root->data) {
        root->right = insert(root->right, data);
    }
    return root;
}

// 查找节点
Node* search(Node* root, int data) {
    if (root == NULL || root->data == data) {
        return root;
    }
    if (data < root->data) {
        return search(root->left, data);
    }
    return search(root->right, data);
}

// 找到最小值节点
Node* findMin(Node* root) {
    while (root->left != NULL) {
        root = root->left;
    }
    return root;
}

// 删除节点
Node* deleteNode(Node* root, int data) {
    if (root == NULL) {
        return root;
    }
    if (data < root->data) {
        root->left = deleteNode(root->left, data);
    } else if (data > root->data) {
        root->right = deleteNode(root->right, data);
    } else {
        // 找到要删除的节点
        if (root->left == NULL) {
            Node* temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            Node* temp = root->left;
            free(root);
            return temp;
        }
        // 找到右子树的最小节点
        Node* temp = findMin(root->right);
        root->data = temp->data; // 用最小节点替代当前节点
        root->right = deleteNode(root->right, temp->data); // 删除最小节点
    }
    return root;
}

// 中序遍历
void inorderTraversal(Node* root) {
    if (root != NULL) {
        inorderTraversal(root->left);
        printf("%d ", root->data);
        inorderTraversal(root->right);
    }
}

// 主函数
int main() {
    Node* root = NULL;
    
    // 插入节点
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 70);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 60);
    root = insert(root, 80);
    
    printf("中序遍历: ");
    inorderTraversal(root);
    printf("\n");
    
    // 查找节点
    int key = 40;
    Node* foundNode = search(root, key);
    if (foundNode) {
        printf("找到节点: %d\n", foundNode->data);
    } else {
        printf("未找到节点: %d\n", key);
    }
    
    // 删除节点
    root = deleteNode(root, 50);
    printf("删除 50 后的中序遍历: ");
    inorderTraversal(root);
    printf("\n");
    
    return 0;
}
```

#### 代码说明

1. **结构体定义**：`Node`结构体表示树的节点，包含数据和左右子节点指针。
2. **插入函数**：`insert`用于将新节点插入到适当的位置。
3. **查找函数**：`search`用于查找特定值的节点。
4. **删除函数**：`deleteNode`用于删除节点，处理三种情况：无子节点、一个子节点、两个子节点。
5. **中序遍历**：`inorderTraversal`用于输出树的节点值，以验证结构。

#### 使用

* 在`main`函数中插入一些节点，并进行查找和删除操作。
* 通过中序遍历输出节点，验证树的结构。



有助于理解AVL的删除节点的操作，其实是一样的。


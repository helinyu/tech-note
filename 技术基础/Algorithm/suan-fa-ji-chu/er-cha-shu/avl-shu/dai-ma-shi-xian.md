# 代码实现

AVL树是一种自平衡的二叉搜索树，具有以下性质：对于每个节点，左子树和右子树的高度差最多为1。这种性质使得AVL树能够在最坏情况下保持对数时间复杂度的查找、插入和删除操作。

下面是AVL树的实现，包括构建、遍历（前序、中序、后序）、插入、删除和调整操作的代码示例：

{% code overflow="wrap" %}
```c
#include <stdio.h>
#include <stdlib.h>

// AVL树节点结构
typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
    int height; // 节点高度
} Node;

// 获取节点的高度
int height(Node* node) {
    if (node == NULL) return 0;
    return node->height;
}

// 获取节点的平衡因子
int getBalance(Node* node) {
    if (node == NULL) return 0;
    return height(node->left) - height(node->right);
}

// 创建新节点
Node* createNode(int data) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    newNode->height = 1; // 新节点的高度为1
    return newNode;
}

// 右旋转
Node* rightRotate(Node* y) {
    Node* x = y->left; // 将左子节点赋值给x
    Node* T2 = x->right; // 保存x的右子节点(因为x的右节点将会指向y)

    // 执行旋转
    x->right = y;
    y->left = T2;

// 更新高度，注意先更新自己点，再更新父节点
    y->height = 1 + (height(y->left) > height(y->right) ? height(y->left) : height(y->right));
    x->height = 1 + (height(x->left) > height(x->right) ? height(x->left) : height(x->right));

// 返回新的根节点
    return x;
}

// 左旋转
Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = 1 + (height(x->left) > height(x->right) ? height(x->left) : height(x->right));
    y->height = 1 + (height(y->left) > height(y->right) ? height(y->left) : height(y->right));

    return y;
}

// 插入节点
Node* insert(Node* node, int data) {
    if (node == NULL) return createNode(data);
    
    if (data < node->data) {
        node->left = insert(node->left, data);
    } else if (data > node->data) {
        node->right = insert(node->right, data);
    } else {
        return node; // 不允许重复值
    }

    node->height = 1 + (height(node->left) > height(node->right) ? height(node->left) : height(node->right));

    int balance = getBalance(node);

    // 左左情况
    if (balance > 1 && data < node->left->data) {
        return rightRotate(node);
    }

    // 右右情况
    if (balance < -1 && data > node->right->data) {
        return leftRotate(node);
    }

    // 左右情况
    if (balance > 1 && data > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // 右左情况
    if (balance < -1 && data < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}

// 找到最小节点
Node* minNode(Node* node) {
    Node* current = node;
    while (current->left != NULL) {
        current = current->left;
    }
    return current;
}

// 删除节点
Node* deleteNode(Node* root, int data) {
    if (root == NULL) return root;

    if (data < root->data) {
        root->left = deleteNode(root->left, data);
    } else if (data > root->data) {
        root->right = deleteNode(root->right, data);
    } else {
        if ((root->left == NULL) || (root->right == NULL)) {
            Node* temp = root->left ? root->left : root->right;
            if (temp == NULL) {
                temp = root;
                root = NULL;
            } else {
                *root = *temp; // 复制节点内容
            }
            free(temp);
        } else {
            Node* temp = minNode(root->right);
            root->data = temp->data;
            root->right = deleteNode(root->right, temp->data);
        }
    }

    if (root == NULL) return root;

    root->height = 1 + (height(root->left) > height(root->right) ? height(root->left) : height(root->right));

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

    return root;
}

// 前序遍历
void preorder(Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

// 中序遍历
void inorder(Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

// 后序遍历
void postorder(Node* root) {
    if (root != NULL) {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}

// 主函数
int main() {
    Node* root = NULL;

    // 插入节点
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    printf("中序遍历: ");
    inorder(root);
    printf("\n");

    printf("前序遍历: ");
    preorder(root);
    printf("\n");

    printf("后序遍历: ");
    postorder(root);
    printf("\n");

    // 删除节点
    root = deleteNode(root, 30);

    printf("删除节点后的中序遍历: ");
    inorder(root);
    printf("\n");

    return 0;
}
```
{% endcode %}

#### 代码说明：

1. **节点结构**：定义了一个包含数据、左右子节点和高度的节点结构。
2. **高度和均衡因子的计算**：提供了获取节点高度和计算均衡因子的函数。
3. **旋转操作**：实现了左旋和右旋操作，以保持AVL树的平衡。
4. **插入和删除**：提供了插入和删除节点的函数，并在插入和删除后调整树的平衡。
5. **遍历**：实现了前序、中序和后序遍历的方法。
6. **主函数**：插入一些节点，并展示遍历的结果。之后删除一个节点并展示更新后的中序遍历结果。

#### 使用方法

* 编译并运行这个代码，你将看到插入节点后的中序遍历结果和删除节点后的更新结果。
* 你可以根据需要插入或删除其他节点以测试AVL树的功能。





{% hint style="info" %}
难点：

1、插入 LL RR LR RL 左旋/右旋&#x20;

2、删除的时候，删除节点之后，需要判断所有父节点的平衡

3、平衡因子的计算

4、不管是插入还是删除，都是要递归的，因为高度都是需要重新计算，删除的时候还需要判断父节点是否需要调整，两者代码是可以一样的。
{% endhint %}

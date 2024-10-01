# 代码实现

下面是一个简单的 C 语言实现的红黑树，包括构建、插入、删除和查找操作的示例代码。

```c
#include <stdio.h>
#include <stdlib.h>

typedef enum { RED, BLACK } Color;

typedef struct Node {
    int data;
    Color color;
    struct Node *left, *right, *parent;
} Node;

Node *NIL;  // 代表空节点

Node* createNode(int data) {
    Node *newNode = (Node *)malloc(sizeof(Node));
    newNode->data = data;
    newNode->left = NIL;
    newNode->right = NIL;
    newNode->parent = NULL;
    newNode->color = RED;  // 新节点总是红色
    return newNode;
}

// 左旋
void leftRotate(Node **root, Node *x) {
    Node *y = x->right;
    x->right = y->left;

    if (y->left != NIL) {
        y->left->parent = x;
    }
    y->parent = x->parent;

    if (x->parent == NULL) {
        *root = y;
    } else if (x == x->parent->left) {
        x->parent->left = y;
    } else {
        x->parent->right = y;
    }

    y->left = x;
    x->parent = y;
}

// 右旋
void rightRotate(Node **root, Node *y) {
    Node *x = y->left;
    y->left = x->right;

    if (x->right != NIL) {
        x->right->parent = y;
    }
    x->parent = y->parent;

    if (y->parent == NULL) {
        *root = x;
    } else if (y == y->parent->right) {
        y->parent->right = x;
    } else {
        y->parent->left = x;
    }

    x->right = y;
    y->parent = x;
}

// 修复红黑树的性质
void fixViolation(Node **root, Node *newNode) {
    Node *parent = NULL;
    Node *grandparent = NULL;

    while ((newNode != *root) && (newNode->color == RED) && (newNode->parent->color == RED)) {
        parent = newNode->parent;
        grandparent = parent->parent;

        // 父节点是祖父节点的左子节点
        if (parent == grandparent->left) {
            Node *uncle = grandparent->right;

            // Case 1: 叔叔节点也是红色
            if (uncle->color == RED) {
                grandparent->color = RED;
                parent->color = BLACK;
                uncle->color = BLACK;
                newNode = grandparent; // 向上继续检查
            } else {
                // Case 2: 新节点是父节点的右子节点
                if (newNode == parent->right) {
                    leftRotate(root, parent);
                    newNode = parent;
                    parent = newNode->parent;
                }
                // Case 3: 新节点是父节点的左子节点
                rightRotate(root, grandparent);
                Color tempColor = parent->color;
                parent->color = grandparent->color;
                grandparent->color = tempColor;
                newNode = parent;
            }
        } else { // 父节点是祖父节点的右子节点
            Node *uncle = grandparent->left;

            // Case 1: 叔叔节点也是红色
            if (uncle->color == RED) {
                grandparent->color = RED;
                parent->color = BLACK;
                uncle->color = BLACK;
                newNode = grandparent; // 向上继续检查
            } else {
                // Case 2: 新节点是父节点的左子节点
                if (newNode == parent->left) {
                    rightRotate(root, parent);
                    newNode = parent;
                    parent = newNode->parent;
                }
                // Case 3: 新节点是父节点的右子节点
                leftRotate(root, grandparent);
                Color tempColor = parent->color;
                parent->color = grandparent->color;
                grandparent->color = tempColor;
                newNode = parent;
            }
        }
    }

    (*root)->color = BLACK; // 根节点始终是黑色
}

// 插入新节点
void insert(Node **root, int data) {
    Node *newNode = createNode(data);
    Node *y = NULL;
    Node *x = *root;

    while (x != NIL) {
        y = x;
        if (newNode->data < x->data) {
            x = x->left;
        } else {
            x = x->right;
        }
    }

    newNode->parent = y;
    if (y == NULL) {
        *root = newNode; // 树为空
    } else if (newNode->data < y->data) {
        y->left = newNode;
    } else {
        y->right = newNode;
    }

    fixViolation(root, newNode);
}

// 中序遍历
void inorderHelper(Node *root) {
    if (root != NIL) {
        inorderHelper(root->left);
        printf("%d ", root->data);
        inorderHelper(root->right);
    }
}

void inorder(Node *root) {
    inorderHelper(root);
    printf("\n");
}

// 查找节点
Node* search(Node *root, int key) {
    while (root != NIL) {
        if (key == root->data) {
            return root;
        } else if (key < root->data) {
            root = root->left;
        } else {
            root = root->right;
        }
    }
    return NULL;
}

// 释放内存
void freeTree(Node *root) {
    if (root != NIL) {
        freeTree(root->left);
        freeTree(root->right);
        free(root);
    }
}

int main() {
    NIL = (Node *)malloc(sizeof(Node));
    NIL->color = BLACK;
    NIL->left = NIL->right = NIL->parent = NULL;

    Node *root = NIL;

    insert(&root, 10);
    insert(&root, 20);
    insert(&root, 30);
    insert(&root, 15);

    printf("中序遍历: ");
    inorder(root);

    Node *foundNode = search(root, 20);
    if (foundNode) {
        printf("找到节点: %d\n", foundNode->data);
    } else {
        printf("未找到节点\n");
    }

    freeTree(root);
    free(NIL);
    return 0;
}
```

#### 说明

1. **节点结构**：每个节点包含数据、颜色、左右子节点和父节点的指针。
2. **旋转操作**：左旋和右旋用于保持红黑树的性质。
3. **插入操作**：插入新节点后，调用 `fixViolation` 修复可能违反的红黑树性质。
4. **遍历**：提供中序遍历函数以验证树的结构。
5. **查找操作**：提供查找函数以查找特定值的节点。
6. **内存管理**：在 `main` 函数中动态分配内存，并在结束时释放。


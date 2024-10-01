# 迭代法

以下是使用迭代法实现搜索二叉树的前序、中序和后序遍历的代码示例：

```c
#include <stdio.h>
#include <stdlib.h>

// 定义二叉树节点结构
typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
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
    if (root == NULL) return createNode(data);
    if (data < root->data)
        root->left = insert(root->left, data);
    else
        root->right = insert(root->right, data);
    return root;
}

// 非递归前序遍历
void preorder(Node* root) {
    if (root == NULL) return;

    Node** stack = (Node**)malloc(100 * sizeof(Node*)); // 简单实现，固定大小
    int top = -1;

    stack[++top] = root;
    while (top >= 0) {
        Node* current = stack[top--];
        printf("%d ", current->data);
        
        if (current->right) stack[++top] = current->right; // 先右后左
        if (current->left) stack[++top] = current->left;
    }

    free(stack);
}

// 非递归中序遍历
void inorder(Node* root) {
    Node** stack = (Node**)malloc(100 * sizeof(Node*)); // 简单实现，固定大小
    int top = -1;
    Node* current = root;

    while (current != NULL || top >= 0) {
        while (current != NULL) {
            stack[++top] = current;
            current = current->left;
        }
        current = stack[top--];
        printf("%d ", current->data);
        current = current->right;
    }

    free(stack);
}

// 非递归后序遍历
void postorder(Node* root) {
    if (root == NULL) return;

    Node** stack1 = (Node**)malloc(100 * sizeof(Node*)); // 第一个栈
    Node** stack2 = (Node**)malloc(100 * sizeof(Node*)); // 第二个栈
    int top1 = -1, top2 = -1;

    stack1[++top1] = root;

    while (top1 >= 0) {
        Node* current = stack1[top1--];
        stack2[++top2] = current;

        if (current->left) stack1[++top1] = current->left;
        if (current->right) stack1[++top1] = current->right;
    }

    while (top2 >= 0) {
        printf("%d ", stack2[top2--]->data);
    }

    free(stack1);
    free(stack2);
}

int main() {
    Node* root = NULL;
    root = insert(root, 5);
    insert(root, 3);
    insert(root, 7);
    insert(root, 2);
    insert(root, 4);
    insert(root, 6);
    insert(root, 8);

    printf("非递归前序遍历: ");
    preorder(root);
    printf("\n");

    printf("非递归中序遍历: ");
    inorder(root);
    printf("\n");

    printf("非递归后序遍历: ");
    postorder(root);
    printf("\n");

    return 0;
}
```

这个代码实现了搜索二叉树的前序、中序和后序遍历，均采用了迭代法。前序遍历和中序遍历使用一个栈，而后序遍历使用两个栈来处理。

# 层次遍历（广度）

下面是一个实现二叉树层次遍历的代码示例：

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

// 层次遍历
void levelOrder(Node* root) {
    if (root == NULL) return;

    Node** queue = (Node**)malloc(100 * sizeof(Node*)); // 简单实现，固定大小
    int front = 0, rear = 0;

    queue[rear++] = root;

    while (front < rear) {
        Node* current = queue[front++];
        printf("%d ", current->data);

        if (current->left != NULL)
            queue[rear++] = current->left;
        if (current->right != NULL)
            queue[rear++] = current->right;
    }

    free(queue);
}

int main() {
    Node* root = NULL;
    root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    printf("层次遍历: ");
    levelOrder(root);
    printf("\n");

    return 0;
}
```

这个代码实现了二叉树的层次遍历，<mark style="color:red;">使用简单的队列方法来保存待访问的节点</mark>。


# 基本概念

红黑树是一种自平衡的二叉搜索树，它具有以下特性：

1. **节点颜色**：每个节点是红色或黑色。
2. **根节点**：根节点始终是黑色。
3. **叶子节点**：所有叶子节点（NIL或空节点）都是黑色。
4. **红色节点**：如果一个节点是红色，则它的两个子节点都是黑色（即没有两个红色节点相连）。
5. **黑色高度**：从任何节点到其每个叶子节点的所有路径都包含相同数量的黑色节点。

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

#### 操作

红黑树支持以下基本操作，并保持自平衡特性：

* **插入**：在插入新节点后，可能会违反红黑树的性质，需要通过旋转和重新着色来修复。
* **删除**：删除节点后，同样可能会违反性质，需要进行旋转和重新着色以恢复红黑树的特性。
* **查找**：查找操作与普通二叉搜索树相同，时间复杂度为 O(log n)。

#### 性能

由于红黑树是自平衡的，所有基本操作（插入、删除、查找）的时间复杂度都为 O(log n)，因此在处理大量数据时，红黑树的性能非常优越。


# B+ 树

## MySQL 索引
如果使用Hash存储， 查询时间复杂度可以是O(1),但是不支持范围查找，二叉查找树可以中序 前序 后序遍历 但仍然无法按照范围查询

## B+ 树
在二分查找树的基础上，再加一层级使用有序链表存储所有元素，所以索引文件存储10 个数据，需要20个节点信息，范围查找先找到初始值然后开始在链表中遍历找到符合范围的所有元素
<br/>
但是这样会导致内存比较比较大，可以采用时间换空间的方法,将树存储在磁盘，但是树查询的效率与树的高度有关，频繁查询会导致磁盘IO 频率<br/>
实际上 m 叉查找树+有序连标构成m叉索引就是b+树

## B+ 的实现
```java
package bplus;

/**
 * 树节点的定义，区分于叶子节点
 * 假设为int 类型创建索引
 */
public class BPlusTreeNode {
    int m = 5;// 5叉树
    private int [] keyWorlds=  new int[5-1]; // 存储数据
    BPlusTreeNode [] children = new BPlusTreeNode[5-1];
}

/**
 * 叶子节点
 */
public class BPlusLeafNode {
    BPlusLeafNode prev;
    BPlusLeafNode next;
    // 额外存储数据地址
    private int[] dateAddress;
    // 每个叶子节点存储的数据
    private int [] keyWorld;
}

```

## B+ 树的扩容与删除
**无论是内存还是磁盘，操作系统都是按照页来读取数据**一页通常是4KB，当读取超过一页时候会产生多次IO操作，所以B+ 树在选择过程中一般经过计算，一个节点正好是一页，也就是m叉查找树是经过计算而来的<br/>
因为要一直维护成m叉查找树，所以必然在插入和删除时候消耗性能，
<br/>
为了避免删除元素和删除时候的合并造成性能浪费，默认节点的叶子节点不能小于m/2,跟节点可以小于，一般根存储在内存中，其他节点在磁盘中

## B树与B- 树
B 树就是B- 树，B+ 是对B 树的升级<br/>
B+树的节点不存储数据，而B 树存储<br/>
B 树没有有序链表，所以B树只是一个m叉且节点树不能小于m/2的m叉查找树




##
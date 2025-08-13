
# 双向循环链表设计（带哨兵节点）Design of Doubly Circular Linked List with Sentinel Node

> 📌 适用于 Java 项目，简化链表边界处理逻辑，便于维护。

---

## 🧠 什么是带哨兵节点的双向链表？  
### What is a doubly circular linked list with sentinel node?

带哨兵节点的双向链表是一种链表设计模式，引入一个不存储实际数据的「哨兵节点（Sentinel Node）」，用作统一的头尾标记。链表的最后一个节点的 `next` 指向哨兵节点，哨兵节点的 `prev` 指向最后一个节点，从而形成一个 **循环双向结构**。

A doubly circular linked list with a sentinel node introduces a dummy node (sentinel) that does not hold real data, but simplifies insertion and deletion at both ends. The sentinel node connects to both the head and tail, forming a **circular doubly linked list**.

---

## 🧱 节点结构定义（Node Structure）

```java
class DListNode {
    int val;
    DListNode prev;
    DListNode next;

    DListNode() {}  // 哨兵节点构造器
    DListNode(int val) {
        this.val = val;
    }
}
```

---

## 🧰 链表类定义与初始化（List Initialization）

```java
public class MyLinkedList {
    private DListNode sentinel;
    private int size;

    public MyLinkedList() {
        sentinel = new DListNode();
        sentinel.prev = sentinel;
        sentinel.next = sentinel;
        size = 0;
    }
}
```

### 初始化结构示意图 Initialization:
```
sentinel <-> sentinel
```

---

## ➕ 添加节点 Add a Node at Tail

```java
public void addAtTail(int val) {
    DListNode node = new DListNode(val);
    DListNode last = sentinel.prev;

    node.prev = last;
    node.next = sentinel;

    last.next = node;
    sentinel.prev = node;

    size++;
}
```

---

## ❌ 删除头部节点 Delete Head Node

```java
public void deleteAtHead() {
    if (size == 0) return;

    DListNode first = sentinel.next;
    DListNode second = first.next;

    sentinel.next = second;
    second.prev = sentinel;

    size--;
}
```

---

## 🎯 查询第 k 个节点 Get k-th Node

```java
public int get(int index) {
    if (index < 0 || index >= size) return -1;

    DListNode cur = sentinel.next;
    for (int i = 0; i < index; i++) {
        cur = cur.next;
    }
    return cur.val;
}
```

---

## ✅ 优势总结 Summary of Benefits

| 对比点 Feature | 普通双向链表 Normal DLL | 哨兵循环链表 Sentinel DLL |
|----------------|--------------------------|-----------------------------|
| 插入头部 Insert Head | 需要特殊判断 Special handling | 统一处理 Unified |
| 删除尾部 Delete Tail | 判断空链表 Check if empty | 自动适配 Always works |
| 边界判断 Edge Cases | 多 if、易错 Many checks | 少判断 Safer |
| 实现复杂度 Complexity | 高 High | 低 Low |

---

_Last updated: 2025-08-07_

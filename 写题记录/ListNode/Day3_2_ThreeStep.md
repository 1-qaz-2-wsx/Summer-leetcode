------

# 🧱 标准三步走法（交换链表节点）  
# Standard Three-Step Method (Swap Linked List Nodes)

## 📌 场景说明 | Scenario  
用于链表中每两个节点一组进行交换。  
Used to swap every two adjacent nodes in a singly linked list.

---

## 🪜 三个步骤 | Three Steps

### 🥇 步骤一：重新连接前一个节点与第二个节点  
**Connect previous node to the second node**  
```cpp
cur->next = cur->next->next;
```

- `cur->next` 原本是第一个节点 `a`，
   现在改为指向第二个节点 `b`，为后续交换做准备。

------

### 🥈 步骤二：让第二个节点指向第一个节点

**Let the second node point to the first node**

```cpp
cur->next->next = a;
```

- 现在的 `cur->next` 是 `b`，
   `b->next = a`，完成 `b -> a` 的指向，完成核心交换动作。

------

### 🥉 步骤三：让第一个节点指向后面的节点

**Let the first node point to the next part of the list**

```cpp
a->next = c;
```

- 原来的第一个节点 `a` 现在应指向 `b` 后的节点 `c`，
   保证链表结构不被破坏。

------

## 🧠 示例图解 | Example Diagram

交换前：`cur -> a -> b -> c`
 交换后：`cur -> b -> a -> c`

------


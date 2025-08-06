# From ChatGpt: about the Space Complexity

------

## 📘 Recursion & Space Complexity | 递归与空间复杂度

> Understanding what determines the space complexity of recursive functions.
>  理解递归函数空间复杂度的决定因素。

------

### 🔍 What Determines Recursion Space Complexity?

### 什么决定了递归的空间复杂度？

**Key formula 公式：**

```text
Space Complexity = Recursion Depth × Space per Stack Frame  
空间复杂度 = 递归深度 × 每一帧栈空间大小
```

------

### ✅ 1. Does Recursion Itself Take Space?

### 递归调用本身会占用空间吗？

> **Yes.** Every time a function calls itself, a new **stack frame** is created on the call stack.
>  **是的。** 每次函数递归调用时，系统会在调用栈上开辟一个新的 **栈帧**。

Even if the function has no local variables, it **still consumes stack space**.
 即使函数体内没有任何变量，**递归本身也会占用栈空间**。

------

### 🧠 What is inside a stack frame?

### 栈帧中包含什么？

| Component           | Example (示例)            | Notes (说明)                             |
| ------------------- | ------------------------- | ---------------------------------------- |
| Function parameters | `int n`, `ListNode* head` | Each call has its own copy of parameters |
| Local variables     | `int x`, `ListNode* tmp`  | Declared inside the function body        |
| Return address      | —                         | Tells where to return after this call    |
| Register context    | —                         | Saved by compiler/runtime automatically  |

> Stack frame size is determined by the function definition itself (parameters + local vars).
>  每帧的大小由函数的形参和局部变量决定。

------

### ✅ 2. Do arguments (passed from outside) affect space complexity?

### 函数调用时传入的实参会影响空间复杂度吗？

> **No.** The caller’s variables are stored in their own stack frame.
>  **不会。** 调用函数时传入的实参属于上一个函数的栈帧，与当前帧无关。

Inside the function, the parameters become new **local copies**, and only these copies are counted.
 函数内部接收的是参数副本，**只副本所在的当前帧会占用空间**。

------

### ✅ 3. How to analyze recursion space complexity?

### 如何分析递归函数的空间复杂度？

1. Count the **maximum recursion depth** (`n` calls → depth = `n`)
    计算递归最大深度
2. Determine how much space each frame takes (usually **O(1)**)
    计算每一帧的空间大小（一般为 O(1)）
3. Multiply: `O(n) × O(1) = O(n)`
    相乘即可得到总复杂度

------

### 🔁 Example: Delete nodes from a linked list (recursive)

```cpp
ListNode* removeElements(ListNode* head, int val) {
    if (head == nullptr) return nullptr;
    if (head->val == val) {
        ListNode* newHead = removeElements(head->next, val);
        delete head;
        return newHead;
    } else {
        head->next = removeElements(head->next, val);
        return head;
    }
}
```

- **Time Complexity:** `O(n)` → Each node is visited once
- **Space Complexity:** `O(n)` → One stack frame per node

------

### ❗ Iteration vs Recursion

| Approach  | Time Complexity | Space Complexity | Notes                   |
| --------- | --------------- | ---------------- | ----------------------- |
| Recursion | O(n)            | O(n)             | Due to call stack       |
| Iteration | O(n)            | O(1)             | Uses loop, no recursion |

------

### 📝 Conclusion | 总结

- Recursive functions **always consume stack space**.
- Space complexity is mainly determined by **recursion depth**, not number of variables.
- Variables outside the function **do not affect** the space complexity.
- If you're memory-sensitive (e.g. handling big data), **prefer iteration**.

> ✅ 最终要记住一句话：
>
> **递归空间复杂度 = 递归深度决定栈帧数量，而栈帧大小由参数和局部变量决定。**

------


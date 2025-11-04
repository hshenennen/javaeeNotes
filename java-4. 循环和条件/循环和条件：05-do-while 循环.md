
---

# Java 中的 `do-while` 循环

> [!info] 学习目标
> - 掌握 `do-while` 的语法和执行流程
> - 理解它与 `while` 循环的核心区别
> - 能在合适场景（如用户输入、菜单）中正确使用
> - 避免常见错误（如忘记分号、无限循环）

---

## 1. 什么是 `do-while` 循环？

`do-while` 是一种**后测试循环结构**：  
它**先执行一次循环体，再判断条件是否继续**。

> 💡 核心特点：**循环体至少执行一次**，无论条件是否成立。

这与 `while`（先判断后执行）形成鲜明对比。

---

## 2. 基本语法

```java
do {
    // 循环体（至少执行一次）
} while (条件表达式); // ⚠️ 注意结尾必须有分号！
```

### 执行流程：
1. 执行 `do` 块中的代码
2. 检查 `while` 后的条件
   - 如果为 `true` → 回到第 1 步，继续循环
   - 如果为 `false` → 退出循环

---

## 3. 与 `while` 循环的对比

| 特性 | `do-while` | `while` |
|------|-----------|--------|
| **条件检查时机** | 循环体**之后** | 循环体**之前** |
| **最少执行次数** | **1 次** | **0 次** |
| **适用场景** | 必须先做一次（如输入、菜单） | 条件不满足时可跳过 |

### 🌰 对比例子

```java
int x = 0;

// while：条件为 false，一次都不执行
while (x > 5) {
    System.out.println("while 执行了");
}

// do-while：先执行一次，再判断
do {
    System.out.println("do-while 执行了");
} while (x > 5);
```

**输出**：
```
do-while 执行了
```

---

## 4. 典型应用场景

### ✅ 1. 用户输入验证（最常见！）
```java
Scanner scanner = new Scanner(System.in);
String input;
do {
    System.out.print("请输入你的名字（非空）: ");
    input = scanner.nextLine();
} while (input.trim().isEmpty());
System.out.println("你好, " + input + "!");
```

> ✅ 优势：确保用户至少输入一次，避免空输入直接跳过。

---

### ✅ 2. 菜单系统
```java
int choice;
do {
    System.out.println("=== 主菜单 ===");
    System.out.println("1. 查看余额");
    System.out.println("2. 存款");
    System.out.println("3. 退出");
    System.out.print("请选择: ");
    choice = scanner.nextInt();
    
    switch (choice) {
        case 1 -> System.out.println("余额: ¥1000");
        case 2 -> System.out.println("存款成功");
        case 3 -> System.out.println("再见！");
        default -> System.out.println("无效选项，请重试");
    }
} while (choice != 3);
```

---

## 5. 注意事项与常见错误

### ⚠️ 1. **忘记结尾分号**
```java
do {
    // ...
} while (condition)  // ❌ 编译错误！缺少分号
```
✅ 正确：
```java
} while (condition);
```

---

### ⚠️ 2. **无限循环风险**
如果循环体内**没有更新条件变量**，可能导致死循环：

```java
int i = 0;
do {
    System.out.println("卡住了！");
    // 忘记 i++ → 条件永远为 true！
} while (i < 5);
```

✅ 修复：确保条件变量在循环体内被修改。

---

### ⚠️ 3. **条件变量作用域**
如果在 `do` 块内声明变量，`while` 中无法访问：

```java
do {
    int x = 10; // 作用域仅限 do 块
} while (x > 5); // ❌ 编译错误：x 找不到
```

✅ 正确做法：在 `do` 外声明变量
```java
int x;
do {
    x = getUserInput();
} while (x <= 0);
```

---

## 6. `do-while` 与 `break` / `continue`

- `break`：立即退出整个 `do-while` 循环
- `continue`：跳过本次剩余代码，**直接回到 while 条件判断**

### 🌰 示例
```java
int n = 1;
do {
    if (n == 3) {
        n++;
        continue; // 跳过打印 3
    }
    if (n > 5) {
        break; // 超过 5 就退出
    }
    System.out.println(n);
    n++;
} while (true); // 用 break 控制退出
```

**输出**：
```
1
2
4
5
```

---

## 7. 小练习

写出以下代码的输出：

```java
int i = 5;
do {
    System.out.print(i + " ");
    i -= 2;
} while (i > 0);
```

<details>
<summary>✅ 答案（点击展开）</summary>

- 第1次：i=5 → 输出 `5 `，i=3  
- 第2次：i=3 → 输出 `3 `，i=1  
- 第3次：i=1 → 输出 `1 `，i=-1  
- 检查条件：i > 0？→ -1 > 0 为 false，退出  
- 输出：**5 3 1**
</details>

---

## 8. 总结：何时使用 `do-while`？

✅ **使用 `do-while` 当且仅当**：
- 你需要**至少执行一次**操作
- **典型场景**：用户输入、密码验证、菜单显示、初始化检查

❌ **不要用 `do-while`**：
- 当可能完全不需要执行循环体时（用 `while` 更安全）

---

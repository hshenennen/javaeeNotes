

---

# Java 中的 `break` 和 `continue` 语句

> [!info] 学习目标
> - 理解 `break` 和 `continue` 的作用与区别  
> - 掌握它们在循环（`for`/`while`/`do-while`）和 `switch` 中的使用  
> - 学会使用**标签（label）** 实现多层循环跳转（了解即可）  
> - 避免常见误用（如在 `if` 中滥用）

---

## 1. 核心作用对比

| 语句 | 作用 | 适用场景 |
|------|------|--------|
| `break` | **立即退出**当前 `switch` 或**最内层循环** | `switch`、`for`、`while`、`do-while` |
| `continue` | **跳过本次循环剩余代码**，直接进入**下一次循环判断** | 仅用于**循环**（`for`/`while`/`do-while`） |

> 💡 记忆口诀：  
> **`break` 是“彻底离开”，`continue` 是“这次跳过，下次再来”**

---

## 2. `break` 的使用

### ✅ 1. 在 `switch` 中
- 用于**防止穿透（fall-through）**
- 执行完当前 `case` 后跳出 `switch`

```java
int day = 2;
switch (day) {
    case 1:
        System.out.println("周一");
        break;
    case 2:
        System.out.println("周二");
        break; // 跳出 switch，不再执行后续 case
    default:
        System.out.println("其他");
}
```

### ✅ 2. 在循环中
- 立即**终止整个循环**，执行循环后的代码

```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break; // 遇到 5 就退出循环
    }
    System.out.print(i + " ");
}
// 输出：1 2 3 4
```

---

## 3. `continue` 的使用

> ⚠️ **只能用于循环中！不能在 `switch` 或普通 `if` 中使用**

- 跳过当前循环体**剩余部分**
- 直接进入**下一次循环的条件判断**（`for` 还会先执行“迭代更新”）

### 🌰 示例：跳过偶数
```java
for (int i = 1; i <= 5; i++) {
    if (i % 2 == 0) {
        continue; // 跳过偶数
    }
    System.out.print(i + " ");
}
// 输出：1 3 5
```

### 🔄 在 `while` 中的行为
```java
int i = 0;
while (i < 5) {
    i++;
    if (i == 3) {
        continue; // 跳过 i=3 时的打印
    }
    System.out.print(i + " ");
}
// 输出：1 2 4 5
```

> 💡 注意：`continue` **不会跳过 `while` 的条件判断**，而是直接回到 `while (条件)` 处。

---

## 4. 带标签的 `break` 和 `continue`（了解）

在**嵌套循环**中，可以用**标签（label）** 指定跳出哪一层。

### 语法：
```java
标签名: for/while/do-while { ... }
```

### 🌰 示例：跳出外层循环
```java
outer: for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (i == 2 && j == 2) {
            break outer; // 直接跳出 outer 标签所在的循环
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
System.out.println("循环结束");
```

**输出**：
```
i=1, j=1
i=1, j=2
i=1, j=3
i=2, j=1
循环结束
```

> ✅ **建议**：初学者尽量避免使用标签，优先用函数封装或布尔标志控制逻辑。

---

## 5. 常见错误与陷阱

> [!danger] 初学者易错点

| 错误 | 说明 | 正确做法 |
|------|------|--------|
| 在 `if` 中单独使用 `break` | `break` 必须在循环或 `switch` 内 | 检查是否在合法上下文中 |
| 误以为 `continue` 跳出循环 | `continue` 只是跳过本次，不是退出 | 用 `break` 退出 |
| 在 `switch` 中用 `continue` | `continue` 不能用于 `switch` | 改用 `break` |
| 忘记 `for` 中 `continue` 会执行“迭代更新” | `for (i=0; i<5; i++) { if(...) continue; }` → `i++` 仍会执行 | 理解执行顺序 |

---

## 6. 小练习

写出以下代码的输出：

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    if (i == 4) {
        break;
    }
    System.out.print(i + " ");
}
```

<details>
<summary>✅ 答案</summary>

- i=1 → 打印 `1 `
- i=2 → 打印 `2 `
- i=3 → `continue`，跳过
- i=4 → 执行 `break`，退出循环
- 输出：**1 2**
</details>

---

## 7. 最佳实践建议

- ✅ **优先用清晰的逻辑代替 `break`/`continue`**（如提前 return、布尔标志）
- ✅ **在 `switch` 中始终写 `break`**（除非故意穿透）
- ✅ **`continue` 适合过滤场景**（如跳过无效数据）
- ❌ **避免在深层嵌套中滥用 `break`/`continue`**，降低可读性

---

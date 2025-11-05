
---

# Java 中的 `while` 循环

> [!info] 学习目标
> - 掌握 `while` 循环的基本语法和执行流程
> - 理解 `while` 与 `do-while` 的区别
> - 能编写安全的循环逻辑（避免无限循环）
> - 学会在合适场景使用 `while`（如用户输入、文件读取）
> - 掌握 `break` 和 `continue` 在循环中的作用

---

## 1. 什么是 `while` 循环？

`while` 是一种**条件循环结构**：只要条件为 `true`，就重复执行代码块。

> 💡 核心思想：**“当……就一直做……”**

适用于**循环次数未知**的场景，例如：
- 用户输入直到输入有效数据
- 读取文件直到末尾
- 游戏运行直到玩家退出

---

## 2. 基本语法

```java
while (条件表达式) {
    // 循环体（重复执行的代码）
}
```

- **条件表达式**必须是 `boolean` 类型（`true`/`false`）
- 每次循环**开始前**检查条件
- 如果初始条件为 `false`，循环体**一次都不执行**

### 🌰 示例：倒计时
```java
int count = 3;
while (count > 0) {
    System.out.println(count);
    count--; // 必须在循环体内更新条件变量！
}
System.out.println("起飞！");
```

**输出**：
```
3
2
1
起飞！
```

---

## 3. `do-while` 循环（至少执行一次）

与 `while` 不同，`do-while` **先执行一次循环体，再判断条件**。

### 语法：
```java
do {
    // 循环体
} while (条件表达式); // 注意结尾有分号！
```

### 🌰 示例：用户输入验证
```java
Scanner scanner = new Scanner(System.in);
int number;
do {
    System.out.print("请输入一个正数: ");
    number = scanner.nextInt();
} while (number <= 0); // 直到输入正数才退出
```

> ✅ 适用场景：**必须至少执行一次**的操作（如菜单、密码输入）

---

## 4. `while` vs `for` vs `do-while`

| 循环类型 | 执行次数 | 适用场景 | 特点 |
|---------|--------|--------|------|
| `for` | 已知或可预估 | 遍历数组、固定次数任务 | 初始化、条件、更新集中 |
| `while` | 0 次或多次 | 条件驱动（如读文件、用户输入） | 条件在前，可能一次都不执行 |
| `do-while` | **至少 1 次** | 需要先执行再判断（如菜单） | 条件在后，保证执行一次 |

---

## 5. 避免无限循环

如果**条件永远为 `true`**，或**忘记更新条件变量**，就会陷入无限循环！

### ❌ 危险示例
```java
int i = 0;
while (i < 5) {
    System.out.println("卡住了！");
    // 忘记 i++ → 条件永远为 true！
}
```

### ✅ 安全写法
- 确保循环体内有**改变条件的语句**
- 复杂逻辑可加**安全计数器**防死循环

```java
int attempts = 0;
while (!isValid && attempts < 10) {
    // 尝试操作
    attempts++;
}
```

---

## 6. `break` 和 `continue` 在 `while` 中的使用

| 语句 | 作用 |
|------|------|
| `break;` | **立即退出整个循环** |
| `continue;` | **跳过本次剩余代码，直接进入下一次条件判断** |

### 🌰 示例：跳过偶数，遇到 7 停止
```java
int n = 1;
while (n <= 10) {
    if (n % 2 == 0) {
        n++;
        continue; // 跳过偶数
    }
    if (n == 7) {
        break; // 遇到 7 停止
    }
    System.out.println(n);
    n++;
}
// 输出：1 3 5
```

---

## 7. 常见应用场景

| 场景 | 示例 |
|------|------|
| 用户输入验证 | `while (input.isEmpty())` |
| 文件读取 | `while ((line = reader.readLine()) != null)` |
| 游戏主循环 | `while (gameRunning) { update(); render(); }` |
| 数值逼近 | `while (Math.abs(error) > 0.001)` |

---

## 8. 小练习

写出以下代码的输出：

```java
int x = 5;
while (x > 0) {
    if (x % 2 == 0) {
        x -= 2;
        continue;
    }
    System.out.print(x + " ");
    x--;
}
```

<details>
<summary>✅ 答案</summary>

- x=5 → 奇数 → 输出 `5 `，x=4  
- x=4 → 偶数 → x=2，continue  
- x=2 → 偶数 → x=0，continue  
- x=0 → 条件 `x>0` 为 false，循环结束  
- 输出：**5**
</details>

---

## 9. 常见错误总结

> [!danger] 初学者易错点

| 错误 | 说明 |
|------|------|
| 忘记更新循环变量 | 导致无限循环 |
| `do-while` 忘记结尾分号 | 编译错误 |
| 条件写成赋值 | `while (x = 5)` → 应为 `==`（但 `x=5` 是 int，会编译错误） |
| 在循环外使用循环变量未初始化 | `int i; while (...) { i = ... } System.out.println(i);` → 可能未初始化 |

---

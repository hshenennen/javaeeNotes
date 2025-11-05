

---

# Java 中的 `Scanner`：获取用户输入

> [!info] 学习目标
> - 掌握 `Scanner` 的基本用法  
> - 学会读取不同类型的数据（字符串、整数、浮点数等）  
> - 理解并解决常见输入陷阱（如换行符残留）  
> - 能编写安全的用户交互程序（如菜单、表单）

---

## 1. 什么是 `Scanner`？

`Scanner` 是 Java 标准库（`java.util` 包）中的一个类，用于**从控制台（或其他输入源）读取用户输入**。

> 💡 用途：实现**交互式程序**（如计算器、登录、游戏）

---

## 2. 基本使用步骤

### ✅ 步骤 1：导入包
```java
import java.util.Scanner;
```

### ✅ 步骤 2：创建 `Scanner` 对象
```java
Scanner scanner = new Scanner(System.in);
```
- `System.in` 表示从**标准输入**（通常是键盘）读取

### ✅ 步骤 3：调用方法读取数据
```java
String name = scanner.nextLine(); // 读取一行字符串
int age = scanner.nextInt();      // 读取一个整数
```

### ✅ 步骤 4：关闭 `Scanner`（可选但推荐）
```java
scanner.close();
```
> ⚠️ 注意：如果关闭了 `System.in` 的 `Scanner`，后续无法再从控制台读取输入（在简单程序中可省略）

---

## 3. 常用读取方法

| 方法 | 说明 | 示例 |
|------|------|------|
| `nextLine()` | 读取**整行**（包括空格），以回车结束 | `"Hello World"` |
| `next()` | 读取**一个单词**（遇到空格/换行停止） | `"Hello"`（输入 `"Hello World"` 时） |
| `nextInt()` | 读取一个 `int` 整数 | `42` |
| `nextDouble()` | 读取一个 `double` 浮点数 | `3.14` |
| `nextBoolean()` | 读取 `true`/`false` | `true` |

### 🌰 示例：完整用户信息输入
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("请输入姓名: ");
        String name = scanner.nextLine();
        
        System.out.print("请输入年龄: ");
        int age = scanner.nextInt();
        
        System.out.print("请输入身高(m): ");
        double height = scanner.nextDouble();
        
        System.out.println("你好, " + name + "！你今年 " + age + " 岁，身高 " + height + " 米。");
        
        scanner.close();
    }
}
```

---

## 4. ⚠️ 常见陷阱：换行符残留问题

### ❌ 问题场景：
在 `nextInt()`、`nextDouble()` 等方法后**立即使用 `nextLine()`**，会导致 `nextLine()` 读取到**空字符串**！

```java
Scanner sc = new Scanner(System.in);
System.out.print("年龄: ");
int age = sc.nextInt(); // 用户输入 25 + 回车

System.out.print("姓名: ");
String name = sc.nextLine(); // ❌ 读取到的是回车符后的空行！
```

### 🔍 原因：
- `nextInt()` 只读取数字，**不消耗回车符 `\n`**
- 下一个 `nextLine()` 立即读取到这个残留的 `\n`，返回空字符串

### ✅ 解决方案：

#### 方法 1：在 `nextInt()` 后加一个 `nextLine()` 消费换行符
```java
int age = sc.nextInt();
sc.nextLine(); // 消费掉残留的换行符
String name = sc.nextLine();
```

#### 方法 2：**全部使用 `nextLine()` + 手动转换**
```java
String ageStr = sc.nextLine();
int age = Integer.parseInt(ageStr); // 字符串转整数

String heightStr = sc.nextLine();
double height = Double.parseDouble(heightStr);
```
> ✅ 优点：避免混合使用，逻辑更清晰，适合初学者

---

## 5. 输入验证（健壮性处理）

用户可能输入非法数据（如要求输入数字却输入字母），需用 `try-catch` 或循环验证。

### 🌰 示例：确保输入有效整数
```java
Scanner sc = new Scanner(System.in);
int number;
while (true) {
    System.out.print("请输入一个正整数: ");
    if (sc.hasNextInt()) { // 先检查是否为整数
        number = sc.nextInt();
        if (number > 0) break; // 符合条件，退出循环
    }
    System.out.println("输入无效，请重试！");
    sc.nextLine(); // 清除错误输入
}
System.out.println("你输入的是: " + number);
```

> 💡 `hasNextInt()`、`hasNextDouble()` 等方法用于**预检查输入类型**

---

## 6. 其他输入源（扩展知识）

`Scanner` 不仅能读控制台，还能读文件、字符串等：

```java
// 从字符串读取
Scanner sc = new Scanner("10 20 30");
int a = sc.nextInt(); // 10

// 从文件读取（需处理异常）
Scanner fileScanner = new Scanner(new File("data.txt"));
```

> 初学者重点掌握 `System.in` 即可。

---

## 7. 小练习

以下代码存在什么问题？如何修复？

```java
Scanner sc = new Scanner(System.in);
System.out.print("输入整数: ");
int x = sc.nextInt();
System.out.print("输入字符串: ");
String s = sc.nextLine();
System.out.println("x=" + x + ", s='" + s + "'");
```

<details>
<summary>✅ 答案</summary>

**问题**：`s` 会是空字符串，因为 `nextInt()` 后残留的换行符被 `nextLine()` 读取。

**修复**：在 `nextInt()` 后加 `sc.nextLine()`：
```java
int x = sc.nextInt();
sc.nextLine(); // 消费换行符
String s = sc.nextLine();
```
</details>

---

## 8. 最佳实践总结

- ✅ **初学者建议**：优先使用 `nextLine()` + `Integer.parseInt()` 等转换，避免混合方法
- ✅ **始终验证用户输入**，防止程序崩溃
- ✅ **提示清晰**：`System.out.print("请输入年龄: ")`
- ❌ **不要频繁创建/关闭 Scanner**：一个程序通常一个 `Scanner` 足够
- ⚠️ **注意换行符残留**：这是最常见的输入 bug！

---


---

# 🔤 Java 字符（`char`）的基本认识

> [!info] 学习目标
> - 理解 `char` 是 Java 的基本数据类型  
> - 掌握字符的表示方式（单引号、转义字符、Unicode）  
> - 能进行字符与数字之间的转换（ASCII/Unicode）  
> - 区分 `char` 与 `String`  
> - 了解常见字符操作（如判断大小写、数字等）

> 🏷️ 标签：`#java/基础` `#数据类型` `#char` `#编码`

---

## 1. 什么是 `char`？

- `char` 是 Java 中表示**单个字符**的基本数据类型
- 占用 **2 个字节（16 位）**
- 基于 **Unicode 编码**（支持中文、英文、符号等）
- **必须用单引号 `' '` 包裹**

### ✅ 示例：
```java
char c1 = 'A';      // 英文字母
char c2 = '中';     // 中文字符（Unicode 支持）
char c3 = '5';      // 数字字符（不是数字 5！）
char c4 = '!';      // 符号
char c5 = ' ';      // 空格
```

> ⚠️ 注意：`"A"` 是字符串（`String`），`'A'` 才是字符（`char`）

---

## 2. 字符的三种表示方式

| 方式 | 语法 | 示例 |
|------|------|------|
| **普通字符** | `'X'` | `'a'`, `'9'`, `'@'` |
| **转义字符** | `'\n'`, `'\t'` 等 | `'\n'`（换行），`'\''`（单引号） |
| **Unicode 编码** | `'\uXXXX'` | `'\u0041'` → `'A'`，`'\u4e2d'` → `'中'` |

### 🔸 转义字符常用表：
| 转义序列 | 含义 |
|--------|------|
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\\` | 反斜杠 |
| `\n` | 换行 |
| `\t` | 制表符（Tab） |
| `\r` | 回车 |

### 🔸 示例代码：
```java
char quote = '\'';        // 单引号字符
char newline = '\n';      // 换行符（不可见）
char unicodeA = '\u0041'; // 等价于 'A'
System.out.println(unicodeA); // 输出 A
```

---

## 3. `char` 与整数的转换（重要！）

由于 `char` 基于 Unicode，每个字符都有对应的**数值编码**，因此可以和 `int` 互相转换。

### ✅ 字符 → 数字（获取编码）
```java
char c = 'A';
int code = (int) c; // 强制类型转换
System.out.println(code); // 输出 65（ASCII 值）
```

### ✅ 数字 → 字符（通过编码生成字符）
```java
int code = 66;
char c = (char) code;
System.out.println(c); // 输出 B
```

### 🌰 应用：输出连续字母
```java
for (char c = 'A'; c <= 'Z'; c++) {
    System.out.print(c + " ");
}
// 输出：A B C ... Z
```

> 💡 原理：`char` 在运算时会自动提升为 `int`，所以 `c++` 实际是编码值 +1

---

## 4. 常见字符判断（结合条件语句）

虽然初学不使用方法，但可通过编码范围手动判断：

| 判断类型 | 条件表达式 | 说明 |
|--------|----------|------|
| 大写字母 | `c >= 'A' && c <= 'Z'` | A~Z |
| 小写字母 | `c >= 'a' && c <= 'z'` | a~z |
| 数字字符 | `c >= '0' && c <= '9'` | '0'~'9'（注意是字符！） |

### 🔸 示例：判断输入字符类型
```java
import java.util.Scanner;

public class CharType {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入一个字符: ");
        char c = sc.next().charAt(0); // 读取第一个字符

        if (c >= 'A' && c <= 'Z') {
            System.out.println("这是大写字母");
        } else if (c >= 'a' && c <= 'z') {
            System.out.println("这是小写字母");
        } else if (c >= '0' && c <= '9') {
            System.out.println("这是数字字符");
        } else {
            System.out.println("这是其他字符");
        }

        sc.close();
    }
}
```

> 📌 说明：`sc.next().charAt(0)` 表示读取一个字符串并取其第一个字符

---

## 5. `char` vs `String`（关键区别）

| 特性 | `char` | `String` |
|------|--------|--------|
| 类型 | 基本数据类型 | 引用类型（类） |
| 表示 | 单个字符 | 一串字符（可为空） |
| 引号 | 单引号 `'A'` | 双引号 `"A"` |
| 内存 | 固定 2 字节 | 动态长度 |
| 示例 | `char c = 'X';` | `String s = "Hello";` |

> ❌ 错误示例：
> ```java
> char c = "A"; // 编译错误！不能用双引号
> ```

---

## 6. 小练习与测试

### 💬 问题：以下代码输出什么？
```java
char c = '5';
int n = c;
System.out.println(n);
```

<details>
<summary>✅ 答案</summary>

输出：**53**

> 💡 解析：字符 `'5'` 的 ASCII 编码是 53，不是数字 5！  
> 若想得到数字 5，需用：`int digit = c - '0';`
</details>



---

> ✅ **总结**：  
> `char` 虽小，却是理解**字符编码、输入处理、文本操作**的基础。掌握它，你就能轻松处理字母、数字字符、符号等基本元素！

---


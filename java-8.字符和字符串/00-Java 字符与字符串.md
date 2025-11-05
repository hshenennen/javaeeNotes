
---

# 📚  学习指南  
> 🎯 适合：Java 初学者 | 面试准备 | 基础巩固

> [!info] 本指南将带你从零开始，逐步掌握 `char` 与 `String` 的本质、API 使用、常见陷阱与面试考点。

> 🏷️ 标签：`#java/字符` `#java/字符串` `#基础学习` `#预习指南`


---

## 🧭 学习路线图（对应你的目录）

| 步骤 | 模块 | 学习目标 | 输出成果 |
|------|------|---------|----------|
| ① | `01-char` | 理解 `char` 类型的本质、Unicode 支持、存储方式 | 掌握 `char` 的基本用法 |
| ② | `02-Character API` | 掌握 `Character` 类的常用方法（判别、转换） | 能判断字母、数字、大小写等 |
| ③ | `03-String` | 理解 `String` 是引用类型、不可变性、内存模型 | 理解 `==` vs `equals()` |
| ④ | `04-String 方法` | 熟练使用 `length()`、`charAt()`、`substring()`、`indexOf()` 等 | 能处理文本提取、清洗、比较 |
| ⑤ | `05-速查表` | 整合知识，形成快速查阅能力 | 打造个人“API 小抄” |

---

## ✅ 各阶段详细学习建议

### 🔹 [[01-char]]

#### 📌 学习重点：
- `char` 是 **基本数据类型**，占 2 字节（16 位）
- 使用单引号 `' '` 包裹
- 支持 Unicode：包括中文、表情符号、希腊字母等
- 可以直接赋值为数字（ASCII 或 Unicode）

#### 💡 示例：
```java
char c1 = 'A';           // 字母
char c2 = '中';          // 中文
char c3 = '\u4E2D';      // Unicode 编码
char c4 = 65;            // ASCII 码值（'A'）
```

#### ❗ 注意：
- 不要用双引号 `" "`，那是 `String`
- `char` 不可为 `null`，默认值是 `\u0000`（空字符）

#### ✅ 练习：
1. 定义一个 `char` 变量，存储你的名字首字母
2. 打印出 `'a'` 的 ASCII 码值（用 `(int)` 强转）
3. 尝试存储一个表情符号（如 `'😊'`）

---

### 🔹 [[02-char（Character）的常用API]]

#### 📌 学习重点：
- `Character` 是 `char` 的包装类（位于 `java.lang`）
- 提供大量静态方法来判断和转换字符
- 所有方法都是 `static`，调用方式：`Character.xxx(c)`

#### 📊 必须掌握的 8 个方法：

| 方法 | 功能 | 示例 |
|------|------|------|
| `isLetter(c)` | 是否为字母（含中文） | `Character.isLetter('中') → true` |
| `isDigit(c)` | 是否为数字 | `Character.isDigit('5') → true` |
| `isWhitespace(c)` | 是否为空白字符 | `Character.isWhitespace(' ') → true` |
| `isUpperCase(c)` | 是否为大写字母 | `Character.isUpperCase('B') → true` |
| `isLowerCase(c)` | 是否为小写字母 | `Character.isLowerCase('x') → true` |
| `toUpperCase(c)` | 转为大写 | `Character.toUpperCase('a') → 'A'` |
| `toLowerCase(c)` | 转为小写 | `Character.toLowerCase('Z') → 'z'` |
| `isAlphabetic(c)` | 是否为广义字母（Unicode） | `Character.isAlphabetic('α') → true` |

#### ✅ 练习：
1. 写一个程序，判断用户输入的字符是否为字母或数字
2. 实现一个函数：将字符串中的所有小写字母转为大写
3. 验证 `'中'` 是否为字母（`isLetter`）

---

### 🔹 [[03-String]]

#### 📌 学习重点：
- `String` 是 **引用类型**，不是基本类型
- 用双引号 `" "` 包裹
- **不可变（Immutable）**：一旦创建，内容不能更改
- 存储在 **字符串常量池（String Pool）** 中（节省内存）

#### 💡 示例：
```java
String s1 = "Hello";     // 放入常量池
String s2 = "Hello";     // 指向同一对象
String s3 = new String("Hello"); // 堆中新建对象
```

#### ⚠️ 关键概念：
- `==` 比较的是 **引用地址**
- `equals()` 比较的是 **内容**

```java
System.out.println(s1 == s2);        // true（同一个对象）
System.out.println(s1 == s3);        // false（不同对象）
System.out.println(s1.equals(s3));   // true（内容相同）
```

#### ✅ 练习：
1. 创建两个相同的字符串，分别用字面量和 `new`，比较 `==` 和 `equals()`
2. 尝试修改字符串内容（如 `s1[0] = 'X'`），观察编译错误
3. 用 `""` 创建空字符串，并检查长度

---

### 🔹[[04-String 类常用方法]]

#### 📌 学习重点：
- 掌握最常用的 10+ 个方法
- 理解 **不可变性**：所有操作返回新字符串
- 熟悉索引规则（从 0 开始，`substring` 左闭右开）

#### 📊 必须掌握的方法：

| 方法 | 功能 | 示例 |
|------|------|------|
| `length()` | 获取长度 | `"abc".length()` → `3` |
| `charAt(int index)` | 获取指定位置字符 | `"abc".charAt(1)` → `'b'` |
| `equals(Object obj)` | 内容比较 | `"a".equals("A")` → `false` |
| `equalsIgnoreCase()` | 忽略大小写比较 | `"A".equalsIgnoreCase("a")` → `true` |
| `toUpperCase()` / `toLowerCase()` | 大小写转换 | `"hi".toUpperCase()` → `"HI"` |
| `trim()` | 去除首尾空白 | `"  ok  ".trim()` → `"ok"` |
| `substring(int begin)`<br>`substring(int begin, int end)` | 截取子串 | `"Hello".substring(1,4)` → `"ell"` |
| `indexOf(String str)` | 查找首次出现位置 | `"abc".indexOf('b')` → `1` |
| `lastIndexOf(String str)` | 查找最后一次 | `"aabbcc".lastIndexOf("b")` → `3` |
| `startsWith()` / `endsWith()` | 是否以某前缀/后缀开头/结尾 | `"file.txt".endsWith(".txt")` → `true` |
| `replace(char old, char new)` | 替换所有匹配项 | `"12-34".replace('-', '/')` → `"12/34"` |

#### ✅ 练习：
1. 提取邮箱中的用户名（`@` 前部分）
2. 判断字符串是否以 `.txt` 结尾
3. 将 `"hello world"` 中的所有空格替换为 `_`

---

### 🔹 [[05-String 类常用方法速查表]]

> 📌 常用方法速查表

| 方法 | 功能 | 参数 | 返回值 | 示例 |
|------|------|------|--------|------|
| `length()` | 长度 | 无 | `int` | `"abc".length()` → `3` |
| `charAt(int index)` | 取字符 | 索引 | `char` | `"abc".charAt(1)` → `'b'` |
| `equals(Object obj)` | 内容相等？ | 对象 | `boolean` | `"a".equals("A")` → `false` |
| `equalsIgnoreCase(String str)` | 忽略大小写比较 | 字符串 | `boolean` | `"A".equalsIgnoreCase("a")` → `true` |
| `toUpperCase()` | 转大写 | 无 | `String` | `"hi".toUpperCase()` → `"HI"` |
| `toLowerCase()` | 转小写 | 无 | `String` | `"HELLO".toLowerCase()` → `"hello"` |
| `trim()` | 去首尾空格 | 无 | `String` | `"  ok  ".trim()` → `"ok"` |
| `substring(int begin)` | 截取从开始到末尾 | 起始索引 | `String` | `"Hello".substring(1)` → `"ello"` |
| `substring(int begin, int end)` | 截取区间 | 起止索引 | `String` | `"Hello".substring(1,4)` → `"ell"` |
| `indexOf(String str)` | 查找首次位置 | 子串 | `int` | `"abc".indexOf('b')` → `1` |
| `lastIndexOf(String str)` | 查找最后位置 | 子串 | `int` | `"aabbcc".lastIndexOf("b")` → `3` |
| `startsWith(String prefix)` | 是否以前缀开头 | 前缀 | `boolean` | `"https://...".startsWith("https")` → `true` |
| `endsWith(String suffix)` | 是否以后缀结尾 | 后缀 | `boolean` | `"file.txt".endsWith(".txt")` → `true` |
| `replace(char old, char new)` | 替换所有 | 旧字符、新字符 | `String` | `"12-34".replace('-', '/')` → `"12/34"` |

> ✅ **记忆口诀**：  
> **“长用 `length`，取用 `charAt`，比用 `equals`，转用 `toXxx`，去空用 `trim`，截用 `substring`，查用 `indexOf`，前后用 `start/endWith`，换用 `replace`！”**


---

> ✅ **总结**：  
> 字符与字符串是 Java 的“语言之基”。掌握它们，你才能：
> - 正确处理用户输入
> - 实现文本解析、清洗、验证
> - 理解集合、泛型、IO 等高级功能的前提

---

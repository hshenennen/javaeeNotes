
---

# 📚 Java String 类常用方法

> [!info] 说明  
> - 所有方法均为 `String` 实例方法（需通过对象调用）  
> - `String` 是不可变类，所有操作返回新字符串  
> - 支持 Unicode 字符（包括中文、符号等）

> 🏷️ 标签：`#java/String` `#API文档` `#字符串处理`

---

 > 🏷️[[05-String 类常用方法速查表]]
---


## ✅ 1. `length()` 方法

### 📄 方法描述
获取字符串的长度（字符个数）。

| 类型 | 方法及描述 |
|------|------------|
| int | `length()`<br>返回该字符串中字符的数量。 |

### 💬 参数
- 无参数

### 🔄 返回值
- `int` 类型，表示字符串的长度

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "Hello";
        System.out.println(str.length()); // 输出: 5
    }
}
```

---

## ✅ 2. `charAt(int index)` 方法

### 📄 方法描述
返回指定索引位置的字符。

| 类型 | 方法及描述 |
|------|------------|
| char | `charAt(int index)`<br>返回该字符串中指定索引处的字符。索引从 0 开始。 |

### 💬 参数
- `index`：要获取字符的位置（整数）

### 🔄 返回值
- `char` 类型，对应位置的字符

### ⚠️ 异常
- 如果 `index` 超出范围，抛出 `StringIndexOutOfBoundsException`

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "Java";
        System.out.println(str.charAt(0)); // 输出: J
        System.out.println(str.charAt(3)); // 输出: a
    }
}
```

---

## ✅ 3. `equals(Object obj)` 方法

### 📄 方法描述
比较两个字符串的内容是否相等。

| 类型 | 方法及描述 |
|------|------------|
| boolean | `equals(Object obj)`<br>如果此字符串与指定对象相等，则返回 `true`；否则返回 `false`。 |

### 💬 参数
- `obj`：要比较的对象（通常为 `String`）

### 🔄 返回值
- `true`：内容相同  
- `false`：内容不同或类型不匹配

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "hello";
        String s3 = "HELLO";

        System.out.println(s1.equals(s2)); // true
        System.out.println(s1.equals(s3)); // false
    }
}
```

---

## ✅ 4. `equalsIgnoreCase(String str)` 方法

### 📄 方法描述
忽略大小写比较两个字符串是否相等。

| 类型 | 方法及描述 |
|------|------------|
| boolean | `equalsIgnoreCase(String str)`<br>如果此字符串与指定字符串内容相同（忽略大小写），则返回 `true`；否则返回 `false`。 |

### 💬 参数
- `str`：要比较的字符串

### 🔄 返回值
- `true`：内容相同（不区分大小写）  
- `false`：不同

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String s1 = "Java";
        String s2 = "java";

        System.out.println(s1.equalsIgnoreCase(s2)); // true
    }
}
```

---

## ✅ 5. `toUpperCase()` 方法

### 📄 方法描述
将字符串转换为大写形式。

| 类型 | 方法及描述 |
|------|------------|
| String | `toUpperCase()`<br>返回一个新字符串，其中所有字符都转换为大写。 |

### 💬 参数
- 无参数

### 🔄 返回值
- `String` 类型，大写版本的新字符串

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "hello";
        System.out.println(str.toUpperCase()); // HELLO
    }
}
```

---

## ✅ 6. `toLowerCase()` 方法

### 📄 方法描述
将字符串转换为小写形式。

| 类型 | 方法及描述 |
|------|------------|
| String | `toLowerCase()`<br>返回一个新字符串，其中所有字符都转换为小写。 |

### 💬 参数
- 无参数

### 🔄 返回值
- `String` 类型，小写版本的新字符串

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "HELLO";
        System.out.println(str.toLowerCase()); // hello
    }
}
```

---

## ✅ 7. `trim()` 方法

### 📄 方法描述
去除字符串首尾的空白字符（空格、制表符、换行等）。

| 类型 | 方法及描述 |
|------|------------|
| String | `trim()`<br>返回一个新字符串，移除首尾空白字符。 |

### 💬 参数
- 无参数

### 🔄 返回值
- `String` 类型，去除了首尾空白的新字符串

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "  Hello World  ";
        System.out.println("'" + str.trim() + "'"); // 'Hello World'
    }
}
```

---

## ✅ 8. `substring(int beginIndex)` 方法

### 📄 方法描述
截取从指定索引开始到末尾的子字符串。

| 类型 | 方法及描述 |
|------|------------|
| String | `substring(int beginIndex)`<br>返回从 `beginIndex` 到字符串末尾的子字符串。 |

### 💬 参数
- `beginIndex`：起始索引（包含）

### 🔄 返回值
- `String` 类型，子字符串

### ⚠️ 异常
- 若 `beginIndex` 超出范围，抛出 `StringIndexOutOfBoundsException`

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "Hello";
        System.out.println(str.substring(1)); // ello
    }
}
```

---

## ✅ 9. `substring(int beginIndex, int endIndex)` 方法

### 📄 方法描述
截取从 `beginIndex` 到 `endIndex`（不包含）之间的子字符串。

| 类型 | 方法及描述 |
|------|------------|
| String | `substring(int beginIndex, int endIndex)`<br>返回从 `beginIndex` 到 `endIndex`（不含）的子字符串。 |

### 💬 参数
- `beginIndex`：起始索引（包含）
- `endIndex`：结束索引（不包含）

### 🔄 返回值
- `String` 类型，子字符串

### ⚠️ 异常
- 若索引越界，抛出 `StringIndexOutOfBoundsException`

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "Hello";
        System.out.println(str.substring(1, 4)); // ell
    }
}
```

---

## ✅ 10. `indexOf(String str)` 方法

### 📄 方法描述
查找指定子字符串首次出现的位置。

| 类型 | 方法及描述 |
|------|------------|
| int | `indexOf(String str)`<br>返回指定子字符串首次出现的索引；若未找到，返回 `-1`。 |

### 💬 参数
- `str`：要查找的子字符串

### 🔄 返回值
- `int` 类型：首次出现的索引，或 `-1`（未找到）

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "Hello World";
        System.out.println(str.indexOf("World")); // 6
        System.out.println(str.indexOf("Java"));  // -1
    }
}
```

---

## ✅ 11. `lastIndexOf(String str)` 方法

### 📄 方法描述
查找指定子字符串最后一次出现的位置。

| 类型 | 方法及描述 |
|------|------------|
| int | `lastIndexOf(String str)`<br>返回指定子字符串最后一次出现的索引；若未找到，返回 `-1`。 |

### 💬 参数
- `str`：要查找的子字符串

### 🔄 返回值
- `int` 类型：最后一次出现的索引，或 `-1`（未找到）

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "aabbccbb";
        System.out.println(str.lastIndexOf("bb")); // 6
    }
}
```

---

## ✅ 12. `startsWith(String prefix)` 方法

### 📄 方法描述
判断字符串是否以指定前缀开头。

| 类型 | 方法及描述 |
|------|------------|
| boolean | `startsWith(String prefix)`<br>如果此字符串以指定前缀开头，则返回 `true`；否则返回 `false`。 |

### 💬 参数
- `prefix`：要检查的前缀

### 🔄 返回值
- `true`：以该前缀开头  
- `false`：不是

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "http://example.com";
        System.out.println(str.startsWith("http")); // true
    }
}
```

---

## ✅ 13. `endsWith(String suffix)` 方法

### 📄 方法描述
判断字符串是否以指定后缀结尾。

| 类型 | 方法及描述 |
|------|------------|
| boolean | `endsWith(String suffix)`<br>如果此字符串以指定后缀结尾，则返回 `true`；否则返回 `false`。 |

### 💬 参数
- `suffix`：要检查的后缀

### 🔄 返回值
- `true`：以该后缀结尾  
- `false`：不是

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "file.txt";
        System.out.println(str.endsWith(".txt")); // true
    }
}
```

---

## ✅ 14. `replace(char oldChar, char newChar)` 方法

### 📄 方法描述
替换字符串中所有指定字符。

| 类型 | 方法及描述 |
|------|------------|
| String | `replace(char oldChar, char newChar)`<br>返回一个新字符串，其中所有 `oldChar` 都被替换为 `newChar`。 |

### 💬 参数
- `oldChar`：要替换的字符
- `newChar`：替换后的字符

### 🔄 返回值
- `String` 类型，替换后的新字符串

### 🧪 示例代码
```java
public class Test {
    public static void main(String[] args) {
        String str = "123-456-789";
        System.out.println(str.replace('-', '/')); // 123/456/789
    }
}
```


---

> ✅ **总结**：  
> 这些是 Java `String` 最核心、最常用的方法。掌握它们，你可以轻松实现：
> - 字符串清洗（`trim()`）
> - 内容比较（`equals()` / `equalsIgnoreCase()`）
> - 子串提取（`substring()`）
> - 查找定位（`indexOf()` / `lastIndexOf()`）
> - 格式转换（`toUpperCase()` / `toLowerCase()`）
> - 简单替换（`replace()`）

---


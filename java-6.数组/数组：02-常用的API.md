
---

# Java 数组常用 API（`java.util.Arrays` 类）

> [!info] 学习目标
> - 掌握 `Arrays` 工具类的核心方法  
> - 能高效完成数组的打印、排序、查找、比较等操作  
> - 理解这些 API 的使用场景与注意事项

> 💡 提示：Java 原生数组**没有内置方法**（如 `arr.sort()`），所有高级操作都通过 **`java.util.Arrays`** 工具类提供。

---

## 1. 导入 `Arrays` 类

```java
import java.util.Arrays;
```

> ⚠️ 必须导入才能使用以下方法！

---

## 2. 常用 API 一览表

| 方法 | 作用 | 示例 |
|------|------|------|
| `Arrays.toString(arr)` | 将一维数组转为字符串（便于打印） | `"[1, 2, 3]"` |
| `Arrays.deepToString(arr)` | 打印多维数组 | `"[[1, 2], [3, 4]]"` |
| `Arrays.sort(arr)` | 对数组**升序排序**（原地修改） | `{3,1,2} → {1,2,3}` |
| `Arrays.binarySearch(arr, key)` | **二分查找**（需先排序！） | 返回索引或负数 |
| `Arrays.equals(arr1, arr2)` | 判断两个数组内容是否相等 | `true` / `false` |
| `Arrays.fill(arr, value)` | 用指定值填充整个数组 | `{0,0,0} → {5,5,5}` |
| `Arrays.copyOf(arr, newLength)` | 复制数组（可扩容/缩容） | 新数组长度可不同 |
| `Arrays.copyOfRange(arr, from, to)` | 复制数组的某一段 | `[from, to)` |

---

## 3. 详细说明与示例

### ✅ 1. `Arrays.toString()` —— 安全打印数组
```java
int[] nums = {10, 20, 30};
System.out.println(nums);           // ❌ 输出类似 [I@1b6d3586
System.out.println(Arrays.toString(nums)); // ✅ [10, 20, 30]
```

> 📌 适用于：`int[]`, `double[]`, `String[]` 等一维数组

---

### ✅ 2. `Arrays.deepToString()` —— 打印二维及以上数组
```java
int[][] matrix = {{1, 2}, {3, 4}};
System.out.println(Arrays.deepToString(matrix)); // [[1, 2], [3, 4]]
```

---

### ✅ 3. `Arrays.sort()` —— 快速排序
```java
int[] arr = {5, 2, 8, 1};
Arrays.sort(arr);
System.out.println(Arrays.toString(arr)); // [1, 2, 5, 8]

// 字符串数组按字典序排序
String[] words = {"banana", "apple", "cherry"};
Arrays.sort(words); // ["apple", "banana", "cherry"]
```

> ⚠️ 注意：
> - **原地排序**：直接修改原数组
> - 对象数组需实现 `Comparable` 接口（如 `String` 已实现）

---

### ✅ 4. `Arrays.binarySearch()` —— 高效查找
```java
int[] arr = {1, 2, 5, 8}; // 必须已排序！
int index = Arrays.binarySearch(arr, 5); // 返回 2
int notFound = Arrays.binarySearch(arr, 3); // 返回负数（插入点）
```

> 🔍 规则：
> - 找到：返回**索引**
> - 未找到：返回 `-(插入点 + 1)`（如 `-3` 表示应在索引 2 插入）

---

### ✅ 5. `Arrays.equals()` —— 内容比较
```java
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
int[] c = {1, 2};

System.out.println(Arrays.equals(a, b)); // true
System.out.println(Arrays.equals(a, c)); // false
```

> ❌ 不要用 `==` 或 `arr1.equals(arr2)`！它们比较的是**引用地址**

---

### ✅ 6. `Arrays.fill()` —— 批量赋值
```java
int[] arr = new int[5];
Arrays.fill(arr, 7);
System.out.println(Arrays.toString(arr)); // [7, 7, 7, 7, 7]

// 填充部分区域（重载方法）
Arrays.fill(arr, 1, 3, 99); // 索引 [1,3) → [7,99,99,7,7]
```

---

### ✅ 7. `Arrays.copyOf()` —— 安全扩容/缩容
```java
int[] original = {1, 2, 3};
int[] copy1 = Arrays.copyOf(original, 5); // 扩容 → [1,2,3,0,0]
int[] copy2 = Arrays.copyOf(original, 2); // 缩容 → [1,2]
```

> 💡 底层使用 `System.arraycopy()`，比手动复制更安全高效

---

### ✅ 8. `Arrays.copyOfRange()` —— 截取子数组
```java
int[] arr = {10, 20, 30, 40, 50};
int[] sub = Arrays.copyOfRange(arr, 1, 4); // [20, 30, 40]
```

> 📌 范围：`[from, to)`，包含 `from`，不包含 `to`

---

## 4. ⚠️ 常见误区与注意事项

| 问题 | 说明 |
|------|------|
| **忘记排序就二分查找** | `binarySearch` 要求数组已排序，否则结果不可靠 |
| **直接比较数组用 `==`** | 比较的是内存地址，不是内容 → 用 `Arrays.equals()` |
| **修改 `sort` 后的数组影响原数据** | `sort` 是原地操作，会改变原数组 |
| **对 `null` 数组调用 API** | 会抛出 `NullPointerException`，使用前检查非空 |

---

## 5. 实用技巧：结合循环与 API

### 🌰 示例：统计成绩并分析
```java
import java.util.Arrays;

public class ScoreAnalysis {
    public static void main(String[] args) {
        int[] scores = {85, 92, 78, 96, 88};
        
        // 排序后找最高/最低
        int[] sorted = Arrays.copyOf(scores, scores.length);
        Arrays.sort(sorted);
        int min = sorted[0];
        int max = sorted[sorted.length - 1];
        
        // 计算平均分
        double avg = Arrays.stream(scores).average().orElse(0.0); // Java 8+
        
        System.out.println("原始成绩: " + Arrays.toString(scores));
        System.out.println("最高分: " + max + ", 最低分: " + min);
        System.out.println("平均分: " + String.format("%.2f", avg));
    }
}
```

> 💡 提示：Java 8+ 可用 `Arrays.stream()` 进行函数式操作（进阶）

---

## 6. 小练习

以下代码输出什么？
```java
int[] a = {3, 1, 4};
int[] b = Arrays.copyOf(a, 3);
Arrays.sort(b);
System.out.println(Arrays.equals(a, b));
```

<details>
<summary>✅ 答案</summary>

输出：**false**

> 💡 原因：`a = {3,1,4}`，`b` 排序后为 `{1,3,4}`，内容不同。
</details>

---





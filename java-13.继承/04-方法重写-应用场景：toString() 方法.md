
---

## 📌 继承-方法重写-应用场景：`toString()` 方法

> **`toString()`** 是 `Object` 类中的一个方法，所有 Java 类都**隐式继承**自 `Object`。  
> 重写 `toString()` 是**最常见、最实用的方法重写场景之一**，用于提供对象的**可读字符串表示**。

---

### ✅ 为什么需要重写 `toString()`？

#### 默认行为（来自 `Object` 类）：
```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```
输出示例：
```
com.example.Student@1b6d3586
```
> ❌ **无意义！无法看出对象内容**

#### 重写后（有意义的输出）：
```java
Student s = new Student("小明", 18);
System.out.println(s); // 输出：Student{name='小明', age=18}
```
> ✅ **清晰、直观、便于调试**

---

### 🔧 如何正确重写 `toString()`？

#### 基本规范（JavaBean 风格）：
- 返回格式：`类名{字段1=值1, 字段2=值2, ...}`
- 包含关键业务字段（非全部）
- 字符串字段用单引号包裹（可选，但推荐）

```java
public class Student {
    private String name;
    private int age;

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

#### 使用 `Objects.toString()`（Java 7+ 推荐）
```java
import java.util.Objects;

@Override
public String toString() {
    return "Student{" +
            "name=" + Objects.toString(name) +
            ", age=" + age +
            '}';
}
```
> ✅ 自动处理 `null`，避免 `NullPointerException`

#### 使用 Lombok（极简写法）
```java
import lombok.ToString;

@ToString
public class Student {
    private String name;
    private int age;
}
// 自动生成标准 toString()
```

---

### 🌐 应用场景

#### 1. **调试与日志**
```java
Student s = new Student("小明", 18);
logger.info("创建学生: {}", s); // 日志中直接输出有意义信息
```

#### 2. **`System.out.println()` / `String.valueOf()`**
```java
System.out.println(s);          // 自动调用 s.toString()
String str = String.valueOf(s); // 同样调用 toString()
```

#### 3. **集合打印**
```java
List<Student> students = Arrays.asList(new Student("A", 20), new Student("B", 21));
System.out.println(students);
// 输出：[Student{name='A', age=20}, Student{name='B', age=21}]
```

#### 4. **框架集成**
- **Spring Boot**：日志、监控、Actuator 端点
- **Jackson/Gson**：虽然序列化用 getter，但调试时 `toString()` 很有用
- **JUnit**：断言失败时显示对象内容

---

### 🔁 重写 `toString()` 的最佳实践

| 建议 | 说明 |
|------|------|
| **始终重写** | 除非是工具类或无状态类 |
| **包含关键字段** | 不必包含所有字段（如密码、大对象） |
| **避免副作用** | `toString()` 不应修改对象状态 |
| **处理 null 安全** | 使用 `Objects.toString()` 或三元判断 |
| **保持简洁** | 不要包含复杂逻辑或循环引用 |

> ⚠️ **不要在 `toString()` 中调用其他可能重写的子类方法**（可能引发未初始化问题）

---

### 🚫 常见错误

| 错误 | 风险 |
|------|------|
| 忘记加 `@Override` | 无法享受编译检查 |
| 返回 `null` | 可能导致 `NullPointerException` |
| 包含敏感信息 | 如密码、密钥（安全风险） |
| 无限递归 | 对象 A 包含 B，B 的 `toString()` 又包含 A |

```java
// 危险示例：循环引用
class Parent {
    Child child;
    @Override public String toString() { return "Parent{child=" + child + "}"; }
}
class Child {
    Parent parent;
    @Override public String toString() { return "Child{parent=" + parent + "}"; }
}
// 调用 parent.toString() → StackOverflowError!
```

> ✅ 解决方案：在一方 `toString()` 中省略对方引用

---

### 🏷️ Obsidian 标签建议
```markdown
#Java #toString #方法重写 #继承 #Object类 #调试 #日志 #Java11 #Lombok
```

---

  ```markdown
  `toString()` 是 [[Object 类的常用方法]] 之一，通过 [[方法的重写]] 提供对象的可读表示，广泛用于 [[调试]] 和 [[日志]]。
  ```

---

### ✅ 总结口诀
> **“Object 有 toString，继承必须重写好；  
> 调试日志离不了，格式清晰最重要；  
> 关键字段列出来，null 安全要记牢；  
> 敏感信息不能露，循环引用要防爆。”**

---


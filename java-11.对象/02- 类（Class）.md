
---

## 📌 类（Class）—— Java 面向对象的核心

### ✅ 定义
> **类（Class）** 是一种**用户自定义的数据类型**，用于**描述具有相同属性和行为的一组对象的模板或蓝图**。

- 类本身**不是具体存在的东西**，它只是一个“设计图”。
- 通过类，我们可以**创建多个对象（实例）**。

> 💡 简单说：  
> **类 = 抽象的模板**，**对象 = 具体的实例**

---

### 🧱 类的组成

一个典型的 Java 类包含以下部分：

| 组成部分 | 说明 | 示例 |
|--------|------|------|
| **字段（Fields）** | 描述对象的状态（属性） | `String name;` `int age;` |
| **方法（Methods）** | 描述对象的行为（能做什么） | `void run() { ... }` |
| **构造方法（Constructor）** | 用于创建对象时初始化数据 | `Student(String name) { ... }` |
| **访问修饰符** | 控制可见性（如 `public`, `private`） | `private int id;` |

---

### 💻 Java 示例

```java
// 定义一个类：Student
public class Student {
    // 字段（状态）
    private String name;
    private int age;

    // 构造方法
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 方法（行为）
    public void study() {
        System.out.println(name + " 正在学习 Java！");
    }

    // Getter 方法（封装的一部分）
    public String getName() {
        return name;
    }
}
```

```java
// 使用类创建对象
public class Main {
    public static void main(String[] args) {
        Student stu1 = new Student("小李", 20); // 对象1
        Student stu2 = new Student("小王", 21); // 对象2

        stu1.study(); // 输出：小李 正在学习 Java！
        stu2.study(); // 输出：小王 正在学习 Java！
    }
}
```

> ✅ `Student` 是**类**，`stu1` 和 `stu2` 是它的**对象（实例）**。

---

### 🔁 类 vs 对象 对比表

| 项目 | 类（Class） | 对象（Object） |
|------|-------------|----------------|
| 性质 | 抽象的模板 | 具体的实例 |
| 是否占用内存 | 否（仅定义） | 是（在堆中分配内存） |
| 创建方式 | 用 `class` 关键字定义 | 用 `new` 关键字实例化 |
| 数量 | 通常一个类只定义一次 | 可创建多个对象 |
| 举例 | “汽车”这个概念 | “我的红色特斯拉” |

---

### 🏷️ Obsidian 标签建议
```markdown
#Java #OOP #类 #Class #面向对象编程 #模板 #蓝图
```

---

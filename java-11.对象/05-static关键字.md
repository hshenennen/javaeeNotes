当然可以！以下是关于 **`static` 关键字** 的系统化学习笔记，涵盖你提出的四个核心要点：

1. `static` 修饰成员变量  
2. `static` 修饰方法  
3. 静态方法的应用场景  
4. `static` 的注意事项  

内容专为 **Java 11+ 初学者** 设计，采用 **Obsidian 友好格式（Markdown）**，便于你保存为知识卡片、建立双向链接，构建清晰的 Java 面向对象知识体系。

---

## 📌 `static` 关键字详解

> **`static`** 表示“静态的”，用于定义**属于类本身**的成员（变量或方法），而非属于某个具体对象。  
> 它在**类加载时初始化**，**内存中只有一份**，可通过**类名直接访问**。

---

### 1️⃣ `static` 修饰成员变量（静态变量 / 类变量）

#### ✅ 定义
```java
public class Student {
    private String name;           // 实例变量（每个对象一份）
    public static int totalCount;  // 静态变量（所有对象共享）
}
```

#### 🔑 特点
| 特性 | 说明 |
|------|------|
| **内存中唯一** | 存储在方法区（Method Area），不是堆中 |
| **类加载时初始化** | 在 `main` 执行前就已存在 |
| **共享性** | 所有对象共用同一份数据 |
| **调用方式** | 推荐：`类名.变量名`（如 `Student.totalCount`）<br>不推荐：`对象.变量名`（编译器会警告） |

#### 💡 应用示例：统计对象数量
```java
public class Student {
    public static int totalCount = 0;

    public Student() {
        totalCount++; // 每创建一个对象，总数+1
    }
}

// 使用
new Student();
new Student();
System.out.println(Student.totalCount); // 输出：2
```

---

### 2️⃣ `static` 修饰方法（静态方法 / 类方法）

#### ✅ 定义
```java
public class MathUtils {
    public static int add(int a, int b) {
        return a + b;
    }
}
```

#### 🔑 特点
| 特性 | 说明 |
|------|------|
| **无需对象即可调用** | `MathUtils.add(1, 2)` |
| **不能访问非静态成员** | ❌ 不能使用 `this`、实例变量、实例方法 |
| **只能访问静态成员** | ✅ 可调用其他 `static` 方法或变量 |
| **不能被重写（Override）** | 子类可定义同名静态方法，但属于“方法隐藏（Hiding）”，不是多态 |

#### ❌ 静态方法中的非法操作
```java
public class Student {
    private String name;

    public static void print() {
        System.out.println(name);     // ❌ 编译错误！
        System.out.println(this.name); // ❌ 编译错误！
    }
}
```

✅ 正确做法：通过参数传入对象
```java
public static void print(Student s) {
    System.out.println(s.name); // ✅ 合法
}
```

---

### 3️⃣ 静态方法的应用场景

| 场景 | 说明 | 示例 |
|------|------|------|
| **工具类方法** | 无状态、纯计算功能 | `Math.sqrt()`, `Arrays.sort()` |
| **工厂方法** | 创建并返回对象 | `LocalDateTime.now()` |
| **单例模式** | 提供全局访问点 | `Singleton.getInstance()` |
| **辅助方法** | 与对象无关的逻辑 | `StringUtils.isEmpty(str)` |
| **main 方法** | JVM 入口（必须 static） | `public static void main(String[] args)` |

> 💡 原则：**如果一个方法不依赖对象状态，就应设计为 `static`**

---

### 4️⃣ `static` 的注意事项（必须掌握！）

#### ⚠️ 1. **不能使用 `this` 和 `super`**
- 因为 `static` 属于类，而 `this/super` 属于对象。

#### ⚠️ 2. **静态方法不能被重写（Override）**
- 子类可以定义同名静态方法，但这叫 **方法隐藏（Method Hiding）**，不是多态。
```java
class Parent {
    public static void show() { System.out.println("Parent"); }
}
class Child extends Parent {
    public static void show() { System.out.println("Child"); }
}
Parent p = new Child();
p.show(); // 输出 "Parent"（静态绑定，看引用类型）
```

#### ⚠️ 3. **静态代码块的执行顺序**
- 静态变量 → 静态代码块 → main 方法
```java
static {
    System.out.println("静态代码块执行");
}
```

#### ⚠️ 4. **内存泄漏风险（慎用静态集合）**
```java
public class Cache {
    public static List<String> list = new ArrayList<>(); // 危险！
}
```
- 静态集合生命周期 = 应用生命周期，容易导致 **内存溢出（OOM）**

#### ⚠️ 5. **线程安全问题**
- 静态变量被所有线程共享，多线程下需加锁（如 `synchronized`）

---

### 🔁 静态 vs 非静态 对比表

| 特性 | 静态成员 | 非静态成员 |
|------|--------|----------|
| 所属 | 类 | 对象 |
| 内存分配 | 类加载时（方法区） | 对象创建时（堆） |
| 调用方式 | `类名.成员` | `对象.成员` |
| 是否共享 | 是 | 否 |
| 能否访问对方 | 静态 ❌ 访问非静态<br>非静态 ✅ 访问静态 | |

---

### 🏷️ Obsidian 标签建议
```markdown
#Java #static #静态变量 #静态方法 #类成员 #内存模型 #面向对象 #Java11
```


---

  ```markdown
  静态方法不能使用 [[this 关键字]]，因为它不依赖于任何对象。
  ```

---

✅ **总结口诀**：  
> **“静态属于类，共享一份值；  
> 无对象可调，不能用 this；  
> 工具常静态，封装慎用之。”**


---

## 📌 JavaBean 规范

### ✅ 什么是 JavaBean？
> **JavaBean** 是一种符合特定编码规范的 **Java 类**，主要用于：
> - 封装数据（如表单数据、数据库记录）
> - 被框架（如 Spring、Hibernate、JSP）自动识别和操作
> - 支持可视化开发工具（早期用于 GUI 组件）

它本质上是一个**可重用、可配置、可序列化的组件**。

---

### 📏 JavaBean 的核心规范（必须满足）

一个类要成为标准的 JavaBean，需满足以下 **5 条规则**：

| 要求 | 说明 | 示例 |
|------|------|------|
| **1. 公共类（public class）** | 类必须是 `public` 的 | `public class User { ... }` |
| **2. 提供无参公共构造方法** | 必须有 `public` 无参构造器（即使你写了有参构造） | `public User() {}` |
| **3. 属性私有化（private fields）** | 所有属性必须是 `private` | `private String name;` |
| **4. 提供 public 的 getter/setter 方法** | 每个属性需有标准命名的访问方法 | `getName()`, `setName(...)` |
| **5. 实现 `java.io.Serializable` 接口（推荐）** | 便于网络传输或持久化（非强制但强烈建议） | `implements Serializable` |

> 💡 这些规则使得框架能通过 **反射（Reflection）** 自动创建对象、读写属性。

---

### 💻 标准 JavaBean 示例

```java
import java.io.Serializable;

// 1. 公共类
public class Student implements Serializable { // 5. 推荐实现 Serializable
    private static final long serialVersionUID = 1L;

    // 3. 私有属性
    private String name;
    private int age;

    // 2. 无参公共构造方法（必须！）
    public Student() {}

    // 4. Getter 和 Setter（命名必须规范）
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

✅ 此类可被 Spring、MyBatis、Jackson（JSON 序列化）等框架无缝使用。

---

### 🔍 命名规范细节（getter/setter）

| 属性名               | Getter                       | Setter                      |
| ----------------- | ---------------------------- | --------------------------- |
| `name`            | `getName()`                  | `setName(String name)`      |
| `email`           | `getEmail()`                 | `setEmail(String email)`    |
| `active`（boolean） | `isActive()` 或 `getActive()` | `setActive(boolean active)` |

> ⚠️ 注意：  
> - boolean 属性的 getter **推荐用 `isXxx()`**（如 `isActive()`）  
> - 框架通常优先识别 `isXxx()`，其次才是 `getXxx()`

---

### ✅ JavaBean 的用途

| 场景 | 说明 |
|------|------|
| **Web 开发（Spring MVC）** | 表单数据自动绑定到 JavaBean 对象 |
| **ORM 框架（如 MyBatis、Hibernate）** | 数据库记录映射为 JavaBean 实例 |
| **JSON/XML 序列化** | Jackson、Gson 等库依赖 getter/setter 转换数据 |
| **配置类（Spring Boot）** | `@ConfigurationProperties` 绑定配置到 JavaBean |

示例（Spring Boot）：
```properties
# application.properties
student.name=小明
student.age=18
```

```java
@Component
@ConfigurationProperties(prefix = "student")
public class Student implements Serializable {
    private String name;
    private int age;
    // getter/setter...
}
// Spring 自动将配置注入到 Student 对象中
```

---

### ⚠️ 常见误区

| 误区 | 正确做法 |
|------|--------|
| “只要有 getter/setter 就是 JavaBean” | ❌ 还必须有 **无参构造方法**！ |
| “可以没有无参构造” | ❌ 框架通过 `new Class()` 创建对象，没有会报错 |
| “属性可以是 public” | ❌ 必须 `private`，否则破坏封装，框架可能无法识别 |

---

### 🏷️ Obsidian 标签建议
```markdown
#Java #JavaBean #封装 #Serializable #框架集成 #面向对象 #数据模型
```

---


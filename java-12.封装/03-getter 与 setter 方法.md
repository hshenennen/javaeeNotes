
---

## 📌 封装：getter 与 setter 方法

> **封装（Encapsulation）** 是面向对象编程（OOP）的核心原则之一，而 **getter 和 setter 方法** 是实现封装的关键手段。  
> 它们允许你**控制对私有字段的访问**，在保证数据安全的同时提供灵活的接口。

---

### ✅ 为什么需要 getter/setter？

#### ❌ 直接暴露字段的问题
```java
class Student {
    public String name; // 公共字段
    public int age;
}

Student s = new Student();
s.age = -5; // ❌ 无法阻止非法值！
```

#### ✅ 使用 getter/setter 的优势
- **数据校验**：在 `setter` 中验证输入合法性  
- **隐藏实现**：外部不关心内部如何存储  
- **灵活性**：未来可修改逻辑而不影响调用方  
- **兼容框架**：Spring、Hibernate、JSON 库依赖标准 getter/setter

---

### 🔧 标准写法（JavaBean 规范）

#### 1. 字段私有化（`private`）
```java
private String name;
private int age;
```

#### 2. 提供 public 的 getter/setter
```java
// Getter：获取值
public String getName() {
    return name;
}

// Setter：设置值（可加入校验）
public void setName(String name) {
    if (name != null && !name.trim().isEmpty()) {
        this.name = name;
    } else {
        throw new IllegalArgumentException("姓名不能为空");
    }
}

public int getAge() {
    return age;
}

public void setAge(int age) {
    if (age >= 0 && age <= 150) {
        this.age = age;
    } else {
        throw new IllegalArgumentException("年龄必须在 0~150 之间");
    }
}
```

> 💡 命名规则（JavaBean 规范）：
> - `getXxx()` / `setXxx()`（字段 `xxx` 首字母大写）
> - boolean 字段推荐 `isXxx()`（如 `isActive()`）

---

### 🧪 使用示例

```java
Student s = new Student();
s.setName("小明");   // ✅ 合法
s.setAge(18);        // ✅ 合法

// s.setAge(-5);     // ❌ 抛出异常，防止非法数据

System.out.println(s.getName()); // 输出：小明
```

---

### 🛠️ 开发技巧：自动生成 getter/setter

#### 1. **IDE 快捷键**
- **IntelliJ IDEA**：`Alt + Insert` → 选择 `Getter and Setter`
- **Eclipse**：`Source` → `Generate Getters and Setters...`

#### 2. **使用 Lombok（推荐）**
```java
import lombok.Data;

@Data // 自动生成 getter、setter、toString、equals、hashCode
public class Student {
    private String name;
    private int age;
}
```
> ✅ 极大减少样板代码，保持简洁

---

### ⚠️ 常见误区与注意事项

| 误区 | 正确做法 |
|------|--------|
| “getter/setter 就是简单返回/赋值，没必要” | ❌ 忽略了未来扩展性和数据安全 |
| 在 setter 中不做任何校验 | ⚠️ 至少应做基本非空/范围检查 |
| 将 getter/setter 设为 `private` | ❌ 外部无法访问，失去封装意义 |
| boolean 字段用 `getActive()` 而非 `isActive()` | ⚠️ 某些框架（如 Jackson）优先识别 `isXxx()` |

---

### 🔁 getter/setter 与封装的关系

| 概念 | 说明 |
|------|------|
| **封装** | 思想：隐藏内部细节，暴露可控接口 |
| **getter/setter** | 实现手段：提供受控的读写通道 |
| **private 字段** | 基础：确保外部不能直接访问 |

> 🔄 三者缺一不可：  
> `private 字段 + public getter/setter = 完整封装`

---

### 🌐 框架依赖示例

#### Spring Boot（配置绑定）
```java
@ConfigurationProperties(prefix = "app.user")
@Data
public class UserConfig {
    private String name;
    private int maxAttempts;
}
```
```properties
# application.properties
app.user.name=Admin
app.user.max-attempts=3
```
> Spring 通过 `setName()` 和 `setMaxAttempts()` 自动注入值

#### JSON 序列化（Jackson）
```java
ObjectMapper mapper = new ObjectMapper();
String json = mapper.writeValueAsString(student); // 调用 getName(), getAge()
Student s = mapper.readValue(json, Student.class); // 调用 setName(), setAge()
```

---

### 🏷️ Obsidian 标签建议
```markdown
#Java #封装 #getter #setter #JavaBean #面向对象 #数据校验 #访问控制
```


---

### ✅ 总结口诀
> **“字段私有化，访问靠方法；  
> getter 读数据，setter 做校验；  
> 封装保安全，框架都依赖。”**

---


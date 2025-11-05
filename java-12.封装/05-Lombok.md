
---

## 📌 使用 Lombok（进阶）：`@Data` 自动生成 getter/setter/toString

### ✅ 什么是 Lombok？
> **Lombok** 是一个 Java 编译期注解库，通过注解**自动生成样板代码**（如 getter、setter、构造方法、toString 等），大幅减少重复代码，提升开发效率。

- 它在 **编译时** 自动生成代码（运行时无性能损耗）
- IDE 需安装 Lombok 插件才能正确识别（IntelliJ / Eclipse 均支持）

---

### 🚀 核心优势

| 传统写法                   | 使用 Lombok     |
| ---------------------- | ------------- |
| 手动写 10 行 getter/setter | 一行 `@Data` 注解 |
| 修改字段后需同步更新方法           | 自动同步，无需维护     |
| 容易出错、冗长                | 简洁、安全、可读性强    |

---

## 🔧 如何使用 Lombok？

### 步骤 1：添加依赖（Maven）

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.34</version> <!-- 兼容 Java 11+ -->
    <scope>provided</scope>
</dependency>
```

> 💡 Lombok 在编译期生效，运行时不需要，所以用 `provided`

### 步骤 2：安装 IDE 插件
- **IntelliJ IDEA**：  
  `Settings → Plugins → 搜索 "Lombok" → 安装并重启`
- **Eclipse**：  
  下载 `lombok.jar` 并运行：`java -jar lombok.jar` → 指定 IDE 路径

### 步骤 3：编写代码（使用 `@Data`）

```java
import lombok.Data;

@Data // ← 一行注解，替代 getter/setter/toString/equals/hashCode
public class Student {
    private String name;
    private int age;
}
```

✅ 编译后，Lombok 会自动生成等价于以下代码：

```java
public class Student {
    private String name;
    private int age;

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }

    @Override
    public String toString() {
        return "Student(name=" + name + ", age=" + age + ")";
    }

    @Override
    public boolean equals(Object o) { /* 自动生成 */ }
    @Override
    public int hashCode() { /* 自动生成 */ }
}
```

---

## 🎯 `@Data` 注解包含哪些功能？

`@Data` 是一个**组合注解**，等价于以下注解的集合：

| 注解 | 功能 |
|------|------|
| `@Getter` | 为所有字段生成 getter |
| `@Setter` | 为所有字段生成 setter |
| `@ToString` | 生成 `toString()` 方法 |
| `@EqualsAndHashCode` | 生成 `equals()` 和 `hashCode()` |
| `@RequiredArgsConstructor` | 为 `final` 或 `@NonNull` 字段生成构造方法 |

> ⚠️ 注意：`@Data` **不会生成无参构造方法**！  
> 如果你需要无参构造（如用于 JavaBean 或框架），需额外添加 `@NoArgsConstructor`

---

### ✅ 完整 JavaBean 示例（兼容框架）

```java
import lombok.Data;
import lombok.NoArgsConstructor;
import java.io.Serializable;

@Data
@NoArgsConstructor // ← 显式添加无参构造（满足 JavaBean 规范）
public class Student implements Serializable {
    private static final long serialVersionUID = 1L;

    private String name;
    private int age;
}
```

> ✅ 此类：
> - 有无参构造（`@NoArgsConstructor`）
> - 有 getter/setter/toString（`@Data`）
> - 可序列化（`Serializable`）
> - 完全符合 **JavaBean 规范**

---

## 🔍 其他常用 Lombok 注解（扩展）

| 注解 | 用途 |
|------|------|
| `@AllArgsConstructor` | 生成包含所有字段的构造方法 |
| `@RequiredArgsConstructor` | 为 `final` 或 `@NonNull` 字段生成构造方法 |
| `@Builder` | 启用建造者模式（`Student.builder().name("小明").build()`） |
| `@Slf4j` | 自动生成日志对象：`log.info("...")` |

示例：建造者模式
```java
@Data
@Builder
public class Student {
    private String name;
    private int age;
}

// 使用
Student s = Student.builder()
    .name("小明")
    .age(18)
    .build();
```

---

## ⚠️ 注意事项

| 问题 | 解决方案 |
|------|--------|
| IDE 报错“找不到 getter/setter” | 安装 Lombok 插件并启用 Annotation Processing |
| 框架（如 Spring）无法反序列化 | 确保有无参构造（加 `@NoArgsConstructor`） |
| 不想为某个字段生成 setter | 使用 `@Setter(AccessLevel.NONE)` |
| `equals/hashCode` 性能问题 | 对大对象谨慎使用 `@Data`，可改用 `@Getter + @Setter` |

---

## 🏷️ Obsidian 标签建议
```markdown
#Java #Lombok #JavaBean #封装 #代码简化 #开发效率 #@Data
```


---


  ```markdown
  Lombok 的 `@Data` 是 [[JavaBean 规范]] 的高效实现方式。
  ```

---

✅ **小结**：  
Lombok 不是魔法，而是**编译期代码生成工具**。它让你专注于业务逻辑，而不是样板代码。在现代 Java 开发（尤其是 Spring Boot 项目）中，Lombok 已成为事实标准。

> 🚀 **动手试试**：  
> 用 `@Data + @NoArgsConstructor` 重写你之前的 `Student` 类，体验代码量的大幅减少！


---

## 📌 `super` 关键字

> **`super`** 是 Java 中用于**在子类中访问父类成员**的关键字。  
> 它是实现**继承复用**与**方法扩展**的重要工具，常见于构造方法和重写方法中。

> 🔑 核心作用：**“显式调用父类的东西”**

---

### ✅ 三大用途

#### 1️⃣ 调用父类的构造方法（`super(...)`）

- **必须出现在子类构造方法的第一行**
- 若未显式调用，编译器自动插入 `super()`（调用父类无参构造）

```java
class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name); // ← 调用父类构造方法
        // this.name = name; // 不需要，父类已初始化
    }
}
```

> ⚠️ 如果父类**没有无参构造**，子类**必须显式调用** `super(...)`，否则编译报错！

---

#### 2️⃣ 访问父类的成员变量（`super.field`）

当子类与父类**字段同名**时，用 `super` 区分：

```java
class Animal {
    protected String name = "动物";
}

class Dog extends Animal {
    private String name = "狗"; // 隐藏父类字段（Field Hiding）

    public void printNames() {
        System.out.println("子类 name: " + this.name);   // 输出：狗
        System.out.println("父类 name: " + super.name);  // 输出：动物
    }
}
```

> 💡 字段隐藏（Hiding） ≠ 方法重写（Overriding）  
> 字段访问在**编译期**决定（看引用类型），而方法调用在**运行期**（多态）。

---

#### 3️⃣ 调用父类的成员方法（`super.method()`）

在**重写方法中**，调用父类原始实现，实现“**扩展而非替换**”：

```java
class Animal {
    public void speak() {
        System.out.println("动物发声");
    }
}

class Dog extends Animal {
    @Override
    public void speak() {
        super.speak();        // 先执行父类逻辑
        System.out.println("汪汪！"); // 再添加子类行为
    }
}

// 调用结果：
// 动物发声
// 汪汪！
```

> ✅ 典型场景：日志记录、权限校验、基础逻辑复用

---

### 🔁 `super` vs `this` 对比表

| 特性 | `this` | `super` |
|------|--------|--------|
| **指向对象** | 当前子类对象 | 父类部分（隐式存在于子类对象中） |
| **调用构造** | `this(...)`：调用本类其他构造 | `super(...)`：调用父类构造 |
| **访问字段** | `this.field`：当前类字段 | `super.field`：父类字段 |
| **调用方法** | `this.method()`：当前类方法 | `super.method()`：父类方法 |
| **使用位置** | 构造方法、实例方法 | 构造方法、实例方法 |
| **第一行限制** | `this(...)` 必须是构造第一行 | `super(...)` 必须是构造第一行 |

> ⚠️ **`this()` 和 `super()` 不能共存**于同一个构造方法！

---

### ⚠️ 常见误区与注意事项

| 误区 | 正确理解 |
|------|--------|
| “`super` 是一个对象引用” | ❌ `super` 不是对象，只是**访问父类成员的语法工具** |
| “`super` 可以在静态方法中使用” | ❌ 静态上下文无 `this`/`super`（属于类，不属于对象） |
| “`super` 能访问父类 `private` 成员” | ❌ 不能！`private` 对子类不可见，即使使用 `super` |
| “`super()` 可以放在构造方法任意位置” | ❌ 必须是**第一条语句** |

---

### 💡 实际应用场景

#### 场景 1：模板方法模式（Template Method）
```java
abstract class Beverage {
    public final void prepare() {
        boilWater();
        brew();
        pourInCup();
        if (wantsCondiments()) addCondiments();
    }
    protected abstract void brew();
    protected void addCondiments() { } // 默认空实现
}

class Coffee extends Beverage {
    @Override
    protected void brew() {
        System.out.println("冲泡咖啡");
    }

    @Override
    protected void addCondiments() {
        super.addCondiments(); // 调用父类（虽为空，但体现扩展意图）
        System.out.println("加糖和牛奶");
    }
}
```

#### 场景 2：安全地扩展父类行为
```java
class SecureService {
    public void process() {
        validateUser(); // 父类做基础校验
        doProcess();
    }
    protected void doProcess() { }
}

class OrderService extends SecureService {
    @Override
    protected void doProcess() {
        // 无需重复校验，直接专注业务
        System.out.println("处理订单");
    }
}
```

---

### 🏷️ Obsidian 标签建议
```markdown
#Java #super #继承 #面向对象 #构造方法 #方法重写 #Java11 #OOP
```

---


  ```markdown
  `super` 是 [[继承]] 机制的核心工具，常与 [[this 关键字]] 对比使用，用于在子类中调用 [[父类]] 的构造方法或被 [[方法的重写]] 覆盖的原始实现。
  ```

---

### ✅ 总结口诀
> **“super 三大用：构造调父类，字段分父子，方法扩行为；  
> 构造第一行，静态不能用；  
> 不是真实对象，只是访问通道。”**

---


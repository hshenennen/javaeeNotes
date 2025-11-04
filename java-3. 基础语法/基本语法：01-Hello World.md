我们创建了一个名为 `Main.java` 的 Java 文件，并使用以下代码将 "Hello World" 打印到屏幕上：


#### Main.java
```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```

下面将逐步介绍如何保存、编译以及运行这个程序：
 - 打开代码编辑器，把上面的代码添加进去；
- 把文件名保存为：HelloWorld.java；
- 打开 cmd 命令窗口，进入目标文件所在的位置，假设是 C:\
- 在命令行窗口输入 javac HelloWorld.java 按下回车键编译代码。如果代码没有错误，cmd 命令提示符会进入下一行（假设环境变量都设置好了）。
- 再键输入 java HelloWorld 按下回车键就可以运行程序了
你将会在窗口看到 Hello World
```
$ javac HelloWorld.java
$ java HelloWorld 
   Hello World
```

如果遇到编码问题，我们可以使用 -encoding 选项设置 **utf-8** 来编译：
```
javac -encoding UTF-8 HelloWorld.java 
java HelloWorld
```

---
### 例子解释

在 Java 中运行的每一行代码都必须位于一个 **`class`** 中。在我们的例子中，我们将类命名为 _Main_。类名应该大写首字母。

==注意==：Java 区分大小写："MyClass" 与 "myclass" 有不同的含义。

Java 文件名_必须匹配_类名。请使用类名保存文件并添加扩展名 ".java"。

---

## main 方法

```java
public static void main(String[] args)

```


main( )  方法中的任何代码都会被执行。现在，您还不必理解 main 前后的关键字。随着学习的深入，您将一点一点地了解它们。

现在，请记住每个 Java 程序都有一个必须与文件名匹配的 `class` 名，并且每个程序都必须包含 `main()` 方法

#### System.out.println()
在 `main()` 方法内部，我们可以使用 `println()` 方法将一行文本打印到屏幕上：

```java
public static void main(String[] args) {
  System.out.println("Hello World");
}
```


---

> [!注意]
> 注意：花括号 `{}` 标记了一段代码的开始和结束。
> 
> `System` 是一个内置的 Java 类，它包含了一些有用的成员，比如 `out`，它是 "output"（输出）的缩写。`println()` 方法是 "print line"（打印行）的缩写，用于将值打印到屏幕上（或文件中）。
> 
> 不用太担心 `System`、`out` 和 `println()` 是如何工作的。只需要知道您需要将它们一起使用来在屏幕上打印内容。
> 
> 您还应注意，每条代码语句都必须以分号 (`;`) 结尾
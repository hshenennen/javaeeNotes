---
tags: [Java, 环境配置, Windows]
---

# Windows 系统安装 Java  

## 1. 下载 JDK  
首先我们需要下载 JDK。下载地址：<https://www.oracle.com/java/technologies/downloads/>。在下载页面中根据自己的系统选择对应的版本。本文以 Windows 64 位系统为例。 
![[jdk-download 1.png]]
安装 JDK 时也会一并安装 JRE。安装过程中可以自定义安装目录，例如：  
`C:\Program Files (x86)\Java\jdk1.8.0_91`

## 2. 配置环境变量  
1. 安装完成后，右击 “我的电脑” → “属性” → “高级系统设置”。  
2. ![[win-java1.png]]
3. 点击 “高级” → “环境变量”。 
. ![[java-win2.png]]
4. 在 “系统变量” 中设置三项变量：`JAVA_HOME`、`PATH`、`CLASSPATH`。若已存在则编辑，否则新建。 

![[java-win3.png]]
> 注意：如果使用 JDK 1.5 以上版本，不必须设置 CLASSPATH，也可正常编译运行 Java 程序。 :contentReference[oaicite:5]{index=5}  

### 2.1 JAVA_HOME  
- 变量名：`JAVA_HOME`  
- 变量值：你的 JDK 安装目录（如 `C:\Program Files (x86)\Java\jdk1.8.0_91`）  
              ![[java-win5 1.png]]  
### 2.2 PATH  
- 变量名：`Path`（或 `PATH`）  
- 变量值：`%JAVA_HOME%\bin; %JAVA_HOME%\jre\bin;`  

> 在 Windows 10 中，Path 变量里的项是分条显示的，建议分条添加：  
> - `%JAVA_HOME%\bin;`  
> - `%JAVA_HOME%\jre\bin;` 

    
  ![[java-win7 1.png]]
       ![[44A70696-B2E6-4055-B88F-7FC0222DCCA4.png]]
## 3. 测试 JDK 是否安装成功  
1. “开始” → “运行” → 输入 `cmd`。  
2. 输入命令：  
   ```bash
   java -version  
   javac  
   ```

   ---
   ## 返回目录 -[[Java-开发环境配置]]
   
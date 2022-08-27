# Could not find com.android.tools.build:gradle:3.0.1


在此介绍一种**简单、粗暴、有效**的解决办法。
### 
### **第一步**
打开**项目的build.gradle**。再次强调：是项目的build.gradle而不是Module的build.gradle
### 
### **第二步**
在build.gradle文件中的buildscript的repositories添加google( )，代码如下：


```
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.3'
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

```
### 
### **第三步**
在build.gradle文件中的allprojects的repositories添加google( )，代码如下：


```
allprojects {
    repositories {
        google()
        jcenter()
    }
}

```
### 
### **第四步**


更新，OK，收工。

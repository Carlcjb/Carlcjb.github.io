---
layout: post
title: 异常lambda expressions are not supported at this language level处理
date: 2017-6-10
tags: android  
---

### 解决方案
在模块工程build.gradle中添加
```
compileOptions {  
    sourceCompatibility JavaVersion.VERSION_1_7  
    targetCompatibility JavaVersion.VERSION_1_7  
}
```

```
apply plugin: 'me.tatarka.retrolambda'

```

在根目录工程build.gradle里添加
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.0'
    classpath 'me.tatarka:gradle-retrolambda:3.2.0'
    // NOTE: Do not place your application dependencies here; they belong
    // in the individual module build.gradle files
}

```

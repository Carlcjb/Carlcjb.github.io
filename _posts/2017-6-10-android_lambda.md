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

### Android Studio --“Cannot resolve symbol” 解决办法
Android Studio 无法识别同一个 package 里的其他类，将其显示为红色，但是 compile 没有问题。鼠标放上去后显示 “Cannot resolve symbol XXX”，重启 android Studio，重新 sync gradle，Clean build 都没有用。
多半是因为 Android Studio 之前发生了错误，某些 setting 出了问题。解决方法如下：
点击菜单中的 “File” -> “Invalidate Caches / Restart”，然后点击对话框中的 “Invalidate and Restart”，清空 cache 并且重启。语法就会正确的高亮了

### 图片压缩工具 pngquant
50-80 有点过 50-50感觉差不多
```
echo "开始处理..."

for /R %%i in (*.png) do (
  pngquant -f --ext .png --quality 50-80 "%%i"
)

pause
```

```
import os,sys
import os.path
rootdir=sys.path[0]

#需要过滤的文件
notActionFile = ["choose_bg1.png"]
#需要过滤的文件夹
notActionPath = ["test"]

#需要删除的文件
needDeleteFile = ["s2.png"]


def file_extension(path):
  return os.path.splitext(path)[1]




for parent,dirnames,filenames in os.walk(rootdir):
    for filename in filenames:
        fullPath = os.path.join(parent,filename)
        #删除文件
        for deleteFile in needDeleteFile:
           if  filename == deleteFile: 		
              os.remove(fullPath)			  
        isFilter = False
        #过滤文件压缩
        for noActionName in notActionFile:
          if noActionName == filename:
              isFilter = True
        #过滤文件夹压缩			  
        for onePath in notActionPath:
          lastPath = fullPath.split('\\')[-2]
          if lastPath == onePath:
              isFilter = True              		   
        if file_extension(fullPath) == ".png" and isFilter == False:
          #print "action"		
          os.system("pngquant -f --ext .png --quality 50-80 \"" + fullPath  + "\"")
          print fullPath

```

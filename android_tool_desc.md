---
title: Android开发工具链
tags: Android,开发工具,工具链
grammar_cjkRuby: true
---
## Android Studio
### 快捷键
## 插件
### generator findViewById

### GsonFormat
https://github.com/zzz40500/GsonFormat/blob/master/README_CN.md[](https://github.com/zzz40500/GsonFormat/blob/master/README_CN.md)


 
 ## 开源框架
 ### glide
 
 ### 

## 测试
### Monkey

	adb shell monkey -p com.glodon.glm.pad -s 200 --throttle 300   -v -v -v 1000
 
 

``` stylus
1.-help   查看monkey的帮助信息
例：adb shell monkey -help
2.-p   指定被测应用的包名 
  例：adb shell monkey -p com.UCMobile.x86 100
  如果想要指定多个包名，每一个包名要跟一个-p
  例：adb shell monkey -p packageName1 -p packageName2 100

3.  COUNT  设置执行的次数
  例：adb shell monkey 100

4.-s 设置种子数（相当于设置一个路径，因为monkey是
  随机事件，所以为了使回归路径一致就需要设置相同的seed值）
  例：adb shell monkey 100 -s 5
  如果想重现上面例子的路径下次执行的-s也必须为5

5.--throttle 设置每次随机事件的时间间隔(单位：毫秒)
  例：adb shell monkey 100 --throttle 500

6.--throttle time --randomize-throttle 设置随机时间的时间间隔区间
  例：adb shell monkey 100 --throttle 500 --randomize-throttle 
  说明：执行一百次monkey随机事件，每次事件的间隔在0到500毫秒之间不固定

7.-v 设置日志级别最多(默认一个-v)
  例：adb shell monkey -v 100
  如需更详细的日志可以加多个-v,最多3个
  例：adb shell monkey -v -v -v 100

8.--ignore-crashes   运行中忽略crash，遇到crash依然把后面的事件跑完
  例：adb shell monkey --ignore-crashes -v 100

9.--ignore-timeouts  运行中忽略ANR,遇到ANR依然把后面的事件跑完
例：adb shell monkey --ignore-timeouts -v 100

10.设置事件百分比,所有的百分比加起来不能超过100%
    0：触摸事件百分比，即参数--pct-touch
    1：滑动事件百分比，即参数--pct-motion
    2：缩放事件百分比，即参数--pct-pinchzoom
    3：轨迹球事件百分比，即参数--pct-trackball
    4：屏幕旋转事件百分比，即参数--pct-rotation
    5：基本导航事件百分比，即参数--pct-nav
    6：主要导航事件百分比，即参数--pct-majornav
    7：系统事件百分比，即参数--pct-syskeys
    8：Activity启动事件百分比，即参数--pct-appswitch
    9：键盘翻转事件百分比，即参数--pct-flip
    10：其他事件百分比，即参数--pct-anyevent
  例：adb shell monkey --pct-touch 20 -v 100

11.--ignore-native-crashes   忽略monkey本身的异常，直到事件执行完毕
  例：adb shell monkey --ignore-native-crashes -v 100
monkey日志分析

1.Monkey: seed=1470511671524 count=100
monkey执行的seed值和随机事件次数

2.AllowPackage: com.UCMobile.x86
  可以运行的包名

3.// Event percentages:
  //   0: 15.0%
  //   1: 10.0%
  //   2: 2.0%
  //   3: 15.0%
  //   4: -0.0%
  //   5: -0.0%
  //   6: 25.0%
  //   7: 15.0%
  //   8: 2.0%
  //   9: 2.0%
  //   10: 1.0%
  //   11: 13.0%
  分配事件的百分比，事件号可以参考第二部分

4.事件0：触摸事件
    Sending Touch (ACTION_DOWN): 0:(572.0,1105.0)
    Sending Touch (ACTION_UP): 0:(576.20734,1105.024)

5. 事件1：滑动事件
  Sending Touch (ACTION_DOWN): 0:(233.0,761.0)
  Sending Touch (ACTION_MOVE): 0:(208.49568,736.34766)
  Sending Touch (ACTION_MOVE): 0:(202.7063,729.8338)
  Sending Touch (ACTION_MOVE): 0:(183.89723,722.677)
  Sending Touch (ACTION_UP): 0:(174.83568,721.8229)

6.事件2：缩放事件
  Sending Touch (ACTION_DOWN): 0:(107.0,242.0)
  Sending Touch (ACTION_POINTER_DOWN 1): 0:(108.14705,248.53061) 1:(270.0,262.0)
  Sending Touch (ACTION_MOVE): 0:(110.117355,252.96329) 1:(267.9937,262.25485)
  Sending Touch (ACTION_MOVE): 0:(111.30056,261.88846) 1:(261.90106,262.58475)
  Sending Touch (ACTION_MOVE): 0:(113.11743,265.60138) 1:(253.92662,263.13382)
  Sending Touch (ACTION_POINTER_UP 1): 0:(113.29031,267.4419) 1:(248.60628,263.23257)

7.事件3：轨迹球事件
  Sending Trackball (ACTION_MOVE): 0:(3.0,-2.0)
  Sending Trackball (ACTION_MOVE): 0:(1.0,-1.0)

8.事件4：屏幕旋转事件（隐藏事件）
  Sending rotation degree=0,persist=true

9.事件5：导航事件（上下左右）
   Sending Key (ACTION_DOWN): 21    // KEYCODE_DPAD_LEF

10.事件6：主要导航事件（menu等）
  Sending Key (ACTION_DOWN): 23    // KEYCODE_DPAD_CENTER

11.事件7：系统按键事件(音量，home,返回按键等)
  Sending Key (ACTION_UP): 25    // KEYCODE_VOLUME_DOWN

12.事件8：启动应用事件
  Switch: #Intent;action=android.intent.action.MAIN;category=android.intent.category.LAUNCHER;launchFlags=0x10200000;component=com.UCMobile.x86/com.UCMobile.main.UCMobile;end

13.事件9：键盘事件（隐藏显示键盘）
  Sending Flip keyboardOpen=true

14.事件10：其他按键
  Sending Key (ACTION_DOWN): 66    // KEYCODE_ENTER
  Sending Key (ACTION_UP): 66    // KEYCODE_ENTER

15.延时
  Sleeping for 300 milliseconds
```


 ### espresso
 #### 常规运行AndroidTest命令
 
 
 	./gradlew test
    ./gradlew connectedAndroidTest
 	./gradlew cAT
  
  参考地址：
  [https://developer.android.com/studio/test/command-line](https://developer.android.com/studio/test/command-line)
 
#### AndroidTest测试运行
``` stylus
/**
 * 1)安装apk包
 * 2）安装测试AndroidTest.apk
 * 3)运行如下命令
 * adb shell am instrument -w -r   -e debug false  com.XXXX/android.support.test.runner.AndroidJUnitRunner
 * */

C:\Program Files\Android\Android Studio\jre
```


 
 
欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过==设置==里的修改模板来改变新建文章的内容。
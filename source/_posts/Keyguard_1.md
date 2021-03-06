---
title: Android Keyguard(二) lock & unlock流程  
date: 2017-12-28 16:25:34
tags: [android, keyguard]
description: 通过上一篇我们了解到Keyguard会伴随着SystemUI的启动而启动，其中最重要的一个文件就是KeyguardViewMediator,这个文件负责SystemUI与Keyguard的交互，我们来看一下keyguard的整个流程。
---
源码分析来自于 http://androidxref.com/8.0.0_r4/
## show keyguard流程
show keyguard有两个触发点，一个是systemReady,意思是系统启动完成以后show keyguard。另一个是screenOff，表示灭屏，手机要灭屏进入休眠状态有两个原因：手动按Power键灭屏（WindowManagerPolicy.OFF_BECAUSE_OF_USER）和 系统自动灭屏（WindowManagerPolicy.OFF_BECAUSE_OF_TIMEOUT）。
### systemReady加锁
在完成系统启动以后，WindowManagerServices成功拉起SystemUI以后，SystemUI也能正常拉起KeyguardViewMediator，执行到onSystemReady中，并通过该方法将Lock show出。
![Keyguard](Keyguard_1/keyguard_1.png)
![Keyguard](Keyguard_1/keyguard_2.png)
而showLocked()方法中通过发消息的方式将Keyguardshow出来。并在此时acquire亮屏锁，该锁为申请CPU调度时，保证单一性。
![Keyguard](Keyguard_1/keyguard_3.png)
在处理show消息的case中，开始执行锁屏的展示动作，包含动画等操作，同样会执行SystemUI对Statubar的变化，Window type的变更。同时开始使用userActivity()来执行即时亮屏等操作。
### sreenOff加锁


## SystemUI的启动
![Keyguard](Keyguard_1/keyguard_systemUI_7.0.png)
![Keyguard](Keyguard_1/keyguard_systemUI_8.0.png)
在android8.0版本中,去掉了ServiceMonitor,在systemBars.start()中直接掉起createStatusBarFromConfig();去new StatusBar.java, 这里和7.0不一样的是去掉了BaseStatusBar.
## POWER键灭屏时Keyguard的加载
![Keyguard](Keyguard_1/keyguard_power.png)
## 解锁
每个用户隔一段时间重新开始使用手机时，首先按电源键点亮屏幕，紧接着解锁。android.intent.action.USER_PRESENT就是解锁时发出的intent.
于是,监听android.intent.action.USER_PRESENT就能识别用户进入home界面，进而启动想启动的相关服务,包括弹出对话框welcome用户\后台启动程序升级服务等等。
ACTION_USER_PRESENT 文档说明.
```
public static final String ACTION_USER_PRESENT
Since: API Level 3
Broadcast Action: Sent when the user is present after device wakes up (e.g when the keyguard is gone).
This is a protected intent that can only be sent by the system.
Constant Value: "android.intent.action.USER_PRESENT"
```
翻译过来就是:
注意这个action只能有系统发出，是在用户唤醒机器的时候才会发出这种action.
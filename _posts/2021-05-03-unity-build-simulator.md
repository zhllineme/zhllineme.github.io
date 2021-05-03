---
layout:     post
title:      "xlua框架unity生成ios模拟器版本"
subtitle:   ""
date:       2021-05-03 17:59:00 +0800
author:     "雨冻住了"
catalog: false
header-style: text
tags:
  - unity
  - xlua
  - ios
---

> 转载请注明出处： https://zhllineme.github.io/2021-05-03-unity-build-simulator

项目为unity2019 xlua框架，由于facebook申请权限需要提交模拟器版本安装包，android包是可以在模拟器安装的，ios包的话要做些修改，经过一番折腾，以下为主要要点：

[facebook ios要求](https://developers.facebook.com/docs/ios/getting-started/advanced#sim_build)



1. xlua编译库要编译模拟器版本。

    

2. targetsdk选择模拟器sdk，关闭metal（2019模拟器不支持metal）。路径： Edit -> Project Settings -> Player -> ios平台

![unity ios build 设置](/img/2021/unity_simulator_build.png)



3. 打完包导出xcode工程后，修改MetalHelper.mm文件，

    ```objective-c
    [UnityCurrentMTLCommandBuffer() presentDrawable: surface->drawable afterMinimumDuration: 1.0 / targetFPS];
    ```

    改成：

    ```objective-c
    [UnityCurrentMTLCommandBuffer() presentDrawable: surface->drawable];
    ```



4. xcode工程target下的Build Phases标签里，找到Link Binary With Libraries，在里面找到GameController.framework，把status由Required 修改成Optional。
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
2. 要修改平台设置，路径： Edit -> Project Settings -> Player -> ios平台，Other Settings
   - color space 选择 Gamma。
   - 关闭metal（2019模拟器不支持metal）
   - targetsdk选择模拟器sdk

![unity ios build 设置](/img/2021/unity_simulator_build.png)

<center style="font-size:14px;color:#C0C0C0;text-decoration:underline">unity ios build 设置</center>

> 打完包导出xcode工程后，其实会打包失败的，因此直接在xcode工程修改，需要修改MetalHelper.mm文件，

![build fail](/img/2021/build_fail_for_simulator.png)

<center style="font-size:14px;color:#C0C0C0;text-decoration:underline">编译报错</center>



> [UnityCurrentMTLCommandBuffer() presentDrawable: surface->drawable afterMinimumDuration: 1.0 / targetFPS];

改成：

> [UnityCurrentMTLCommandBuffer() presentDrawable: surface->drawable];



>  如果遇到模拟器ios 11以下运行闪退，先在xcode选择目标模拟器ios 11运行，闪退后在xcode的运行日志里可看到闪退的信息，一般是xxx.framework不支持。

[dyld: Library not loaded: /System/Library/Frameworks/AuthenticationServices.framework/AuthenticationServices](https://www.jianshu.com/p/9028e2ef4ad4)

我的是AuthenticationServices.framework报错，修改内容：xcode工程target下的Build Phases标签里，找到Link Binary With Libraries，在里面找到AuthenticationServices.framework，把status由Required 修改成Optional。


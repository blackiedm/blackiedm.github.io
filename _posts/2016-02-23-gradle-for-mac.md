---
layout: post
title:  "gradle for mac"
date:   2016-02-23 19:47:25
categories: gradle
tags: android
---

配置流程
---

* 配置用户级环境变量`.bash_profile`
* 打开终端输入 `open .bash_profile`
* 打开并编辑 `export GRADLE_HOME=/Users/yql/gradle-2.2.1`（这里路径记得填写正确
* `export PATH=$PATH:$GRADLE_HOME/bin`
* 保存关闭，然后记得更新 `source .bash_profile`
* 查看是否配置成功 `gralde -version`
* 如果提示没有`gradle`命令，则有可能是：
1. `GRADLE_HOME`路径可能不对；
2. 没有执行`source .bash_profile`

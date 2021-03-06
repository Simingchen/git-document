### 前言

Git 具有快速、分布式、可离线等优点，已成为目前最流行的版本控制软件之一。Git 使用元数据存储源文件的版本信息，并且新建的分支存储于本地，这种特性令 Git 的分支操作非常便捷。然而 Git 并没有严格的分支管理规范，高度的灵活性造成目前市面上存在多种多样的 Git 分支开发策略，质量也参差不齐。

* 下图是目前比较普遍的一种 Git 分支管理策略。

![git流程图](https://135editor.cdn.bcebos.com/files/users/490/4904074/202011/0YpqsgULI_95nQ.png)

* **master** -- 主分支，存储已发布版本的源码，不能在此分支上进行开发，只能合并 release 和 hotfix 分支。

* **hotfix** -- 热修复分支，用来修复线上的紧急 Bug,以线上版本对应的主分支为基础新建。

* **release** -- 预发布分支， 也可以称为提测分支，可以在此分支上修复 Bug,以 develop 分支为基础新建或者合并 develop 分支。

* **develop** -- 开发分支， 用于汇总各feature分支，只能合并，不能在此分支.上进行开发。

* **current feature** -- 当前版本迭代功能的分支， 业务开发人员均在 feature 分支上进行开发。

* **future feature** -- 未来版本迭代功能的分支，比如某个非常重要的功能需要在几个版本之后开放，且开发耗时较长，所以需要提前投入开发。如果项目中没有类似场景，可忽略此分支类型。


#### Git 分支管理流程中，有以下几点需要特别注意。

1. 负责修复线上紧急 Bug 的 hotfix 分支在开发完成之后必须合并到当前正在开发中的 develop 分支，否则会造成下次发布版本中丢失 hotfix 的修复代码。

2. release 分支在测试阶段可能会有频繁的修复 Bug 的行为，如果在此过程中同时进行下一个版本的迭代，必须在修复 Bug 之后将 release 分支合并到 develop 分支，否则会引起 3.0 版本发布后 2.0 版本既有功能出现问题。

### 适用性

从适用性角度来讲，不同规模、分工的团队所采用的分支策略也各有不同。如只有一个人的团队直接在主分支上开发也无伤大雅，但是对于涉及多人协作完的项目来说，严谨的分支管理策略能够在很大程度上增强源码的可维护性。

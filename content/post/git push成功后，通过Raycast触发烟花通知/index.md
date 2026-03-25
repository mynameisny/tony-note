---
title: "Git Push成功后，通过Raycast触发撒花通知"
summary: "‌Raycast Confetti‌ 是 Raycast 应用中的一个趣味功能，用于在完成特定任务或达成目标时触发全屏撒花动画，以示庆祝。本文介绍如果实现在Git Push代码成功之后触发这个动画的功能。"
keywords: "git push成功后，通过Raycast触发烟花通知"

date: 2026-03-24T16:44:11+08:00
lastmod: 2026-03-24T16:44:11+08:00

categories:
  - 经验技巧
tags:
  - git
  - hook
  - raycast
  - deeplink
  - MAC
---

### Raycast Confetti

Confetti [kənˈfeti]：五彩纸屑

Raycast Confetti‌ 是 Raycast 应用中的一个趣味功能，用于在完成特定任务或达成目标时触发全屏撒花动画，以示庆祝。

可以在终端中通过执行它的 **Deeplink** 来触发：`open raycast://extensions/raycast/raycast/confetti`

<br>



### 如何和Git集成

Git 本身不支持原生的 post-push hook。 官方支持的客户端 hooks 中，只有 pre-push（推送前触发），没有 post-push（推送后触发）。

> **为什么不支持**
> git push 是网络操作，可能失败（网络中断、权限不足、冲突等）。Git 设计上倾向于在本地操作成功后再触发 hook，而推送的远程结果对本地而言是"异步"且"不可靠"的。简言之就是Push的成功或失败应该是服务端来判断的。



### 解决方案

用 alias 包装 `git push`，当执行 `git pushf` 时，其实是在执行一段 bash 脚本

```bash
git config --global alias.pushf '!f() { 
  git push "$@"; 
  if [ $? -eq 0 ]; then 
    echo "🚀 Push 成功！代码已发射"; 
    open "raycast://confetti"; 
    say "Push successful"; 
  else 
    echo "💥 Push 失败"; 
  fi 
}; f'
```



#### 方案解析

```bash
git config --global alias.pushf '!f() { ... }; f'
```

- `alias.pushf`：定义一个新命令 👉 `git pushf`，pushf是可以自定义的
- `!`：**告诉 Git：后面不是 Git 子命令，而是 Shell 命令**
- `f() { ... }; f`：
  - 定义一个 shell 函数 `f`
  - 然后立刻执行它



##### 1️⃣ 执行真正的 push

> 这一步非常关键，否则 alias 就“吃掉参数”了

```
git push "$@";
```

- 调用原生 `git push`
- `"$@"`：把你传的所有参数原封不动传进去

**举例**

```
git pushf origin main
```

等价于：

```
git push origin main
```

<br>



##### 2️⃣ 判断 push 是否成功

> 这句意思是：如果 `git push` 成功（exit code = 0）

```
if [ $? -eq 0 ]; then
```

- `$?` = 上一条命令的**退出码（exit code）**
- `0` 表示成功，非 0 表示失败

<br>



##### 3️⃣ 成功时执行的逻辑 🎉

```bash
# 打印提示
echo "🚀 Push 成功！代码已发射";

# 触发 Raycast 的彩带动画
open "raycast://confetti";

# 使用MacOS的自带语音播报
say "Push successful";
```

<br>



##### 4️⃣ 失败时执行的逻辑

> 如果 push 失败，就只打印一行提示

```
else 
  echo "💥 Push 失败"; 
fi
```

<br>



##### 5️⃣ 函数结束并执行

- f() { ... }; 是方法定义

- f是方法调用

<br>



#### 恢复环境

> 验证：git config --global --get alias.pushf，如果没有任何输出，说明已经删掉了

```bash
git config --global --unset alias.pushf
```


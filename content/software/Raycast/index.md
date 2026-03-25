---
title: "Raycast"
summary: "Raycast是一个macOS上的快速启动器应用，和mac系统自带的启动器Spotlight很像，但是功能远比它的前辈丰富。我们可以通过纯键盘操作，直接在Raycast输入框中调用各种各样的功能。"
keywords: "Raycast MacOS 快速启动器"

date: 2026-03-23T23:39:45+08:00
lastmod: 2026-03-23T23:39:45+08:00

categories:
 - 软件
tags:
  - Raycast
  - MacOS
  - 启动器
  - 效率
  - 工具
---

## 执行命令

| 关键词            | 类型        | 含义                  |
| ----------------- | ----------- | --------------------- |
| store             | Command     | 打开Raycast的应用商店 |
| clipboard history | Command     | 打开剪贴板历史        |
| calendar          | Application | 打开Mac系统的“日历”   |
| calendar          | Command     | My Schedule，查看日程 |
| weather           | Application | 打开Mac系统的“天气”   |

<br>



## 代码片段

- 新建：打开 Raycast → 输入 `Snippets`，选择`Create Snippets`
- 删除：打开 Raycast → 输入 `Snippets`，选择`Search Snippets`，选中想要删除的脚本，用快捷键`Cmd + k`呼出菜单后，选择`Delete Snippet`

| 名称（Name）   | 内容（Snippet）                 | 关键词（Keyword） |
| -------------- | ------------------------------- | ----------------- |
| 输入今天的日期 | {date format="yyyy-MM-dd EEEE"} | ;today            |

<br>



## 窗口管理

| 关键词            | 类型              | 含义                             |
| ----------------- | ----------------- | -------------------------------- |
| left half         | Window Management | 保留左半边窗口（Maximize可恢复） |
| right half        | Window Management | 保留右半边窗口（Maximize可恢复） |
| Top half          | Window Management | 保留上半边窗口（Maximize可恢复） |
| bottom half       | Window Management | 保留下半边窗口（Maximize可恢复） |
| Maximize Weight   | Window Management | 全宽                             |
| Maximize Height   | Window Management | 全高                             |
| Toggle Fullscreen | Window Management | 全屏（Maximize可恢复）           |

<br>



## 计算器

>快捷键
>
>- `↵` 复制结果到剪贴板
>- `⌘ ⇧ ↵` 把结果作为搜索框的输入

### 汇率

| 关键词        | 含义                | 示例  |
| ------------- | ------------------- | ----- |
| 1 cny         | 1人民币兑换多少美元 | $0.15 |
| 1 USD to YUAN | 1美元兑换多少人民币 | ¥6.88 |
| 1$            | 1美元兑换多少人民币 | ¥6.89 |
| 10 usd in gbp | 10美元兑换多少英磅  | £7.47 |



### 温度

| 关键词   | 含义               | 示例    |
| -------- | ------------------ | ------- |
| 23C to F | 23摄氏度转成华氏度 | 73.4 °F |



### 重量长度

| 关键词          | 含义           | 示例                 |
| --------------- | -------------- | -------------------- |
| 0.75kg          | 0.75kg是多少磅 | 1.6534669664 lb      |
| 1oz to g        | 1盎司是多少克  | 28.349523125 g       |
| 1t to oz        | 1吨是多少盎司  | 35,273.9619495804 oz |
| 29 inches to cm | 29英寸转成厘米 | 73.66 cm             |

<br>



### 算术计算

| 关键词      | 含义            | 示例         |
| ----------- | --------------- | ------------ |
| 55 * 123    | 乘法            | 6,765        |
| 2^3         | 2的3次方        | 8            |
| 2**3        | 2的3次方        | 8            |
| 2 power 3   | 2的3次方        | 8            |
| sqrt(9)     | 9的平方根       | 3            |
| 9%2         | 9对2取余        | 1            |
| pi * 1      | π               | 3.1415926536 |
| 50% of 5000 | 5000的50%是多少 | 2,500        |

<br>



### 日期时间

#### 基准时间

| 关键词     | 含义         | 示例     |
| ---------- | ------------ | -------- |
| today      | 今天         | March 22 |
| tomorrow   | 明天         | March 23 |
| yesterday  | 昨天         | March 21 |
| now        | 当前时间     | 22:26    |
| this year  | 今年是哪年   | 2026     |
| this month | 这个月是几月 | March    |
| this week  | 今天是几号   | March 22 |



#### 时间偏移

| 关键词             | 含义              | 示例     |
| ------------------ | ----------------- | -------- |
| 3 days after today | 3天后是几号       | March 25 |
| 2 week after today | 2周后的今天是几号 | April 5  |

| 关键词      | 含义                      | 示例     |
| ----------- | ------------------------- | -------- |
| 1 days ago  | 1天前是几号（不包含今天） | March 21 |
| 3 days ago  | 3天前是几号（不包含今天） | March 19 |
| 3 weeks ago | 3周前是几号               | March 1  |

| 关键词         | 含义             | 示例     |
| -------------- | ---------------- | -------- |
| next week      | 下周的今天是哪天 | March 29 |
| next month     | 下个月几月       | April    |
| next year      | 明年是哪年       | 2027     |
| next wednesday | 下周三是几号     | March 25 |

| 关键词         | 含义                                                         | 示例     |
| -------------- | ------------------------------------------------------------ | -------- |
| last week      | 上周的今天是哪天                                             | March 15 |
| last month     | 上个月几月                                                   | February |
| last year      | 去年是哪年                                                   | 2025     |
| last wednesday | 上周三是几号<br />（一定要注意，老外的一周是周日，如果周日问上周三，其实还是我们的这周三） | March 18 |



#### 时间属性

| 关键词       | 含义                   | 示例 |
| ------------ | ---------------------- | ---- |
| day of year  | 今天是一年中的第几天   | 81   |
| day of month | 今天是一个月中的第几天 | 22   |
| week of year | 这周是一年中的第几周   | 12   |



#### 时间差/计算

| 关键词                 | 含义                   | 示例                |
| ---------------------- | ---------------------- | ------------------- |
| now + 15min            | 15分钟后               | 23:47               |
| now + 3 hours          | 3小时后                | Tomorrow at 02:34   |
| today 18:00 - now      | 距离18点过了多久       | 5 hours 34 min 48 s |
| 2026-12-25 - today     | 距离圣诞还有多少天     | 9 months 2 days     |
| now until 23:50        | 现在距离23:50还有多久  | 4 min 27 s          |
| today until 2026-04-05 | 今天距离4月5号还有多久 | 1 week 6 days       |



### 格式化

| 关键词                   | 含义                      | 示例                      |
| ------------------------ | ------------------------- | ------------------------- |
| today in yyyy-MM-dd      | 按”年-月-日“格式化        | 2026-03-23                |
| today in MM/dd/yyyy      | 按“月/日/年”格式化        | 03/23/2026                |
| today in yyyy-MM-dd EEEE | 按“年-月-日 星期几”格式化 | 2026-03-24 Tuesday        |
| now in HH:mm             | 按小时分钟显示当前时间    | 23:38                     |
| now in HH:mm:ss          | 按小时分钟秒显示当前时间  | 23:38:42                  |
| now in ISO               | 按ISO格式显示当前时间     | 2026-03-23T23:39:36+08:00 |
| now in utc               | 按UTC格式显示当前时间     | March 23, 2026 at 16:44   |



### 时区

| 关键词        | 含义           | 示例                    |
| ------------- | -------------- | ----------------------- |
| now in tokyo  | 东京现在是几点 | 01:14                   |
| now in London | 伦敦现在是几点 | March 23, 2026 at 16:15 |

<br>



## 插件

- Kill Process: 一键关闭进程

- ray.so: 一键生成代码块

- Honorable Mention - Year in Progress: 年进度

<br>



## 娱乐

| 关键词   | 类型    | 含义                                                         |
| -------- | ------- | ------------------------------------------------------------ |
| Confetti | Command | 屏幕上播放礼花动画<br />可以在终端中执行这个Deeplink：`open raycast://extensions/raycast/raycast/confetti`，或者将这个deeplink加入到`post-commit`的Git钩子中，这样每次完成commit都会播放一次礼花动画 |





## 参考链接

- Calculator Extension for Mac | Raycast https://www.raycast.com/core-features/calculator

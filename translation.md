阅读汇编代码（read the assembly）

使用调试器（use a debugger）

这其实就是典型的 CSAPP Bomb Lab：

反汇编
  ↓
阅读汇编
  ↓
理解程序逻辑
  ↓
使用 gdb 调试
  ↓
找出正确输入

2. 实验材料与提交
2.1 你会得到什么
文件	说明
bomb	炸弹本体：一个 x86-64 Linux 可执行文件。不要修改它。
bomb.c	你唯一能看到的源代码，只有 main 函数，没有任何 phase 的具体逻辑
solution.txt	用来填写你的答案，每个阶段一行，一共 5 行
bomb.sha256	用于检查 bomb 有没有被修改过的校验和
tools/autograde.sh	自动评分脚本
.github/workflows/autograde.yml	GitHub Actions 工作流，用来触发自动评分

这里最重要的是：

bomb.c 不会直接告诉你每个 phase 怎么做

也就是说你不能直接看：

phase_1(...)
phase_2(...)

因为这些逻辑藏在：

bomb

这个二进制文件里面。

所以你需要：

bomb
 ↓
反汇编
 ↓
查看汇编
 ↓
推断程序逻辑

这正是这个实验要练的东西。

2.2 怎么提交

首先：

使用这个模板创建你自己的 GitHub 仓库。

然后：

把你的答案写入 solution.txt
commit
push

之后打开 GitHub 仓库的：

Actions

找到：

Autograde

然后：

Run workflow

运行自动评分。

完成之后，可以在运行结果底部的：

Summary

里面看到评分报告。

另外，评分报告也会作为：

autograde-report

这个 artifact 保存下来。

3. 开始实验

这个炸弹是：

Linux x86-64 ELF 可执行文件

所以你需要：

Linux
或者 Windows + WSL2

这也正好和你之前问的 WSL 有关系。

第一步：给 bomb 执行权限
chmod +x bomb

意思是：

给 bomb 添加可执行权限。

然后可以故意输入一个错误答案：

./bomb

然后输入：

test

你会看到：

BOOM!!!

以及：

The bomb has blown up.

意思就是：

炸弹爆炸了。

3.1 用文件输入答案

你还可以：

./bomb solution.txt

让炸弹从 solution.txt 读取答案。

它的行为是：

solution.txt
     ↓
读取一行
     ↓
测试 phase 1
     ↓
通过
     ↓
读取下一行
     ↓
测试 phase 2
     ↓
……

这非常方便。

因为你解决完一个 phase 后，可以把答案写入：

solution.txt

以后就不用每次重新输入之前已经解决的答案了。

solution.txt 一开始是什么样？

它一开始有 5 行：

???
???
???
???
???

你解决一个，就替换一个。

例如解决了 phase 1：

正确答案1
???
???
???
???

解决 phase 2：

正确答案1
正确答案2
???
???
???

一直到：

正确答案1
正确答案2
正确答案3
正确答案4
正确答案5
3.2 单独测试某一个 Phase

这个功能非常有用。

如果你卡在 phase 3，可以直接：

./bomb --phase 3

意思：

只运行第 3 个 phase。

它只要求你输入一行。

也可以：

./bomb --phase 3 line3.txt

意思是：

从 line3.txt 中读取 phase 3 的答案。

如果正确：

[phase 3] PASS

退出码：

0

如果错误：

[phase 3] FAILED

退出码：

1
所以有两种运行模式
普通模式
./bomb solution.txt

依次：

phase 1
 ↓
phase 2
 ↓
phase 3
 ↓
phase 4
 ↓
phase 5

如果某一步爆炸：

phase 1
 ↓
phase 2
 ↓
phase 3 💥

就停止。

单独模式
./bomb --phase 3

直接：

phase 3

特别适合调试。

4. 评分
项目	规则
分数	每个 phase 20 分，总共 100 分
每个 phase 独立评分	每个 phase 单独评分
phase 3 错误	不影响 phase 4、5 的得分
二进制完整性	bomb 会通过 bomb.sha256 检查有没有被修改
修改 bomb	0 分
评分报告	会显示每个 phase 是 ✅ 还是 ❌

所以：

phase 1 → 20
phase 2 → 20
phase 3 → 20
phase 4 → 20
phase 5 → 20
----------------
总分     100

如果只做出来 3 个：

phase 1 ✅
phase 2 ✅
phase 3 ❌
phase 4 ❌
phase 5 ❌

那么前两个仍然可以得到分数。

5. 参考资料

实验推荐参考：

《Computer Systems: A Programmer's Perspective》

也就是你现在正在看的：

CSAPP《深入理解计算机系统》

特别是：

Chapter 3
程序的机器级表示

另外还可以参考：

Carnegie Mellon University 的 CS:APP Bomb Lab 实验说明

⭐ 你现在最应该关注什么？

结合你最近正在学的 CSAPP 第 3 章，这个实验其实就是把你现在学的东西真正用起来。

你现在学：

C语言
 ↓
汇编
 ↓
寄存器
 ↓
cmp
 ↓
条件码
 ↓
set
 ↓
跳转

到了 Bomb Lab：

bomb
 ↓
反汇编
 ↓
看到 cmp / test / mov / add / sub / jmp / jne / je ...
 ↓
分析寄存器和内存
 ↓
搞清楚程序在判断什么
 ↓
得到正确输入

所以你现在看不懂 Bomb Lab 很正常。你目前刚学到 CMP / 条件码 / SET，而 Bomb Lab 往往还会综合：

mov
lea
cmp
test
jmp / je / jne / jg / jl
栈
函数调用
参数传递
数组
指针
内存寻址
gdb

这些东西。

**不过你现在开始接触这个 Bomb Lab 是可以的。**建议不要直接上来硬啃全部 5 个 phase，而是先把 phase 1 的汇编贴出来，我们可以
按照你现在学习 CSAPP 的方式，一条一条解释：这条指令干什么 → 寄存器是什么 → 条件怎么判断 → 最后怎么推出输入。

## 总之就是:
Phase N
   ↓
① 找到 Phase N 的函数
   ↓
② 反汇编，查看汇编代码
   ↓
③ 看这个函数接收什么输入
   ↓
④ 一条一条分析汇编
   ↓
⑤ 搞清楚它要求输入满足什么条件
   ↓
⑥ 得到正确答案
   ↓
⑦ 用 ./bomb --phase N 测试
   ↓
⑧ PASS
   ↓
把答案写入 solution.txt
   ↓
进入下一个 PhasePhase N
   ↓
① 找到 Phase N 的函数
   ↓
② 反汇编，查看汇编代码
   ↓
③ 看这个函数接收什么输入
   ↓
④ 一条一条分析汇编
   ↓
⑤ 搞清楚它要求输入满足什么条件
   ↓
⑥ 得到正确答案
   ↓
⑦ 用 ./bomb --phase N 测试
   ↓
⑧ PASS
   ↓
把答案写入 solution.txt
   ↓
进入下一个 Phase


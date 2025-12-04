
# NI Teststand 样例拆解系列文章——（1）下载安装与环境配置，以及Computer Motherboard Test计算机主板测试拆解

---

# 前言

最近由于工作原因，需要学习NI公司的测试执行软件Teststand，但由于Teststand没有官方中文语言包，同时国内的教程比较少，因此我打算从其自带的examples入手，对各类样例进行拆解，进行逆向工程，同时记录并发布。


---

# 一、下载安装

问题最多的部分，首先是NI官网的服务器不太稳定，同时国内访问速度比较慢，偶尔会登录不了，需要看运气。
[NI官网链接](https://www.ni.com/zh-cn.html)

在登录后找到“产品与服务”
![ 你啥都](https://i-blog.csdnimg.cn/direct/1b318cff836243178c27378bb5058e46.png)

选择“下载或免费试用”，点击“下载”
![下载](https://i-blog.csdnimg.cn/direct/cb5e93264b40460e97e8a1c021697222.png)

需要注意的是，NI系列软件都是使用NI package manager 进行统一下载安装管理的。

下载安装完成后，未登录的情况下只有7天试用期，登录账号的情况下有45天试用期，账号需要邮箱注册。


# 二、主界面分析拆解

![主界面](https://i-blog.csdnimg.cn/direct/e14679c836a949f5b4ca2021f6c938a7.png)

## 1. 菜单栏

常规软件的菜单栏，其中，“Configure”我们后续会调整其中的“Adapters”编程语言适配器的部分设置。
Help菜单的功能根据实际试用，都无法使用，可能是网络IP问题，无论是哪里的帮助按钮都会自动跳转NI官网并显示“无结果”，少部分会跳转至用户手册。此处我给出用户手册的链接。
[Teststand用户手册官网](https://www.ni.com/docs/zh-CN/bundle/teststand/page/user-manual-welcome.html)

同时还有网盘链接，方便访问，其中还有单独的样例用户手册
[度盘Teststand用户手册]( https://pan.baidu.com/s/1yw16eGbmGquRzZmFpmOzPw?pwd=lfty)

## 2. 导航栏

点击导航栏左上角的第一个图表，就可以显示“Insertion Palette”即插入面板。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/574dae2ce1a243488bb6efce5f8b97fe.png)

其中有很多测试序列子项，这个我们后续拆解样例的时候就会了解各是什么功能了。

## 3. 序列窗口

这个窗口会展示你目前编辑的序列中的所有子项以及运行顺序，也可以在这个窗口选中某一项序列，查看它的变量和设置。以我们后文使用的样例举例：
点击“File”菜单，点击“Open File”找到如下路径：
C:\Users\Public\Documents\National Instruments\TestStand 2025 (64-bit)\Examples
（根据版本不同可能会有差异）

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b010838bd9264b8bbc7b2999e6118f28.png)

选择打开“Examples.tsw”文件，tsw即test workspace。
此时我们发现，打开了一个工作区“Workspace”，选择其中的Demos-Computer Motherboard Test-python-**Computer Motherboard Test.seq**文件。
seq即sequence，序列文件

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b7adbc00b4ec4f5aad249e0f73ee67ba.png)
此时我们在序列窗口就可以看到一个完整的测试序列了。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/fe0c748beee04bb2934aec201c21af59.png)

如果我们想要设置断点，那么在绿色箭头这一列的位置，在你想要设置断点的地方点一下就能看到红色的断点，比如我在第一项设置断点后，就能看到箭头指的这个断点了。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/dd4c600f4bf84ed9a864536cbd7ca079.png)

## 4. 变量/序列窗口

这一部分比较复杂，我们一点点来。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5b466c4898334c5b9e80274053dc5868.png)

首先，我们要认识到，所有序列自身都存在一些参数，主要是该序列的测试结果“Result”，以及其中的布尔量“Passfail”。
其次，在运行测试的过程中，主序列是存在“RunState”这一状态以及状态包含的各种参数的，比如主序列测试是否出现了错误“SequenceFailed”，或者当前循环的次数“LoopIndex”。

除此之外，还有常见的Locals、Parameters这两个本地变量，以及FileGlobals当前序列文件的全局变量，以及StationGlobals整个软件的全局变量。
需要注意的是，Locals、Parameters、FileGlobals中的变量是需要自己设置的。

另外，我们还可以点击“sequence”以查看主序列和所有的子序列。

## 5. 设置窗口

是针对每一个子项序列的设置窗口，以“Powerup Test”为例，我们可以在“module”界面设置它的各项参数，同时设定它使用的module（代码文件）和函数。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5292ed6ab86a43d0bdcb24f3d895a225.png)

可以在 Data Source 中直接查看和修改表达式
可以在 Properties 中设置各项参数和各类逻辑，要注意的是，图上红框框出来的部分是可以切换的一个选项列表！我刚上手的时候想设置precondition找了半天不知道在哪，才发现在这里！

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4affac0bd17d4301a5fcb706f28661c2.png)

---

# 三、样例拆解——Computer Mother Test-python

根据上文，我们具体来分析这个计算机主板测试样例。

## 1. python环境配置

首先是python环境，我用的是最新的2025 Q3版本，需要注意的是，该版本不支持最新的python 3.14，只支持 3.9 - 3.13版本。
在已经正常安装好python的情况下，找到菜单栏的“Configure”-“Adapters”

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/35655bf8af8341098abfb34d87d48f63.png)

选择“python”，点击“Configure...”

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2a23cc95242a4986ba9b681be935c404.png)

设置好Version版本，否则后续会报错，且闪烁红色感叹号。
对于实际的代码以及运行逻辑流程，如果想要看的话，就需要一个合适版本的 VS Code，同时，需要在python中安装一个debug库，否则会出如下提示：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8ce9a4b70aab4ff6a38439efdcab6e18.png)

如果没有的话可以`win + R`输入“cmd”，键入

```
pip install debug
```

完成安装后，点击Enable debugging。随后重启Teststand和VS Code（可以直接重启电脑），否则会出提示：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8db5bb42e50f403aadb828a3c399518b.png)


这样，在后续设置断点逐个步进的时候就能够把Teststand和VS Code连接起来了。

## 2. 序列整体逻辑分析

该样例本质上是一个模拟仿真的故障检测环境，

### 1. 设置（Setup）

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a39eb25591a746b8a7555ae56bc197bb.png)

- Simulation Dialog：一个模拟对话框界面，设置断点观察可以发现，在运行结束后，会出现如下的界面：
- 
  ![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/617c2b08e8bc497ea910eaaefedca856.png)
  
  我们可以选择，在这一次模拟中，我们想让哪一部分出现问题，假设我选择其中ROM出现错误，并点击“OK”，那么后续测试流程中，在做ROM测试的时候，就会反馈“Failed”。
  这一步调用的是dll文件，目的是用Windows的原生API生成这个窗口，后续都是.py的代码文件。

- Initialize Computer Test
  初始化测试，在python代码中定义函数、参数等

- Turn Vacuum Table On
  打开真空吸盘，这个翻译比较抽象，实际上，对于自动化测试而言，这一步的含义就是我的夹具夹到我要测试的产品了，也就是我们固定好产品的位置了

### 2. 主要测试内容（Main）

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/616578d02c1f4d62adcd292a6c54dc25.png)

- Powerup Test
  上电测试，测试产品是否上电成功

- 第一层 if 结构
  我们点击这个 if 结构，可以看到它的表达式是：

```py
RunState.Sequence.Main["Powerup Test"].Result.PassFail
```

如果我们设置了产品上电测试故障，那么，在上一步，该测试会Failed，`PassFail`的值是`False`，则这一步直接跳转到Else里面的
Powerup Diagnostics 上电诊断，来诊断上电测试失败的原因。

如果上电测试通过，则继续下面的步骤：
CPU Test 这个蓝色Icon是一个新的概念——“子序列”，我们双击该子序列可以看到其中包含的测试项如下：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9011627d5615435a97af95e2ab5deb53.png)

点击左上角的箭头可以返回主序列，我们找到右侧“变量/序列窗口”的序列，可以发现，是存在该子序列的。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7c44589f466e447ea5b7cc815f5de245.png)

我们右键空白处，选择“Display Sequence Hierarchy”就可以看到当前序列的等级关系了

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/db8e6233239b40d49af1ae88e3327e7a.png)

等级关系如下，我们关掉这个窗口回到测试序列。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/ba00e40fe95b4f7b85fa339cdc0fc75e.png)

后续就是ROM Test、RAM Test、Video Test和Keyboard Test，这些测试的整体逻辑是一致的，不过ROM Test和RAM Test这两个项的返回值的布尔量，Video Test和Keyboard Test这两个项的返回值是数字，因为测试内容不一样。

-- 第二层 if 结构
这个 if 结构的表达式是：

```py
ThisContext.SequenceFailed
```

我们可以在右侧窗口找到这个变量，这是一个系统自带的布尔变量`SequenceFailed`，你的测试序列中一旦出现错误，产生“Failed”，这个变量就会变成`True`，随后进入诊断：

诊断与测试一一对应，需要注意的是，每个诊断序列都有一个前置条件`Precondition`，该条件在Properties中设置，如图所示：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6ad20bea418e4f25a5132234cec3e53d.png)

只有当某个部分的测试不通过时，我们才需要运行这一部分的诊断操作，测试通过的，则会直接“Skip”，如图所示：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/3c6de692b27e4a9491ed737db16201ee.png)

（实际测试中，这里还应该有一个“下电”的过程）

### 3. 清理（Cleanup）

- Turn Vacuum Table Off
  关闭真空吸盘，也就是夹具释放产品，测试结束

# 总结

边拆边写边学，我认为Teststand的功能还是很不错的，界面也很高效简洁。后续应该会继续拆解相关样例，并继续学习该软件。


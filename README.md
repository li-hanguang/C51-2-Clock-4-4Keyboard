# C51-2-Clock-4-4Keyboard
基于两块STC89C51RC最小系统板双机通信下的的4*4矩阵键盘控制的8位8段电子数码管时钟

我上传了两个版本的工程文件：
      A.仿真版：使用蓝色8位8段共阴数码管
      B.实物版：使用红色8位8段共阳数码管
  两个版本的原因：最初先仿真实现。但买不到8位8段共阴数码管，又懒得自己打印PCB，结果买了个共阳的数码管，商家连资料都不给提供，引脚连接是错误的，好在统一的引脚是一致的。另外，我在仿真的时候使用轮询的方式来显示时间，仿真是可以的，但在实际的板子上不可用，这就有点魔幻了，哈哈哈QAQ（很多情况下，仿真能用的程序上板不一定行，板子上能用的仿真就不能用QAQ）
  然后我苦逼的一个IO口一个IO口的把段码位测出来了，基本上是手撸驱动代码哈哈哈。

项目说明：
1号机：当有按键按下时，通过中断启动扫描矩阵键盘；
将相应的键值通过串口发送到2号机。
2号机：负责驱动显示8位7段数码管显示时钟。
接收来自1号机发送的键值，并根据发送的内容控制时钟的工作。

系统设计/功能按键：
（1）8位7段数码管显示时钟格式：00-00-00
（2）系统上电启动后时钟开始从00-00-00开始计时；
（3）4X4键盘布局为：
                  1 2 3 h
                  4 5 6 m
                  7 8 9 s
                  T 0 R S
           其中：h m s-分别为小时、分钟、秒设置键，S-时钟设置键，R-运行键，T-未定义；
（4）以中断方式调用键盘扫描程序识别键值；
（5）1号机通过串口发送键值到和2号机；
（6）当按下S键时，时钟显示直接停止；
（7）按下S键后，再按h/m/s键，相应的时钟显示位置变为只有a和d段亮，表示在该位置输入需要设定的值，且只能输入符合时间的值；
（8）再按下R键，时钟从设置好的时间开始运行。
  
顺便附一下图：

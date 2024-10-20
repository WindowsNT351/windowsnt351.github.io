---
layout: default
---

# IBM PS/55 5541-TC4
![Branching](./5541.jpg)<br />

## 机型简述(维基百科)
PS/55是IBM日本公司于1987年发布的个人电脑系列。PS/55 是IBM Multistation的后继产品，但其架构基于IBM PS/2。基于PS/2 Model 80的5570-S（话说这5570也是离奇的存在 https://diarywind.com/blog/e/ibm-ps5570s-spec.html ）除外，该系列的第一批产品由重新命名的 5550 型号组成。与 PS/2 不同，大多数基于 PS/55 的型号都具有32位（80386或80486）CPU 和MCA总线，适用于高端商业计算市场。由于IBM JX失败，日本IBM犹豫是否向消费者销售个人电脑。AT总线型号于1991年面向家庭用户发布。<br />

## 当前机器简述
2021年末收入，外壳被暴力快递暴力了。无配套显示器和键盘，但是由于类似PS/2，用VGA显示器和PS/2键鼠还是可以将就一下的，不过无法使用PS/55的全部功能（后面讲到）。<br />
机器的软驱似乎工作不正常，时好时坏的，修理了之后彻底死翘翘了。之后使用了 https://github.com/mdehling/p7x-floppy-adapter 的转接器，将普通软驱转成PS/2（PS/55）可用的软驱接口。转接器仅焊接一个电阻就能使用。<br />
另外似乎这个机器是中文特供（繁体），显卡字体ROM位置（应该是）焊接全部两个EEPROM，日版机只有一个（ https://www.ardent-tool.com/PS55/video/DA_B_II_New_Photo_Front.jpg ）。<br />
因为这是PS/55，所以肯定有点不一样的东西（什），这机器带一个非标准分辨率，Sync频率也很特别，我的显示器无法同步，在自检程序跑到这一步的时候总是报错，不过有人也遇到了和我这差不多的问题（ https://diarywind.com/blog/e/ibm-ps55t-bootup.html ），我就当是正常的了（摆了（（（ <br />

## 照片
### 主机
![Branching](./P1030930.JPG)<br />
![Branching](./P1030931.JPG)<br />
![Branching](./P1030932.JPG)<br />
![Branching](./P1030933.JPG)<br />
![Branching](./P1030934.JPG)<br />
![Branching](./P1030935.JPG)<br />
![Branching](./P1030936.JPG)<br />
### 内部
![Branching](./P1030938.JPG)<br />
### 内存提升卡（内存分着放我是头一次见）
![Branching](./P1030939.JPG)<br />
### 内存条（4M）
![Branching](./P1030940.JPG)<br />
### 显卡（Display-B2）
![Branching](./P1030941.JPG)<br />
![Branching](./P1030942.JPG)<br />
### 硬盘、MCA提升卡（这俩在一块）
![Branching](./P1030943.JPG)<br />
![Branching](./P1030945.JPG)<br />
### 主板
![Branching](./P1030946.JPG)<br />
### 原装软驱
![Branching](./P1030949.JPG)<br />
![Branching](./P1030950.JPG)<br />

## 奇怪的系统
### 尝试进入
说起这系统也奇怪，在英文模式下操作没问题，只要Switch到中文环境，事情就有点开始离谱了 <br />
首先登场的是键盘错误，显示BIOS-102，我很确定这并不是BIOS发出的消息，而是由切换到中文环境下的引导扇区发出的，不知道为什么要做这个检测，其实标准美式键盘完全可以将就使用一下。<br />
![Branching](./ibmps55t_9.JPG)<br />
^没时间拍了，借一下diarywind.com的图<br /><br />
我把硬盘中的根目录文件、PS2文件夹文件（相当于正常DOS中的英文DOS文件夹）、DOS文件夹文件（中文版DOS文件夹）复制到软盘，然后使用SYS命令在其他软盘上构建引导，再用软盘SYS迁移引导到虚拟硬盘中。<br />
迁移之后，在DOSVAX（PS/55模拟器）下，系统启动了，不过SWITCH到中文直接黑屏，打开DOSVAX的Debug窗（DOSVAX用DOSBOX改的），显示一直在调用一个中断。我对汇编的了解仅限于调用个简单的中断让LOGO.sys显示退出，所以我无法推断哪里出问题了。<br />
在使用软盘里的SYS对虚拟硬盘重新构建引导后，系统启动了，但是基本处于乱码的状态（基础字形SYS拒绝载入，导致后面的程序硬显示中文），大多数程序都拒绝启动。SWITCH到英文界面后，恢复正常。<br />
### 版本分析
在英文界面，COMMAND版本显示IBM DOS Version T5.01，VER显示IBM DOS 5.00。中文时，显示DOS T5.01。<br />
这里有一个命名方法:J是日语版，H是韩文版，P是简中，而T是繁中。（其实OS/2也是一样的）<br />
所以可以断定这是繁中版本。<br />
另外，只有基于KDOS（JDOS）版本才会检测键盘，所以这应该是一个K/JDOS改版。<br />

## 杂谈
【1】硬盘里还有原机的CADAM软件（应该也是中文），引导扇区可能没备份好，如果你知道怎么完整DUMP这种ESDI硬盘，请联系我！！！！！！<br />
【2】话说我那LPFK是不是和这机子一块用的（雾<br />
【3】3D打印的软驱盖板有点松松垮垮的（没测好卡扣导致的<br />
【4】话说这字体ROM怎么DUMP的，也想归档一下<br />
【5】就一个扬声器有必要带音量旋钮嘛（半恼<br />
【6】有什么好心人帮我做个5576键盘转接器，反向转接的那种<br />
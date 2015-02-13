#linux latex 安装

本文是在ubuntu14.10 64位操作系统，安装的texlive版本是2014，其它的linux系统类似。

##1.安装texlive
texlive是tex软件发行套装，包含与tex系统相关的各种程序/编辑与查看工具/常用宏及文档/常用字体及多国语言支持。

安装步骤如下：

* 下载[install-tl-unx.tar.gz]("https://www.tug.org/texlive/acquire-netinstall.html")
* tar -zxvf install-tl-unx.tar.gz
* cd install-tl-20140831 (install-tl-20140831 为解压后的目录)
* sudo ./install-tl
* 后面出来的选择中输入 i

##2.配置环境变量
* sudo gedit ~/.bashrc
* 在最后添加
```
TEXDIR="/usr/local/texlive/2014"
export PATH=$TEXDIR/bin/i386-linux:$PATH    # for 32-bit installation
export PATH=$TEXDIR/bin/x86_64-linux:$PATH  # for 64-bit installation
export INFOPATH=$INFOPATH:$TEXDIR/texmf-dist/doc/info
export MANPATH=$MANPATH:$TEXDIR/texmf-dist/doc/man
```
* 保存退出

##3.配置中文
在终端输入
```
tex --version
```
可以检查texlive是否安装成功。
此时texlive已经可以使用了，但是使用中文时会有问题，因为我们的linux系统里缺少对应的中文字体。
我们新建一个ctex.tex文档，内容如下：
```
\documentclass{ctexart}
\begin{document}
你好,\LaTeX!
\end{document}
```
在终端下切换到ctex.tex目录下，并输入：
```
xelatex ctex.tex
```
此时会显现错误如下：
```
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!
! fontspec error: "font-not-found"
!
! The font "SimSun" cannot be found.
!
! See the fontspec documentation for further information.
!
! For immediate help type H <return>.
!...............................................
l.5
{SimSun}
```
这是由于linux缺少字体的原因，解决办法如下：
* 在windonws系统下 C:\Windows\Fonts目录下将宋体(simsun)、黑体(simhei)、仿宋体(simfang)、楷体(simkai)这几个字体拷贝到 /usr/share/fonts目录下
* 执行
```
fc-cache
```
* 在ctex.tex中添加：
```
\setCJKmainfont{SimSun}
```
此时我们可以在latex中使用中文了,enjoy latex, enjor yourself!

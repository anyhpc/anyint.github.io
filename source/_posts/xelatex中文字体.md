opensuse xelatex 中文字体问题

以下文字为实际操作记录，
文字大量引用自 
http://www.bfcat.com/index.php/2013/10/ubuntu-12-04-kile-texlive2013cjk/
以及
https://huxuan.org/2012/07/14/chinese-font-problem-of-ctex-in-texlive-under-linux/
##

新建 /usr/share/fonts/winfonts 目录并且将需要的中文字体拷入
进入文件夹
	
cd /usr/share/fonts/winfonts

改变权限

	
sudo chmod 744 *

生成核心字体信息

	
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -f -v

此时用命令

	
sudo fc-list :lang=zh-cn

查看中文字体信息。

记下楷体和仿宋对应的名称，即显示信息中第一个英文
比如有的的系统中楷体是 KaiTi，仿宋是 FangSong
此处会因为安装的字体版本不同而有所差异

接下来只要将对应的字体修改即可，即
把[SIMKAI.TTF]修改为KaiTi
把[SIMFANG.TTF]修改为FangSong
需要注意不止一处

vim下的替换命令

	
:%s/\[SIMKAI.TTF\]/KaiTi/g
:%s/\[SIMFANG.TTF\]/FangSong/g

另一个解决方案是使用Adobe的字体，调用ctex包时增加adobefonts参数


以下引用自 http://bbs.ctex.org/forum.php?mod=viewthread&tid=58263&page=1#pid383083
原因是这样的（其实懒人就不必看了）：

在字体定义文件 ctex-xecjk-winfonts.def 中，楷体和仿宋不是使用字体全名，而是使用字体文件名表示的。如楷书是：
\setCJKfamilyfont{zhkai}{[simkai.ttf]}
之所以这样是因为在 Windows XP 中楷书和仿宋是 GB_2313 字符集的，只有 6000 多个汉字，楷体字体全名是 KaiTi_GB2312；而在 Windows Vista 以后和版本则是 GBK 大字库的，有 20000 多个汉字，字体全名是 KaiTi。为了避免为微软的不同操作系统版本写不同的配置文件（这样更麻烦，而且 Windows 用户是大多数），就把它直接用没有变化过的字体文件名表示。

这个修改就是我做的。当然对于 Linux 用户可能有一些副作用。因为上面的字体名使用的是小写字母，而通常大家拷贝的字体是大写字母（这算是我的疏忽）。你知道 Windows 不区分文件名大小写，但 Linux 区分，所以当然 Linux 找不到 simsun.ttf 这个字体了。

我实在不建议 Linux 用户修改 ctex-xecjk-winfonts.def 文件。你可以使用 Windows 字体加上默认选项，但注意你安装的中文字体文件名要匹配。还有一个办法是写自己的配置文件，ctex 宏包有自己的 cfg 文件，在 .../texmf-dist/tex/latex/ctex/cfg/ctex.cfg 中，你可以在这个文件里面添加你自己的 local settings。
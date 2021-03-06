##  Linux 基础命令
> 2019.2.28开始整理之前用过或忘掉的linux基础命令和linux基础知识, 每天整理三个， 加入新的有意思的命令


* [Linux 基础命令](#linux-基础命令)
	* [文件与目录基本操作](#文件与目录基本操作)
		* [nl 输出行号 显示文件](#nl-输出行号-显示文件)
		* [more less 显示文件内容](#more-less-显示文件内容)
		* [head tail 查看文件指定行](#head-tail-查看文件指定行)
		* [mkdir rmdir  目录操作](#mkdir-rmdir--目录操作)
		* [ls cp rm](#ls-cp-rm)
	* [系统信息](#系统信息)
		* [uptime uname](#uptime-uname)
		* [w  who  last](#w--who--last)
		* [date cal](#date-cal)
	* [命令系统](#命令系统)
		* [通配符 ? *  [list]](#通配符----list)
		* [任务管理 基本字符含义](#任务管理-基本字符含义)
		* [转义字符  "" '' \  重定向&gt; &gt;&gt;](#转义字符------重定向-)
	* [常用命令](#常用命令)
		* [wc 统计行数, 字符](#wc-统计行数-字符)
		* [tee 双向重定向](#tee-双向重定向)
		* [xargs 参数代换](#xargs-参数代换)
		* [sort 排序](#sort-排序)
		* [uniq 去重](#uniq-去重)
		* [awk 世界上最好的语言](#awk-世界上最好的语言)
		* [grep  文本检索](#grep--文本检索)
		* [tr 字符转换](#tr-字符转换)
		* [find 文件查找](#find-文件查找)
		* [dd 磁盘管理(备份)](#dd-磁盘管理备份)
		* [cat  tac 查看文件内容](#cat--tac-查看文件内容)
		* [cut 文本切割](#cut-文本切割)


---


### 进程管理


**2019.3.11**
> 今天整理kill, pkill, pstree
#### kill 根据pid发送信号
> kill 删除执行中的程序和工作， 给进程发送信号  
> kill -l 查看所有信号，  -9 可以强制杀死 , 但是使用时要注意， 可能会出现数据丢失状况。。， 还没遇到过  
> ps 查看进程号， kill杀死， 我一般用-9， 不然真的杀不死  

#### pkill 控制同名所有的进程
> pkill 选项 名字  
> 是ps和kill的结合，   
> pkill dingding    #我一般拿他来杀死钉钉  
> pkill -u moying   #杀死指定用户的所有进程， 还可以踢用户
[更多介绍](http://linux.51yip.com/search/pkill)

#### pstree 树状图显示进程
> 以树状图显示进程，只显示进程的名字，且相同进程合并显示。
> pstree -p   还显示pid， 一个很帅的命令， 显示一整个进程树，很壮观， 
> 最后可以搭建一个samba服务器， 实现文件共享。。找到工作了解一下


---
**2019.3.10**
> 今天整理进程管理相关命令, free, top, ps

#### free 打印内存情况
> free 可以输出当前系统内存占用情况， 经常用free -m 来规范输出  
> 因为我只看内存占用， 用的不多， [更多介绍参考](https://www.cnblogs.com/coldplayerest/archive/2010/02/20/1669949.html)

#### ps  进程详细信息
> ps 可以用来像是当前系统的瞬间进程状态， 进程是否结束， 僵尸进程，占用资源  
> ps查看的是当前瞬间的进程状态， 不是动态的， top用来查看动态的
```
ps -a 显示现行终端机下的所有进程，包括其他用户的进程； 
ps -aux 我一般用这个。。 ， 详细输出
ps -ef  同上面差不多
选项介绍 ： [来源](https://blog.csdn.net/u011641865/article/details/71435510)
• USER：该进程属于那个使用者账号的？
• PID ：该进程的进程ID号。
• %CPU：该进程使用掉的 CPU 资源百分比；
• %MEM：该进程所占用的物理内存百分比；
• VSZ ：该进程使用掉的虚拟内存量 (Kbytes)
• RSS ：该进程占用的固定的内存量 (Kbytes)
• TTY ：该进程是在那个终端机上面运作，若与终端机无关，则显示 ?，另外， tty1-tty6 是本机上面的登入者程序，若为 pts/0 等等的，则表示为由网络连接进主机的程序。
• STAT：该程序目前的状态，主要的状态有：
R ：该程序目前正在运作，或者是可被运作；
S ：该程序目前正在睡眠当中 (可说是 idle 状态啦！)，但可被某些讯号(signal) 唤醒。
T ：该程序目前正在侦测或者是停止了；
Z ：该程序应该已经终止，但是其父程序却无法正常的终止他，造成 zombie (疆尸) 程序
```

#### top 系统状况， 进程状况
> 动态显示系统进程情况， 系统状况  
> top 命令实时显示进程的状态。每5秒钟更新一次。你可以通过PID的数字大小
```
top -u username 显示用户的进程信息
top -p pid pid1 显示每个进程的信息
top -d time 设置刷屏时间， 默认5s

top命令显示会在前面打印总的统计数据和内存占用

```

**2019.3.9**
> 今天整理wc  xargs  tee到常用命令里



---


**2019.3.8**
> 今天整理 sort， uniq， awk, 整理到常用命令里

---
### 文件与目录基本操作

**2019.3.7**
> 继续整理 文件与目录基本操作
#### nl 输出行号 显示文件
> nl 将指定的文件添加行号标注后写到标准输出。如果不指定文件或指定文件为"-" ，程序将从标准输入读取数据。  
> -w 行号占用位数  
> -n   ln  左对齐， rn  右对齐，  n代表空格，用空格填充  rz 右对齐， z代表zero 用0填充

```
nl a  输出a中内容， 并打印行号
nl -b a a.txt 给空行编号
nl -n ln a  行号左对齐
nl -n rn  a   行号右对齐    空格填充
nl -n rz  a   行号右对齐， 填充0
nl  -n rz -w 20 a  行号右对齐， 且占位20位， 且用0填充
``` 
#### more less 显示文件内容
> more 只能向下翻页， less 可以上下翻页， 但是在我电脑上， more是可以向上翻页的。。。  
> more 文件   翻看方式   **空格**和 **f** 向下翻页, **b** 返回上一页  
> less 可以向上查找， 且查找的字符串，会显示出来  
1. more
```
more -5 a 设定每次显示5行
more +5 a 从第5行开始显示
/string 向下搜索string， 从找到的字符串的前两行输出
```

2. less 

```

 ?string 向上搜索string, 会把搜到的字符串标记
 此命令还有更多用处， 我还没有用到， 用到会填上
```

#### head tail 查看文件指定行
> head 查看头几行， tail 查看尾几行
> head -n num 显示前num行，  head -n -num 除后num行， 显示
```
head -n 5 a 显示a的前5行
head -n -5 a 除了后5行， 都显示
head -n 200 a | nl -b a  | tail -n 100 显示第101到200行文件内容

```


---

**2019.3.4**
> 整理 文件与目录基本操作
#### mkdir rmdir  目录操作
1. pwd 打印当前工作目录
2. cd 切换工作目录    cd  -  切换上次工作目录， cd ~ 切换到用户家目录
3. mkdir 创建目录  最常用 -p 自动创建父目录，   -m 指定权限
4. rmdir 删除目录,   不怎么用， 都是用rm -r 递归删除

>此处追加相对路径和绝对路径的概念， 相对路径就是以当前目录为中心,  比如`../` 就是当前目录的上层目录
>`/home/moying12138/xxx`  就是绝对路径， 绝对路径是从根目录出发的， 也就是`/`

#### ls cp rm
> ls  一个刚开始认为很简单的命令， 其实有很多秀秀的选项  
> cp   src   dest     把src复制成dest  
> rm 删除文件| 文件夹
1. ls 
```
ls 显示当前目录下的文件
ls -a 显示全部文件， 包括隐藏文件  .开有的都是隐藏文件
ls -l 显示文件详情
ls -Sl  按照文件大小排序， 默认从大到小
ls -Slr  按照文件大小排序， 从小到大。。。。  对文件排序很有作用， 几百万张图片， 删除最小的几个

```
2. cp
```
cp -i 询问模式   ,  如果不存在直接复制， 不询问
cp -r 拷贝文件夹
cp -s 拷贝为软链接
cp -l  拷贝成硬链接
cp -a  = cp -pdr 连同文件的属性，一起拷贝
cp -p  拷贝文件属性
```
3. rm  
```
rm -i 1.txt    询问模式
rm -r dir     递归删除一个文件夹
rm  -f  1.txt  强制删除，  可以和-r 一起用
``` 




**2019.3.3**
> 今天整理查看系统信息命令
### 系统信息
#### uptime uname 
> uptime 系统运行时长， 平均负载， 当前登录用户数量  
> uname 打印当前系统的信息
1. uptime  平均负载， 运行时长
```
uptime -p 友好的格式输出运行时间
uptime  最后三项分别是1/5/15分钟系统cpu平均负载
```
2. uname   获得电脑系统相关信息
- -a 全部信息
```
uname -a 
uname -m 电脑类型
uname -n 主机名称
uname --help  帮助选项
```
#### w  who  last
> w 获得当前登录用户和正在执行的进程， 第一行输出的uptime, 不太清楚有啥用处。  
> who 显示当前登录系统的用户信息  
> last 最近用户的最近登录信息， 可以读取数据文件, 数据文件cat不能读取，file 文件名   输出data  
1. who
```
who -H   打印对应列的标题。。。
who -q   显示当前登录系统的人数和名称
whoami  打印当前登录的用户名
```
2. last 
> last作用是显示近期用户或终端的登录情况。通过last命令查看该程序的log，管理员可以获知谁曾经或者企图连接系统。执行last命令时，它会读取/var/log目录下名称为wtmp的文件，并把该文件记录的登录系统或终端的用户名单全部显示出来。[来源](https://www.cnblogs.com/diantong/p/8940154.html)
```
last -R 不显示登录系统或终端的主机名或ip
第三列是登录的ip或者内核。如果你看见：0.0 或者什么都没有，这意味着用户用过本地终端链接。除了重启活动，内核版本会显示再状态中；

last -d 将ip转换成主机名

last -F 显示登录的完整时间
```
#### date cal
> date 显示或者设置系统时间  
> cal 显示日历， 用处不多， 每咋用过， 直到就行
1. date
```
date -d "1 day" 输出一天后的时间
data -d "1 day ago" 一天前的   "可以指定日期显示"
date +"%Y_%m_%d %H:%M%S"   %Y是年， %m是月， %d天，指定格式显示
date -s "20190303" 设置日期和时间
```



**2019.3.2**
> 今天整理bash通配符(? * )， 任务管理和，转义字符等
### 命令系统
####  通配符 ? *  [list]
> ?代表匹配单个任意字符                   
> *代表匹配任意多个字符
> [list] 匹配在list集合中任意字符
> [ ! list] 和上面 相反                                 
>[x1 - x2] 匹配x1到x2之间任意单一字符                
>[string1,  string2] 匹配集合中任一字符串
> 通配符配合linux命令使用， 效果很棒

#### 任务管理 基本字符含义
1. &
```
在命令后加上& 代表后台执行。可用fg唤醒
command &
```
2. ; (分号)
```
以分号分隔的命令， 顺序执行
command1 ; command2    #先执行command1 后执行command2， 返回值为最后一个运行结果(command2)
```
3. &&
```
命令以&&链接， 只有当第一个命令执行成功才执行第二条命令
command1 && command2      #command1执行成功才执行command2， 否则不执行command2
```
4.  || 
```
命令以||链接， 第一个命令执行成功, 不执行第二条命令， 否则执行
command1 || command2      #command1执行失败才执行command2， 否则不执行command2
```
5.    ``
```
用``把命令括起来， 代表执行时系统优先执行``中的命令， 然后带入父命令中继续运行， 适用与命令中包含另一个命令
command1 `command2`     #把command2的执行输出， 返回给command1的输入
```
6.  ctrl + z
```
组合键
在shell中执行命令时， 按下组合键代表挂起该命令
```
7. bg, fg
```
将一个在挂起的命令，变成继续执行

通过bg %num 即可将挂起的job的状态由stopped改为running，仍在后台执行；当需要改为在前台执行时，执行命令fg %num即可；
```

9. jobs
```
在linux下执行jobs, 可以看到该shell下的后台执行的和挂起的任务以及编号
```
#### 转义字符  "" '' \  重定向> >> 
>在这也总结下重定向的概念    >  >> 都是重定向，  >> 作用和> 基本相同， 但是>>是往文件里追加， 而> 会覆盖  ，都是作为标准输入， 可以当作可执行文件的输入,  如：  ./a.out  <  file1 
> 需要注意的是， 这里 > 不要在想写回源文件时乱用， 举例    cat a.c | tr "x" "n" | > a.c， 这里就会发现a,c被你搞没了， 因为他会先以覆盖形式打开a.c后执行前面命令， 想写回可以用tee, 就是把> 替换成tee，不做介绍

1. "" 软转义
```
软转义， 其内部只允许出现特定的shell 元字符($, \, `) $用于变量替换， \用于转义单个字符
`用于命令替换
```
2. '' 硬转义              
```
硬转义， 硬引用， 其内部关闭所有shell元字符，通配符，内部不允许出现单引号''
```
3. \ 转义后面的单个字符 
```
去掉后面紧跟着的元字符或通配符的特殊含义
```

### 常用命令
**2019.3.09**
#### wc 统计行数, 字符
```
wc a.txt    输出行数， 字数， 字节数 
wc -l a.txt  统计出现行
wc -w a.txt  字数， 代表由空格或换行分割的字符串，我也刚知道，之前一直不知道是啥。。 为一个字
wc -m a.txt 列出字符数
```


#### tee 双向重定向
>  我经常用来写回源文件， 如 cat a.txt > a.txt 这时a.txt 执行完是空的， 但是cat a.txt | tee a.txt可以写回  
> tee默认打印到标准输出， 指定文件会打印到文件中  
>  tee -a file 追加， 不覆盖， 默认覆盖  
>  网上还有tee ---- 可以重复输出，  我的终端不好用  
```
cat a.txt | tr a b | tee a.txt    把a.txt 文件中的a替换成b， 并保存回去
cat a.txt | tee -a a.txt     追加到文件末尾
cat a.txt | tee a.txt b.txt 写回到多个文件

```
#### xargs 参数代换
> 我用的不多， 但是感觉挺厉害的, 可以配合很多命令使用find,   
> -n num  xargs不是每次把前面的内容都拿过来， -n可以指定 一次取多少个  
> [详细操作](http://www.runoob.com/linux/linux-comm-xargs.html)  
```
find . -type f | xargs rm -rf {}  删除本文件夹下的文件
ls | xargs  -i cp  {} /home/moying  复制本目录下的所有文件到家目录,-i 一行一行的取
cat a.txt | xargs  不换行输出
cat test.txt | xargs -n3 三个一行

```


**2019.3.08**
#### sort 排序
> 将文本中的内容排序， 我都是配合uniq命令使用  
> sort将文件的每一行作为一个单位，相互比较，比较原则是从首字符向后，依次按ASCII码值进行比较，最后将他们按升序输出。

-b  忽略每行前面开始的空格
-d 只处理英文数字和空格， 忽略其他字符
-r 反转排序, 降序
-n 以数值大小排序， 10 > 9   否则  9 > 10
-t  指定间隔符
-k  指定区间   和cut的-d  -f 选项很像
```
sort a.txt  对a.txt 以行为标准排序, 升序
sort -r a.txt   降序
sort -u a.txt   去除重复的行， 进行排序
sort -n a.txt   以数字大小排序,  以字符串方式的话  10 会比2小
sort -t "-" -k 2 a.txt  以-分割， 第二区间升序
```
#### uniq 去重
> 和sort命令配合使用， 统计词频  
> uniq只过滤相邻的重复行， 和sort配合使用  
-d 只输出重复的行
-c 统计每个字符串的频率
-i 不区分大小写

```
cat a.txt | uniq  只能去除相邻的重复行
cat a.txt | sort  | uniq 此处和sort -u a.txt 其实没有区别。。
cat a.txt | sort | uniq -c  统计每个字符串的频率

```

#### awk 世界上最好的语言
> 一个语法和c语言很像， 很适合对文本进行处理  
> 默认对每行进行处理， [很多的语言特性](https://www.cnblogs.com/ginvip/p/6352157.html)  
> 分为三部分， 'BEGIN{begin} {action} END {end}', 对于每行都执行action部分, 其他两部分只执行一次  
> NR代表行数， NF代表字段数量， $NF 代表最后最和一个字段  
> -F 指定分割符   -F ‘[ .]+’ 以多个空格或.分割  
> awk 不可以直接用全局变量， -v 指定
```
awk '{print $0}' /etc/passwd  此处没有begin和end部分，对文件每一行执行action
awk '{if(NR >= 20 && NR <= 50) print $1}' a.txt 输出20到50行

awk -F '[ ,]+' -v a=$a '{print a}' a.txt 
awk '/^(\([0-9]{3}\)|[0-9]{3}-)-[0-9]{3}-[0-9]{4}$/'   awk的正则匹配awk '/正则/{}'
```


---
**2019.2.28**
#### grep  文本检索
> 一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。

-  grep -i "moying" a.txt      忽略大小写查找含有字符串"moying"
-  grep -w  "moying" a.txt    完全匹配
-  -v    反转匹配
-   -e  -E   多模式串检索  -e    要分开    -E 以管道符分割 grep -E "moying | yingmo" a.txt    
-  -c  输出匹配的行数
-  -o 只输出检索到的词， 而不是一行
-  可以加入正则来检索
	
#### tr 字符转换
> tr -[cdst] [第一字符集] [第二字符集]   
>  tr 指令从标准输入设备读取数据，经过字符串转译后，将结果输出到标准输出设备。

- -d 删除第一字符集的字符
- -c  反转替换， 取第一字符集的补集， 来被第二字符集提替换
- -s 连续压缩重复的字符为单个字符， cat a.txt  | tr -s "\n"  删除空行
- -t  默认用第一字符集的长度来替换， -t 消减第一字符集的长度，用第二字符集的长度。
- tr [a-z] [A-Z]   小写转换大写

#### find 文件查找
> 强大的文件搜索命令, 注意查找根目录时最好加上管理员权限， 不然就会  哇  哇  哇
> find path -option     最近知道一个-exec  command {} \;  和  -delete 可以直接删除   -perm  664 权限

- 查找本目录下所有的c程序
```
find . -name "*.c"
```
- 查找本目录下所有文件夹  
```
find . -type d 

-exec  command  {}  \;  对每个检索到的目标执行command 命令
find . -type d -exec ls {} \;   展开所有文件夹中的内容

-print  输出匹配到的目标
find . -type d -print  -exec ls {} \;   展开所有文件夹中文件

-ok   交互式匹配， 没检索到匹配项需要确认
find . -type d -ok ls {} \;   展开所有文件夹中文件
```

- 查找文件以时间来查找
```
find ./ -mtime -2  查找文件更新日时在距现在时刻二天以内的文件
find ./ -mtime +2  查找文件更新日时在距现在时刻二天以上的文件
find ./ -mtime 2   查找文件更新日时在距现在时刻一天以上二天以内的文件
find ./ -newer abc  查找文件更新时间比文件abc的内容更新时间新的文件


```
- 查找文件以大小来查找   
```
find ./ -size -10m 查找10M以内的文件或目录
find ./ -empty 查找空文件或空目录
find ./ -empty -type f -delete   查找空文件并删除
```
---
**2019.3.1**
> 今天测试命令时， 想快速建立一个指定大小的文件， 才发现不会适合的命令

#### dd 磁盘管理(备份) 
> 用于读取、转换并输出数据。dd可从标准输入或文件中读取数据，根据指定的格式来转换数据，再输出到文件、设备或标准输出。 命令很强大 
> 
> if=文件名：输入文件名，缺省为标准输入。即指定源文件。
> of=文件名：输出文件名，缺省为标准输出。即指定目的文件。 
> bs=块大小，  count=块数量，   //最终文件大小= bs * count  
> 有意思的选项 conv=很多参数， 例如： ucase 转大写， lcase转小写   

- 创建指定大小的文件，用0填充
```
sudo dd if=/dev/zero of=./a.txt bs=500k count=6  //创建一个6×500K的文件， /dev/zero提供无数的0。 此处应该是二进制的0， 因为cat a.txt 是空， 可以用od 命令去查看 od a.txt，这里不介绍 
```
- 备份文件， 不能是文件夹
```
sudo dd if=/linux/1_happy.txt of=./1_happy_back.txt   //这里只复制文件内容，不复制文件权限
```

- 销毁磁盘数据
```
dd if=/dev/urandom of=/dev/hda1   // 利用随机的数据填充磁盘，必要的场合可以用来销毁数据。
```
- [更多秀秀的操作](https://www.cnblogs.com/jikexianfeng/p/6103500.html)

#### cat  tac 查看文件内容
> cat 为正向按行读取， tac 为反向按行读取

- 查看文件内容
```
cat a.txt //查看文件
cat -n a.txt //从1开始按行编号
cat -b a.txt  //对空白行不编号
cat -s a.txt  //对多个连续空行， 压缩成一个空行
tac 没有上述选项。。 有什么好的玩法没玩过
```
- 从标准输入写入指定文件
```
cat << END  >> a.txt     从标准输入追加到a.txt    输入END结束， 可替换成别的结束字符
cat << END > a.txt       从标准输入覆盖到a.txt
一个很好的解释
1、cat << EOF，以EOF输入字符为标准输入结束：
2、cat>filename，创建文件，并把标准输入输出到filename文件中，以ctrl+d作为输入结束：
注意：输入时是没有'>'的。
3、cat>filename<<EOF，以EOF作为输入结束，和ctrl+d的作用一样：
```
#### cut 文本切割
> 从文本中提取分割有效的信息， 很好用， 但是因为有时分割符不好确定，可以使用awk
- -d 指定分隔的字符， 默认是TAB        
- -f 指定显示范围
- -b 按照字节选取
- -c 按照字符选取    反正在我电脑上-b  和 -c是一样的， 我的是中文算3个字节编码
```
cat /etc/passwd | cut -b1-3　#取每行的第1-3字字节

cat /etc/passwd | cut -b1-3,5-7,8　#取每行的第1-3,5-7,8的字节(后面的数字会先进行从小到大的排列) 需要事先知道具体字节，很容易出错

cat song.txt |cut -nb 1,2,3  #当 -b 添加 -n 后则不会分割多字节 (我的系统是utf-8，所以需要用三个字节来表示一个汉字)
cat /etc/passwd | cut -c1,3 #适用于中文 

cat /etc/passwd | cut -d : -f 3 #以:分割，取第三段

```
---




[gdb](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/gdb.html)





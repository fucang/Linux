# Linux

数据结构：https://github.com/fucang/fucang.github.io

剑指offer：https://github.com/fucang/-offer

查找命令：http://10740026.blog.51cto.com/10730026/1775291

Linux是多用户、多任务环境的。
Linux权限管理
1、文件访问者的分类(人)  3 个为一组
     a)所有者：u---User  “r-x”
     b)所属组：g---Group  "r-x"
     c)其他用户：o---Others   "---"
2、文件访问权限的种类(事物属性)
     a)基本权限
          i).读（r）read
          ii).写（w）wirte
          iii).执行（x） execute
          iv).“-”表示不具有该项权限
3 个为一组eg：“r-x”,"r-x","---"

root拥有无限的权力
/etc/passwd    记录用户信息    
/etc/shadow   记录个人密码    
/etc/group      记录组名

当出现“Permission deny”---->权限错误

以root身份登陆Linux(执行“su”命令，输入密码即可)，执行"ls -al":

“ls”表示显示文件的文件名和文件属性，
参数“-al”则表示列出所有的文件详细的权限与属性（包含隐藏文件（文件名的第一个字符为“.”的文件））
第一个字符代表这个文件是“目录、文件或链接文件”等
[d]--->目录          [l]--->链接文件              [-]--->文件         
[b]--->设备文件里面的可供存储的接口设备
[c]--->设备文件里面的串行端口设备

第一列代表这个文件的类型与权限
第二列表示有多少文件名连接到此节点
第三列表示这个文件（或目录）的“所有者账号”
第四列表示这个文件所属的用户组
第五列为这个文件的大小，默认单位为B
第六列为这个文件的创建日期或最近修改日期（今年的年份不显示）
显示完整的时间格式可以使用ls的参数，即“ls -l --full-time”


第七列表示该文件名

使用“man ls”或“info ls”可以看ls的基本用法


关于系统服务的文件通常只有root才能读写或者是执行，例如/etc/shadow,通常访问权限为[-rw-------]


如何修改文件属性与权限？？
chgrp：改变文件的所属用户组         
chown：改变文件的所有者         
chmod：改变文件的权限

chgrp：改变文件的所属用户组（要改变的用户组名必须在/etc/group中才行，否则会报错）


错误更改：
chown：改变文件的所有者（用户必须是已经存在于系统中的账号，也就是在etc/passwd这个文件中有记录的用户）


主要用于复制文件： “cp 源文件 目标文件”
chmod：改变文件的权限
权限的设置有两种方法，分别可以使用数字或字符来进行权限修改



当一个文件具有w权限时，可以具有写入、编辑、新增、修改文件的内容的权限，但并不具有删除该文件本身的权限。
对于目录而言r、w、x的意义：
     r：表示具有读取目录结构列表的权限，可以查询该目录下的文件名数据
     w：表示具有更改该目录结构列表的权限，即具有以下权限：

     x：表示用户能否进入该目录成为工作目录的用途（目录不能被执行）
更换目录的命令是“cd”.





文件种类：
      1、普通文件
        2、纯文本文件
     3、二进制文件
     4、数据格式文件

Linux目录配置标准：FHS
FHS是依据文件系统使用的频繁与否与是否允许用户随意改动，而将目录定义为四种交互作用的形态。


Linux的三层目录：

	* /（root，根目录）：与开机系统有关
	* /user：与软件安装/执行有关
	* /var：与系统运作过程有关

根目录与开机、还原、系统修复有关。
不可与根目录分开的目录：

	* /etc：配置文件
	* /bin：重要执行文件
	* /dev：执行文件所需的函数库与内核作序的模块
	* /sbin：重要的系统执行文件


/usr里面放置的数据属于可分享的与不可变动的。
/var目录主要针对常态性变动文件，包括缓存（cache）、登陆文件（log file）以及某些软件运行所产生的文件

目录树的主要特性：

	* 目录树的起始点为根目录（/，root）；
	* 每个目录不只能使用本地端的文件系统，也可以使用网络上的文件系统，eg：可以利用NFS服务器挂载某特定目录等
	* 每一个文件在此目录树中的文件名（包括完整路径）都是独一无二的。

使用“ls -l /”查看根目录下的数据：

绝对路径：由根目录（/）开始写起的文件名或目录名称
相对路径：相对于目前路径的文件名的写法，开头不是“/”就属于相对路径的写法
回到上一层：“../”

	* "."：代表当前目录，也可以使用“./”来表示
	* ".."：代表上一层目录，也可以使用“../”来表示


总结：

	* Linux的每个文件中，依据权限分为用户、用户组与其他人三种身份（User，Group，Others）
	* 用户组最有用的功能之一就是在团队开发资源的时候，且每个账号都可以有多个用户组的支持
	* 利用ls -l显示的文件属性中，第一个字段是文件的权限，共10位，第一位是文件类型，接下来三个为一组共三组，

       为用户、用户组、其他人的权限，权限有r、w、x三种

	* 更改文件的用户组chgrp，修改文件的所有者chown，修改文件的权限chmod
	* 权限：r（可读），w（可写），x（可执行）
	* 要开放目录给人浏览时，应该至少给予r（查看目录包含的文件名）及x（查看目录里面的具体内容）的权限，

     但w权限不可随意给（w可修改可删除）

	* FHS制定的四种目录特色：shareable（可分享）、unshareable（不可分享）

                                            static（不变的）、variable（可变的）

	* FHS定义的三层主目录：/、/var、/user
	* 有五种目录不可与根目录放在不同的分区：/etc、/bin、/lib、/dev、/sbin


比较特殊的目录：

	* “.”代表此层目录
	* “..”代表上一层目录
	* “-”代表前一个工作目录
	* “~”代表“目前用户身份”所在的主文件夹
	* “~account”代表account这个用户的主文件夹（account是个账号名称）

所有的目录都会存在两个目录，分别是“.”，“..”

常见的处理目录的命令：

	* cd：切换目录
	* pwd：显示当前目录
	* mkdir：新建一个新的目录
	* rmdir：删除一个空的目录

mkdir（新建新目录） mkdir [-mp]  目录名称

在默认情况下，所需要的目录得一层一层建立才行，不过如果加上“-p”这个参数，系统会自动建立上层目录
（尽量少用“-p”参数）
可以利用“-m”来强制给予一个新的目录相关的权限

rmdir（删除“空”目录）
rmdir [-p] 目录名称 仅能删除“空目录”
参数“-p”会连同上层的“空的”目录也一并删除
目录需要一层一层的删，而且被删除的目录里面必定不能存在其他的目录或文件
如果要将目录下所有的东习全删除那就需使用“rm -r 目录名称”

执行文件路径的变量：$PATH   每个目录中间用冒号（：）来隔开


	* 不同身份用户默认的PATH不同，默认能够随意执行的命令也不同
	* PATH是可以修改的，所以一般用户还是可以通过修改PATH来执行某些位于/sbin或/user/sbin下的命令来查询
	* 使用绝对路径或相对路径直接指定某个命令的文件名来执行，会比查询PATH来得正确
	* 本目录（.）最好不要放到PATH中

查看文件与目录：ls

-a：全部文件，连同隐藏文件
-d：仅列出目录本身，而不是列出目录内的文件数据
-l：列出长数据串，包含文件的属性与权限等数据
当只执行ls命令时，默认显示的只有非隐藏文件的文件名，以文件名进行排序及文件名代表的颜色显示
在Linux系统中，这些与权限、属性有关的数据放在i-node中
ll <==> ls -l

复制、删除、移动：cp,rm,mv
对于移动目录与文件，也可以直接拿重命名（rename）来操作。

cp(复制文件或目录)：
-a：相当于-pdr的意思
-i：若目标文件（destination）已经存在时，在覆盖时会先询问操作的运行
-r：递归持续复制，用于目录的复制行为
-p：连同文件的属性一并复制，而非使用默认属性（备份中常用）
cp命令不同的身份者执行会有不同的效果产生，尤其是-a，-p


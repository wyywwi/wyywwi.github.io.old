---
layout: default
title: "linux"
permalink: /notes/linux/
---

# Basic_Linux_in_kali

---

[toc]

---

## 常用指令部分

### 文件管理

#### 1.目录操作 (pwd/ls/cd)

1. pwd  -- print working directory
   As it's name implies, it can reply where you are.

2. ls  -- list   **列出目录**

   ```bash
   ls -l #--------------list in long form
   ls -a #--------------list all
   ls -s #--------------list in short form
   ll #-----------------a short term of ls -l
   l #------------------a short term of ls or ls -s
   ```

   l 和 ls 的区别：

   [![vmLkE6.png](https://s1.ax1x.com/2022/08/05/vmLkE6.png)](https://imgtu.com/i/vmLkE6)

   [![vmLCuR.png](https://s1.ax1x.com/2022/08/05/vmLCuR.png)](https://imgtu.com/i/vmLCuR)

3. cd -- change directory  **更改工作目录**

   ```bash
   cd ~           #go back to users main directory
   cd /           #go back to root directory
   cd -           #返回之前所在目录
   cd ..          #go back to father directory
   cd ../..       #go back to grandfather directory
   cd !$          #把上个命令的参数作为 cd 参数使用
   ```

#### 2. 创建文件/文件夹 (touch/mkdir)

1. **touch   创建文件**

   ```bash
   touch newFile           #create a file named "newFile"
   touch file1 file2 ...   #create mutiple files named "file1", "file2" ...
   ```

   

   [![vmqOEV.png](https://s1.ax1x.com/2022/08/05/vmqOEV.png)](https://imgtu.com/i/vmqOEV)

   **Like this image shows, a file has Access time (a-time), Modify time (m-time) and Change time (c-time). When you touch a file that has been created, you change it's a-,m- and c-time.**

   ```bash
   touch -a oldFile    #change oldFile's a-time and c-time to now
   touch -m oldFile    #change oldFile's m-time and c-time to now
   ```

   **Other command options will be shown later.**

2. **mkdir 创建文件夹**

   ```bash
   mkdir [-p] dirname
   mkdir testdir               #make a directory named testdir
   mkdir testdir2/newdir       #if testdir2 did not exist, it will return error
   mkdir -p testdir2/newdir    #if testdir2 did not exist, then create it too
   ```

#### 3. 显示文件/文件夹信息(file/stat)

1. **stat   文件/文件夹详细信息**

   ```bash
   stat oldFile      #list oldFile's info
   stat -f oldFile   #list oldFile's file system info
   stat [-f] oldDir  #just like oldFile
   ```

   

   [![vmqXNT.png](https://s1.ax1x.com/2022/08/05/vmqXNT.png)](https://imgtu.com/i/vmqXNT)

2. **file    辨识文件类型**

   [![vmqxCF.png](https://s1.ax1x.com/2022/08/05/vmqxCF.png)](https://imgtu.com/i/vmqxCF)

#### 4. 删除文件/文件夹(rm)

1. **rm   remove  删除**

   **\*为通配符**

   对于文件夹，采用举例说明：

   [![vmLpv9.png](https://s1.ax1x.com/2022/08/05/vmLpv9.png)](https://imgtu.com/i/vmLpv9)

   [![vmLSgJ.png](https://s1.ax1x.com/2022/08/05/vmLSgJ.png)](https://imgtu.com/i/vmLSgJ)

   **只有递归操作，才能删除文件夹**

#### 5. 复制/剪切/重命名文件/文件夹(mv/cp)

1. **mv move 移动/重命名文件/文件夹**

   ```bash
   mv file1 file2              #将file1重命名为file2
   mv file1 file2 ... dir1     #将file1、file2、......移动至目录dir1下
                               #若其中一个file不存在，则会给出报错，但是存在的file会被顺利移动
   mv file1 file2 dir1         #若dir1不存在则会报错；若仅有file1则为重命名
   mv dir1 dir2                #可以正常操作；mv没有递归（-r）选项
   ```

   [![vmLPD1.png](https://s1.ax1x.com/2022/08/05/vmLPD1.png)](https://imgtu.com/i/vmLPD1)

2. **cp copy 复制文件**

   ```bash
   cp file1 dir1/file2      #将file1复制并粘贴到dir1中，同时重命名为file2
   cp file1 file2 ... dir1  #将file1 file2 ... 复制粘贴到dir1中， **不提供改名功能**
   cp -r dir1 dir2 ... dirn #同上，不能改名，dirn须已存在
   cp -r dir1 dir2/dir3     #将dir1复制到dir2下并改名为dir3，**不加-r则会报错**
   ```

```
##### 6. 展示文件内容(cat/head/tail)

1. **cat concatenate 连接（显示文件内容）**

   ```bash
   cat file1            #显示file1的内容
   cat -n file1         #显示file1的内容，同时附加上行号
   cat file1 file2 ...  #依次显示内容
```

2. **head 显示文件头部**

   head -n 显示头部n行

   tail -n     仿此

#### 6. 查找文件(which/whereis/locate)

1. which    在环境变量$PATH设置的目录里查找符合条件的文件

   ​                适用于查找系统文件夹/系统命令    不适用于查找用户文件/文件夹

   [![vmLAUK.png](https://s1.ax1x.com/2022/08/05/vmLAUK.png)](https://imgtu.com/i/vmLAUK)

2. whereis 

   在特定目录中查找符合条件的文件。这些文件应属于原始代码、二进制文件，或是帮助文件。

   只能用于查找二进制文件（-b）、源代码文件（-s）和man手册页（-m）。

   [![vmLE4O.png](https://s1.ax1x.com/2022/08/05/vmLE4O.png)](https://imgtu.com/i/vmLE4O)

   （查询用户文件kali：未找到   查询service：找到二进制可执行文件和man说明文件）

3. locate

   在保存文档和目录名称的数据库内，查找合乎范本样式条件的文档或目录。

   因使用数据库，故与updatedb配合食用。

   updatedb一般每天自动执行一次。

   ```bash
   -b     --basename      #仅匹配路径名的基本名称
   -c     --count         #仅输出查找到的数量
   -i      --ignore-case  #忽略大小写
   ```

   [![vmLe8e.png](https://s1.ax1x.com/2022/08/05/vmLe8e.png)](https://imgtu.com/i/vmLe8e)

   ​                                                                                               （passwd为数众多，只截取一部分)

   [![vmLnvd.png](https://s1.ax1x.com/2022/08/05/vmLnvd.png)](https://imgtu.com/i/vmLnvd)

   


#### 7. find    --最强大的查找

```bash
find  path  -option  [-exec command {} \;]
```

- option可以叠加；
- 常用option：(i)name, type, size, empty, (i)path, a/c/mtime/min

> -exec command：command 为其他指令，-exec后面可再接额外的指令来处理搜寻到的结果。
>
> { }代表的是「由 find 找到的内容」，找到的结果会被放置到 { } 位置中;
> -exec一直到 ; 是关键字，代表找到额外动作的开始（-exec）到结束（\），在这中间的就是找到指令内的额外动作
>
> 因为「;」在bash的环境下是有特殊意义的，因此利用反斜线来跳脱。

1. **options**

- name:  与通配符*配合食用， 须加单引号， iname表示忽略大小写。
- type：常见type如下：

| 类型参数列表 | 表示字母 |
| ------------ | -------- |
| 普通文件     | f        |
| 符号连接     | l        |
| 普通目录     | d        |
| 字符设备     | c        |
| 块设备       | b        |
| 套接字       | s        |

[![vmLKKA.png](https://s1.ax1x.com/2022/08/05/vmLKKA.png)](https://imgtu.com/i/vmLKKA)

- size：单位主要有 b 块（512字节）， c 字节， w 字（2字节)， k 千字节， M 兆字节， G 吉字节

  [![vmLMDI.png](https://s1.ax1x.com/2022/08/05/vmLMDI.png)](https://imgtu.com/i/vmLMDI)

- empty：空文件

  [![vmL1VP.png](https://s1.ax1x.com/2022/08/05/vmL1VP.png)](https://imgtu.com/i/vmL1VP)

- path：所在路径

  [![vmLQbt.png](https://s1.ax1x.com/2022/08/05/vmLQbt.png)](https://imgtu.com/i/vmLQbt)

- time/min：略

2. **exec**

   --exec rm -rf {} \;         删除搜索出的文件

   --exec ls -l {} \;             详细列出搜索出的文件

   **其他依此类推**

#### 8. 查询命令(man/whatis）

1. man  command

   查询命令，弹出一页展示该命令的详细用法等等。

2. whatis  command

   查询命令，返回一句话简短介绍。

#### 9. 打包/解包/压缩/解压缩(tar/gzip/zip)

###### 9.1. tar使用

1. tar   文件打包

   常用参数：

   ```
   -c 建立新的归档文件；  
   -v 处理过程中输出相关信息；  
   -f 对普通文件操作；
   -z 使用gzip进行打包
   -j 使用bzip2进行打包
   ```

   tar -cvf new1.tar  a b c     将文件a, b, c压缩为一个文件new1.tar

   tar -czvf new2.tar.gz a b c        将文件a, b, c压缩为一个文件new1.tar.gz

   **(以上两个操作里.tar和.tar.gz都不是必要选项，只是为了方便辨认文件类型而添加)**

2. tar 文件解包

   ```
   -x 或--ext\fract或--get：从备份文件中还原文件；  
   -v 处理过程中输出相关信息；  
   -f  对普通文件操作；  
   -C <目的目录> 切换到指定的目录；  
   ```

   tar -xzvf new2.tar.gz

   tar -xvf new1.tar -C ./Newdir

3. tar 文件查看

   ```
   -t 列出tar文件
   ```

   tar -tf new2.tar.gz        列出new2中的文件（简短）

   tar -tvf new2.tar.gz      列出new2中的文件（详细）

   tar -tzvf new2.tar.gz    同上（若new2为tar文件则会报错）

###### 9.2. bzip2/gzip/zip

1. bzip2

   用于创建和管理（包括解压缩）`.bz2`格式的压缩包。

   ```bash
   -z或——compress：强制执行压缩；  
   -d或——decompress：执行解压缩；  
   -f或-force：bzip2在压缩或解压缩时，若输出文件与现有文件同名，预设不会覆盖现有文件。若要覆盖。请使用此参数；  
   -v或——verbose：压缩或解压缩文件时，显示详细的信息；    
   -k或——keep：在解压缩后，预设会删除原来的压缩文件。若要保留压缩文件，请使用此参数；   
   ```

   eg:

   ```bash
   bzip2 new.tar         #压缩
   bzip2 new.tar.bz2     #解压
   bzip2 -d new.tar.bz2  #解压
   tar -xjvf new.tar.bz2 #解压同时解包
   ```

2. gzip

   用于创建和管理（包括解压缩）`.gz`格式的压缩包.

   ```bash
   -d或--decompress或----uncompress：解开压缩文件；  
   -f或——force：强行压缩/解开压缩文件。不理会文件名称或硬连接是否存在以及该文件是否为符号连接；  
   -l或——list：列出压缩文件的相关信息；  
   -r或——recursive：递归处理，将指定目录下的所有文件及子目录一并处理；  
   -v或——verbose：显示指令执行过程；    
   -q或-quiet：不显示警告信息；    
   ```

   eg:

   ```bash
   gzip new.tar         #压缩
   gzip new.tar.gz      #解压
   gzip -d new.tar.gz   #解压
   tar -xzvf new.tar.gz #解压同时解包
   ```

3. zip

   `zip`命令对文件进行打包操作。`zip`是个使用广泛的压缩程序，文件经它压缩后会另外产生具有`.zip`扩展名的压缩文件。

   具体命令如下：

   ```bash
   zip　命令参数　指定生成的压缩文件名　要被压缩的文件/目录列表
   ```

   常用命令参数如下：

   ```bash
   -d：从压缩文件内删除指定的文件；  
   -q：不显示指令执行过程；  
   -r：递归处理，将指定目录下的所有文件和子目录一并处理；  
   -v：显示指令执行过程或显示版本信息；  
   -u：更换较新的文件到压缩文件内；  
   -x<范本样式>：压缩时排除符合条件的文件； 
   ```

     eg.

   ```bash
   zip -r newDir.zip newDir  
   ```

4. unzip

   `unzip`命令用于解压缩由`zip`命令压缩的`.zip`压缩包。

   具体命令如下：

   ```
   unzip　命令参数　指定要解压的文件
   ```

   常用参数如下:

   ```bash
   -q：执行时不显示任何信息；  
   -n：解压缩时不要覆盖原有的文件；  
   -d<目录>：指定文件解压缩后所要存储的目录；  
   ```

   

### 用户管理

#### 1. 我是谁？（whoami）

Who am I, 无需赘述。

#### 2. 给我特权！（sudo）

sudo  -V   -h   -l   -v   -k   -b   -p   -u   -i   command

command 以root的身份执行command

-V 显示版本编号

-h 显示版本编号，指令使用帮助说明

-l  显示使用者所拥有的权限

[![vmLY8g.png](https://s1.ax1x.com/2022/08/05/vmLY8g.png)](https://imgtu.com/i/vmLY8g)

-k 下次sudo时强制询问密码

-u user command   以某user的身份执行command

-i (--login)  切换使用账号，与-u配合食用，如果没有添加-u user则默认为切换成root

[![vmLJPS.png](https://s1.ax1x.com/2022/08/05/vmLJPS.png)](https://imgtu.com/i/vmLJPS)



#### 3. 添加用户/用户组（useradd/adduser）

useradd和adduser是同一命令。

useradd -m testUser                        添加用户testUser，同时创建其登录目录。

useradd -c  text testUser                添加用户testUser，同时加上备注文字。备注文字会保存在passwd的备注栏位中。

useradd -e exbiredate testUser    指定用户有效期限（过expiredate之后用户无效）。

useradd -g group testUser              指定用户所属群组。

useradd -r testUser                            将用户设置为系统用户。

useradd -b directory testUser       指定用户的登入目录为directory

#### 4. 切换用户（su）

**switch user  切换用户**

su [-c command] [-/-l/--login] user

su -c command user     以user的身份执行command然后返回自身身份

su user        切换到user身份，但是不改变工作目录

su - user    相当于重新登陆地切换到user身份

[![vmL858.png](https://s1.ax1x.com/2022/08/05/vmL858.png)](https://imgtu.com/i/vmL858)

​                                                                          （su user 与 su - user 对比，前者不改变工作目录，后者改变）

#### 5. 用户/用户密码管理（userdel/passwd）

- 删除用户（userdel）

  userdel [-r] username    -r用于将用户文件夹和相关文件一并删除。

- 修改密码（passwd）

  passwd [-k] [-l] [-u [-f]] [-d] [-S] [username]

  **不添加参数则为修改密码**

  -g      修改群组密码

  -S      显示账号密码信息

  -d      删除密码

  -l       停止账号使用

  -u      启用被停止使用的账户

  [![vmLNvj.png](https://s1.ax1x.com/2022/08/05/vmLNvj.png)](https://imgtu.com/i/vmLNvj)

  （-S并不会直接展示密码，只会展示账户信息；有无密码（P/NP），账户设立时间等等）


### 其他



#### 1. pwd 打印工作目录

（没啥用的功能）

#### 2. service

服务状态（status），开启服务（start），关闭服务（stop），重启服务（restart），所有服务状态（--status-all）

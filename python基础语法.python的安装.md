###1、安装python环境
     linux下：
     一 下载：
          第一种可以直接采用apt-get install的方式  
          第二种下载ubuntu下的shell终端，通过wget命令下载python源码包。
            sudo wget http://www.python.org.......tgz等等具体版本号
            [sudo] password for zhm:
          将其下载到/opt的目录下
     二 解压：
          然后对python进行解压：
          进入到opt目录下查看安装包是否存在 用ls命令
          然后进行解压
            sudo tar zxvf python....tgz
       
     三 编译与安装：因为在linux上配置和编译的过程已经自动化，所以输入几条命令就可以了。
          首先：我们通过执行./configure开始编译，我们可以传一些参数来进行脚本的配置
          之后：我们可以运行make,如下代码所示：
            opt/python....$sudo。/configure --prefix=/usr/local/python..
          通过添加--prefix用于指定python的安装路径于/usr/local/python..配置完成后，我们就可以执行make操作了。
            opt/Python-..$make
          make的编译时间比较长，大概5-6分钟，完成之后我们可以进行安排操作：
            /opt/Python...$ sudo make install
       
          接下来我们可以查看安装后的python目录：
            /opt/Pyhton..$ ls /usr/local/python../
          因为这是自己动手将python安装于/usr/local/python..目录下，所以此时的$PATH环境无法找到此目录下的python解释器。
          为此可以增加一个软链接，代码如下：
            /opt/Python_..$ sudo ln -s /usr/local/python../bin/python  /bin/python..
            
            /opt/Python-..$ python
            
          通过ln -s/usr/loacl/pyton../bin/python /bin/python..命令可以在/bin路径下创建一软链接文件python..,当访问
          此链接文件，就可以间接的访问/usr/local/python..下的程序了。这种方式与windows下的快捷方式类似。
          
          接下来我们可以通过运行python命令的交互模式以查看刚刚安装得python版本情况：
            /opt/Python-..$ python..
          或者通过执行python..  -v来查看
          至此python安装完成。
          
     四 Setuptools的安装过程：
        1、setuptools的下载
           setuptools源码的下载与python类似，通过wget来下载，指令如下：
              /opt$ sudo wget http://pypi.python.org/packages/source/s/setuptools/setuptools-...tar.gz
              
              
              之后:
              /opt$ ls
         2、解压：
              /opt$ sudo tar zxvf setuptools-...tar.gz
              
         3、setuptools的编译及安装：
            编译如下，用python..版本的程序来执行setup.py脚本，此脚本带参数build，执行编译过程。
               /opt/setuptools-..$sudo python.. setup.py build,执行编译过程。
               
            如果编译完成：就可以进行安装了，指令如下：
               /opt/setuptools..$ sudo python.. setup.py install
            如果不出问题就是成功了，但是如果安装未成功，显示如下错误：
                z = zipfile.ZipFile(zip_filename,mode,compression=compression)
              File "/usr/local/python../lib/python../zipfile.py", line681, in __init__
                 "Comoression requires the(missing) zlib module"
            RuntimeError:Compression requires the(missing) zlib module
            zhem@master:/opt/seyuptools-..$
            
            根据错误提示，主要错误在于"Compression requires the(missing) zlib module",错误的原因在于缺少zlib模块，
            但是最根本的原因在于安装python..版本之前未进行依赖检查，我们可以通过：
                sudo apt-get build-dep python
            进行检查。所以要解决zlib module缺少的问题，必须在安装python..版本之前先安装zlib1g-dev软件包，安装完成后再重
            新安装python，然后再运行：
                sudo python.. setup.py install
            此时才可以正常解决问题。
            
            安装成功之后，我们也可以看到setuptools的路径在/usr/local/python/python..目录下
            我们可以查看一下：
                /opt/setuptools-..$ ls /usr/.ocal/python../bin
                
            我们可以看到在刚安装的python目录下存在一些easy_install程序，这就是setuptools工具的一些程序，方便我们后期安装
            第三方模块使用，再次我们继续做个软链接：
                /opt/setuptools-..$ sudo ln -s /usr/bin/python../bin/easy_install  /bin/easy_install
                
                /opt/setuptools-..$ easy_install
            这样，当我们直接输入easy_install就可以直接访问此程序了。
         
         
         4、用setuptools自动安装django及numpy
         
            安装django命令如下：
            sudo easy_install django
            但有时会发生"unknow url: httpd"错误
            解决方法是在安装python之前需要先安装libssl-dev
            命令如下：
            sudo apt-get install libssl-dev
            安装numppy命令如下：
            sudo easy_install numpy
            就可以自动安装了
            这种方式和sudo apt-get install类似
            
            
            
            
         
              

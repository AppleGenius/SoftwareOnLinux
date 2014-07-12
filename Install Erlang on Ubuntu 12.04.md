### 准备工作： ###
 - 配置Java环境（详细见我的Evernote）
 - 升级系统
    apt-get install update    
    apt-get install upgrade
 - 安装Erlang依赖包
     apt-get install g++ build-essential libncurses5-dev libgl1-mesa-dev libglu1-mesa-dev

### 下载Erlang源代码包 ###
[下载地址：otp_src_R16B02.tar.gz][2]
### 编译Erlang源代码 ###
解包后执行以下命令，其中--enable-smp-support选项用于打开多处理器支持，--enable-kernel-poll选项用于打开epoll支持

      ./configure --prefix=/usr/local/erlang --enable-smp-support --enable-threads --enable-kernel-poll --enable-hi
配置结束会有如下结果

    *********************************************************************
    **********************  APPLICATIONS DISABLED  **********************
    *********************************************************************
    crypto        : No usable OpenSSL found
    odbc          : ODBC library - link check failed
    ssh            : No usable OpenSSL found
    ssl            : No usable OpenSSL found

    *********************************************************************
    *********************************************************************
    **********************  APPLICATIONS INFORMATION  *******************
    *********************************************************************
    wx            : wxWidgets not found, wx will NOT be usable

解决方法：
    
     前四个问题的解决方案：安装以下两个包即可
     - apt-get install libssl-dev
     - apt-get install unixodbc unixodbc-dev 
     
     解决wxWidgets的问题：需要手动安装编译wxWidgets源码
        安装依赖包：
        安装GTK apt-get install libgtk2.0-dev 
        配置OpenGL：
          ln -s /usr/lib/x86_64-linux-gnu/libGL.so /usr/lib/libGL.so
          ln -s /usr/lib/x86_64-linux-gnu/libGLU.so /usr/lib/libGLUso
        下载源码：[wxWidgets-2.8.12.tar.gz][3]
        解压源码后进入文件包，然后配置wxWidgets
         ./configure --enable-unicode --with-opengl
        编译wxWidgets：
         make && make install
         cd wxWidgets-2.8.12/contrib/src/stc
         make && make install
         echo /usr/local/lib > /etc/ld.so.conf.d/wx.conf
         ldconfig

#### 重新编译Erlang ####
     ./configure --prefix=/usr/local/erlang --enable-smp-support --enable-threads --enable-kernel-poll --enable-hipe
     
     make && make install
        
        
######## 本文基于[Ubuntu 12.04 LTS 64位下编译安装Erlang R16B02][1]指导在Ubuntu上成功安装Erlang ########
     

    
    
    


  [1]: http://www.linuxidc.com/Linux/2013-10/91105.htm
  [2]: http://www.erlang.org/download/otp_src_R16B02.tar.gz
  [3]: http://colocrossing.dl.sourceforge.net/project/wxwindows/2.8.12/wxWidgets-2.8.12.tar.gz
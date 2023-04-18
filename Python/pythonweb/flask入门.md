### 从零创建一个flask项目

1. #### 初始化
   所有的flask程序都必须创建一个程序实例，这个程序实例就是Flask类的对象。客户端把请求发送给Web服务器，服务器再把请求发送给Flask程序实例，然后由程序实例处理请求。创建方法，随便新建一个python文件，写入以下代码：

   ~~~python
   from flask import Flask
   app = Flask(__name__)
   ~~~

   此处的\_\_name\_\_是一个全局变量，它的值是代码所处的模块或包的名字，flask用这个参数决定程序的根目录，一遍稍后能找到相对于程序根目录的资源文件位置。

2. #### 路由和视图函数
   程序实例通过路由来处理请求——路由就是URL和处理请求的函数的映射——处理请求的函数就叫做视图函数。
   Flask定义路由最简便的方式，是使用程序实例提供的app.route装饰器。
   程序根地址处理程序如下：

   ~~~python
   @app.route('/'):
       def index():
           return '<h1>Hello world!</h1>'
   ~~~

   地址包含可变部分的路由：

   ~~~python
   @app.route('/user/<name>'):
       def user(name):
           return '<h1>Hello,%s!</h1>' %name
   ~~~

   尖括号中的内容是动态部分，任何能匹配静态部分的URL都会映射到这个视图函数，调用视图函数是，Flask会将动态部分作为参数传入函数。

   注意：路由中的动态部分默认类型是字符串，不过也可以使用别的类型如：/user/只会匹配动态片段id为整数的url

3. #### 启动服务器
   Flask应用自带Web开发服务器，通过flask run命令启动。这个命令在FLASK_APP环境变量指定的Python脚本中寻找应用实例。
   使用编程直接启动，调用app.run()方法

   ~~~python
   if __name__ == '__main__':
       app.run(debug=True) #debug参数为True，表示启用调试
   ~~~

4. #### 部署项目到服务器

   - 安装所需依赖：

     ~~~shell
      # 安装开发工具组
      yum -y groupinstall "Development tools"
      # 安装一些漏网之鱼
      yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel libffi-devel 
      # 下载python3，版本根据自己需求来，装到/usr/local/python3下，装错目录用mv命令剪切
      wget https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tar.xz
      # 解压并安装
      tar -xvJf Python-3.7.10.tar.xz  
       cd Python-3.7.10
       ./configure --prefix=/usr/local/python3  
       make && make install
       # 创建python3软链接，防止与系统自带的python2冲突，这样就可以通过python使用python2，python3使用python3.
       sudo ln -s /usr/local/python3 /usr/bin/python3
       # 配置pip的软连接来使用pip
       ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
       # 安装虚拟环境
       yum install python-virtualenv
       # 建立python3独立环境
       virtualenv -p /usr/local/python3/bin/python3.7 /py3env
       # 如果出现ModuleNotFoundError: No module named '_ctypes'的报错，运行下面的代码
       yum install libffi-devel 
       # 并重新运行下面的代码安装python3
       cd Python-3.7.10
       ./configure --prefix=/usr/local/python3  
       make && make install
       # 进入python3独立环境，如果上面报错，需重新建立python3独立环境
       source /py3env/bin/activate
       # 进入项目目录，在此之前需把项目文件上传，运行代码安装依赖
       pip3 install -r requirements.txt 
       # 安装gunicorn
       pip3 install gunicorn 
       # 运行项目，1 表示一个线程，注意端口是否开放，:app前面是项目名
       gunicorn -w 1 -b 0.0.0.0:8080 spider:app
       # 安装nginx
       yum -y install nginx 
       # 先关闭apache，并设置关闭开机启动
       systemctl stop httpd.service 
       systemctl disable httpd.service
       # 配置nginx，让其反向代理我们要访问的ip，找到/etc/nginx下的nginx.conf文件，找到server配置项，修改如下代码，原来有的配置不变
       server{
       	listen 80;
       	location / {
       		proxy_pass http://127.0.0.1:4500;# 这里是要代理的地址
       		proxy_set_header Host $host;
       		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       	}
       }
       # 重新启动gunicorn即可
       # 注意，以后重新进入服务器重启gunicorn，需要重新进入虚拟环境
     ~~~
     
   - gunicorn 停止/重启服务
     获取进程树
     ~~~shell
     pstree -ap | grep gunicorn
     ~~~
   
     找到主进程id，使用命令重启该进程
     ~~~shell
     kill -HUP 14256
     ~~~
   
     或直接杀死该进程
     ~~~shell
     kill -9 14256
     ~~~
   
   - 不挂断运行（command是要执行的命令）
     ~~~shell
     nohup command &
     ~~~
   
     


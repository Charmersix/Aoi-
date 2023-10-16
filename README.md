## AoiAWD环境搭建

官方其实提提供了构建流程, 但是其搭建过程中的坑网上的处理方式还是很少的, 网上大部分教程也已经很老了, 这里结合本人遇见的问题大体写一下.

首先更新一波

```shell
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential
```

下载项目

```shell
apt install git
git clone https://github.com.cnpmjs.org/DasSecurity-HatLab/AoiAWD.git
```

安装`inotifywait`

```shell
mkdir inotifywait  
cd inotifywait     
wget  https://github.com/inotify-tools/inotify-tools/archive/refs/tags/4.23.9.0.tar.gz 
tar zxf 4.23.9.0.tar.gz  
cd inotify-tools-4.23.9.0/
```

接下来配置构建

```shell
./autogen.sh
./configure
./configure --prefix=/usr/local
make
sudo make install
```

安装`mongdb`需要的依赖

```
sudo apt install mongodb-server
sudo apt-get install php-dev php-pear
sudo pecl install mongodb 
```

安装好后可顺便启动一下

```
sudo service mongodb start
sudo service mongodb status
```

![image-20231016205938006](https://blog-1308152021.cos.ap-beijing.myqcloud.com/image-20231016205938006.png)

接着我们去php的配置文件php.ini进行修改

```shell
sudo vim /etc/php/5.6/cli/php.ini
```

![image-20231016210200190](https://blog-1308152021.cos.ap-beijing.myqcloud.com/image-20231016210200190.png)

![image-20231016210124119](https://blog-1308152021.cos.ap-beijing.myqcloud.com/image-20231016210124119.png)

然后再把这两个开关改成Off，记住要把前面的分号去掉，不然会被注释掉

构建Fronted项目

```shell
apt install npm      
cd AoiAWD  			
cd Frontend
npm install       
npm run build
```

npm与node的版本问题，可能会出现版本互不支持的情况，

如果有npm或node，先查看一下版本

```shell
node -v
npm -v
```

版本对应情况:https://nodejs.org/zh-cn/download/releases

接下来就可以按照官方提供的文档进行搭建了

https://github.com/DasSecurity-HatLab/AoiAWD/blob/master/BUILD.md

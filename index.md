### 一、下载启动 MongoDB
Leanote 依赖 MongoDB 作为数据存储，开始安装 MongoDB：

下载 MongoDB

进入 /home 目录，并下载 MongoDB：

    cd /home
    wget http://labs-1253675457.cosgz.myqcloud.com/mongodb-linux-x86_64-3.0.1.tgz

解压缩源码包：

    tar -xzvf mongodb-linux-x86_64-3.0.1.tgz

创建用于存储的文件夹目录

    mkdir -p /data/db

配置 MongoDB 的环境变量：

编辑 /etc/profile，在文件末尾追加以下配置：

示例代码：/etc/profile

    export PATH=$PATH:/home/mongodb-linux-x86_64-3.0.1/bin

并执行以下命令，使环境变量生效。

    source /etc/profile

启动 MongoDB（启动大概需要 3 ~ 5 分钟）：

    #本处localhost如需远程访问，需要改为0.0.0.0
    
    mongod --bind_ip localhost --port 27017 --dbpath /data/db/ --logpath=/var/log/mongod.log --fork

### 二、安装 Leanote
Leanote 是一款 Linux 下开源的软件，开始安装 Leanote：

下载 Leanote

先进入 /home 目录

    cd /home
    wget http://labs-1253675457.cosgz.myqcloud.com/leanote-linux-amd64-v2.4.bin.tar.gz

解开压缩包：

    tar -zxvf leanote-linux-amd64-v2.4.bin.tar.gz

编辑 Leanote 配置文件

编辑文件 /home/leanote/conf/app.conf，在文件中找到 app.secret= 项，并修改为如下内容：

    app.secret=ysl1970

初始化数据库

导入初始化数据：

    mongorestore -h localhost -d leanote --dir /home/leanote/mongodb_backup/leanote_install_data/

启动 Leanote 服务

    nohup /bin/bash /home/leanote/bin/run.sh >> /var/log/leanote.log 2>&1 &

### 三、准备域名和证书
如果不需要通过域名访问 Leanote 云笔记本则到此就结束了，通过访问 http:// 地址>:9000 就可以了使用自己的笔记本，初始化账户： admin，初始化密码： abc123

域名注册

可以在腾讯云或阿里云上进行购买

域名解析

域名购买完成后, 需要将域名解析到云服务器上

域名设置解析后需要过一段时间才会生效，通过 ping 命令检查域名是否生效

如果 ping 命令返回的信息中含有你设置的解析的 IP 地址，说明解析成功。

访问 Leanote 云笔记本

通过 ip 访问笔记本
通过访问 http://你的域名:9000 就可以了使用自己的笔记本。

初始化账户： admin
初始化密码： abc123





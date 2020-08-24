## dnmp docker环境安装步骤

### 安装虚拟机
1. 虚拟机可以使用VirtualBox或其他，这里推荐使用VirtualBox,下载文件地址：`https://mirrors.tuna.tsinghua.edu.cn/help/virtualbox/`
2. 在虚拟机上安装linux系统。系统最好使用ubuntu，因为测试环境和线上也是使用ubuntu，具体按照步骤可以参考网上。这里附上清华大学的镜像下载地址：`https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/16.04/`
3. docker环境的安装需要ubuntu系统在16.04版本以上，如果不是，要先进行升级。 查看ubuntu的版本号 `cat /etc/issue`,升级ubuntu系统可参考最下面教程。

### 安装docker
1. 参考文档 https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/  
2. 检查docker是否成功 `sudo docker -v`
3. 将当前用户加入到docker用户组 `sudo gpasswd -a $USER docker && newgrp docker`
4. `docker -v` 检查当前用户是否有权限

### 安装docker-compose
1. 参考文档 https://docs.docker.com/compose/install/  
    注：这个过程会比较久，在下载docker-compose文件的时候可以使用daocloud的镜像源
    `sudo sh -c "curl -L https://get.daocloud.io/docker/compose/releases/download/1.26.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose"`
2. 检查docker-composes是否安装成功 `docker-compose -v`

### 挂载磁盘
1. 首先在windows上将项目的目录文件夹设置成共享文件夹
2. 在虚拟机上新建项目目录 `sudo mkdir -p /opt/htdocs2/`
3. 挂载目录 `sudo mount -t cifs //XXXX/windows本地的项目目录 /opt/htdocs2 -o username=你的windows用户名,password=你的windows密码,rw,uid=0,gid=0,dir_mode=0777,file_mode=0777`
4. cd /opt/htdocs2/ ls查看是否挂载成功

### 构建镜像
1. 修改.env文件（一般不需要修改）
2. 常用的docker和docker-compose命令
    ```
    运行容器: docker-compose -f docker-compose.yml up(首次使用)
    后台运行容器: docker-compose -f docker-compose.yml up -d
    查看当前运行的容器：docker ps -a
    进入php容器: docker exec -it php56 sh
    进入nginx容器：docker exec -it nginx sh
    ```
3. 可以根据自己的需要将一些常用的命令写在shell文件中，快速进行操作

### 升级ubuntu系统（参考）
1. 因为国外源存在网络耗时问题，so使用国内清华大学的ubuntu镜像。打开`https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/` 按照提示进行换源操作。
2. `sudo apt-get update`
3. `sudo apt-get dist-upgrade`
4. `sudo do-release-upgrade` 按照提示系统进行操作
5. `sudo reboot`,检查是否升级成功 `cat /etc/issue`
6. 升级成功后，根据当前的系统版本可进行换源操作，因为不同的版本有不同的镜像源地址。参考步骤1
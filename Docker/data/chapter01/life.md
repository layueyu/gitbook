# Docker容器生命周期管理

## 一、Docker run 命令

### 说明

- 创建一个新的容器并运行一个命令

### 语法

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

- OPTIONS说明：
  - **-a stdin** ： 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；
  - **-d:** 后台运行容器，并返回容器ID；
  - **-i:** 以交互模式运行容器，通常与 -t 同时使用；
  - **-p:** 端口映射，格式为：主机(宿主)端口:容器端口 
  - **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
  - **--name="nginx-lb":** 为容器指定一个名称；
  - **--dns 8.8.8.8:** 指定容器使用的DNS服务器，默认和宿主一致；
  - **--dns-search example.com:** 指定容器DNS搜索域名，默认和宿主一致；
  - **-h "mars":** 指定容器的hostname；
  - **-e username="ritchie":** 设置环境变量；
  - **--env-file=[]:** 从指定文件读入环境变量；
  - **--cpuset="0-2" or --cpuset="0,1,2":** 绑定容器到指定CPU运行；
  - **-m**设置容器使用内存最大值；
  - **--net="bridge":** 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；
  - **--link=[]:** 添加链接到另一个容器；
  - **--expose=[]:** 开放一个端口或一组端口；
  - **--restart：** 设置重启方式
    - no -  容器退出时，不重启容器
    - on-failure - 只有在非0状态退出时才从新启动容器
    - always - 无论退出状态是如何，都重启容器

### 实例

1. 使用docker镜像nginx:latest以后台模式启动一个容器,并将容器命名为mynginx

   ```bash
   docker run --name mynginx -d nginx:latest
   ```

2. 使用镜像nginx:latest以后台模式启动一个容器,并将容器的80端口映射到主机随机端口。

   ```bash
   docker run -P -d nginx:latest
   ```

3. 使用镜像 nginx:latest，以后台模式启动一个容器,将容器的 80 端口映射到主机的 80 端口,主机的目录 /data 映射到容器的 /data。

   ```bash
   docker run -p 80:80 -v /data:/data -d nginx:latest
   ```

4. 绑定容器的 8080 端口，并将其映射到本地主机 127.0.0.1 的 80 端口上。

   ```bash
   docker run -p 127.0.0.1:80:8080/tcp ubuntu bash
   ```

5. 使用镜像nginx:latest以交互模式启动一个容器,在容器内执行/bin/bash命令。

   ```bash
   docker run -it nginx:latest /bin/bash
   ```

## 二、Docker start/stop/restart 命令

### 说明

- **docker start** :启动一个或多个已经被停止的容器

- **docker stop** :停止一个运行中的容器

- **docker restart** :重启容器

### 语法

```bash
docker start [OPTIONS] CONTAINER [CONTAINER...]
docker stop [OPTIONS] CONTAINER [CONTAINER...]
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

#### 实例

1. 启动已被停止的容器myrunoob

    ```bash
    docker start myrunoob
    ```

2. 停止运行中的容器myrunoob

    ```bash
    docker stop myrunoob
    ```

3. 重启容器myrunoob

    ```bash
    docker restart myrunoob
    ```

## 三、 Docker kill 命令

### 说明

- **docker kill** :杀掉一个运行中的容器。

### 语法

```bash
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

- OPTIONS说明：
  - **-s**向容器发送一个信号

### 实例

- 杀掉运行中的容器mynginx

    ```bash
    docker kill -s KILL mynginx
    ```

## 四、Docker pause/unpause 命令

### 说明

- **docker pause** :暂停容器中所有的进程。

- **docker unpause** :恢复容器中所有的进程。

### 语法

```bash
docker pause [OPTIONS] CONTAINER [CONTAINER...]
docker unpause [OPTIONS] CONTAINER [CONTAINER...]
```

### 实例

1. 暂停数据库容器db01提供服务。

    ```bash
    docker pause db01
    ```

2. 恢复数据库容器db01提供服务。

    ```bash
    docker unpause db01
    ```

## 五、 Docker create 命令

### 说明

- **docker create ：**创建一个新的容器但不启动它

### 语法

```bash
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### 实例

1. 使用docker镜像nginx:latest创建一个容器,并将容器命名为myrunoob

    ```bash
    docker create  --name myrunoob  nginx:latest  
    ```

## 六、 Docker exec 命令

### 说明

- **docker exec ：**在运行的容器中执行命令

### 语法

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

- OPTIONS说明：
  - **-d**分离模式: 在后台运行
  - **-i**即使没有附加也保持STDIN 打开
  - **-t**分配一个伪终端

### 实例

1. 在容器mynginx中以交互模式执行容器内/root/runoob.sh脚本

    ```bash
    docker exec -it mynginx /bin/sh /root/runoob.sh
    ```

2. 在容器mynginx中开启一个交互模式的终端

    ```bash
    docker exec -i -t  mynginx /bin/bash
    ```
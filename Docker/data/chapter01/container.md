# 容器操作

## 一、Docker ps 命令

### 说明

- **docker ps** 列出容器

### 语法

```bash
docker ps [OPTIONS]
```

- OPTIONS说明：
  **-a**显示所有的容器，包括未运行的。
  **-f**根据条件过滤显示的内容。
  **--format**指定返回值的模板文件。
  **-l**显示最近创建的容器。
  **-n**列出最近创建的n个容器。
  **--no-trunc**不截断输出。
  **-q**静默模式，只显示容器编号。
  **-s**显示总的文件大小。

### 实例

1. 列出所有在运行的容器信息。

    ```bash
    docker ps
    ```

2. 列出最近创建的5个容器信息。

    ```bash
    docker ps -n 5
    ```

3. 列出所有创建的容器ID。

    ```bash
    docker ps -a -q
    ```

## 二、Docker inspect 命令

### 说明

- **docker inspect** 获取容器/镜像的元数据。

### 语法

```bash
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

- OPTIONS说明：
  - **-f**指定返回值的模板文件。
  - **-s**显示总的文件大小。
  - **--type**为指定类型返回JSON。

### 实例

1. 获取镜像mysql:5.6的元信息。

    ```bash
    docker inspect mysql:5.6
    ```

2. 获取正在运行的容器mymysql的 IP。
    ```bash
    docker inspect --format=`{{a}}{{b}}{{end}}` mymysql
    ```
    注：
    - 占位符a: range .NetworkSettings.Networks
    - 占位符b: .IPAddress
    - 将上述相应替换

## 三、Docker top 命令

### 说明

- **docker top**查看容器中运行的进程信息，支持 ps 命令参数。

### 语法

```bash
docker top [OPTIONS] CONTAINER [ps OPTIONS]
```

- 容器运行时不一定有/bin/bash终端来交互执行top命令，而且容器还不一定有top命令，可以使用docker top来实现查看container中正在运行的进程。

### 实例

1. 查看容器mymysql的进程信息。

    ```bash
    docker top mymysql
    ```

2. 查看所有运行容器的进程信息。

    ```bash
    for i in  `docker ps |grep Up|awk '{print $1}'`;do echo \ &&docker top $i; done
    ```

## 四、 Docker attach 命令

### 说明

- **docker attach**连接到正在运行中的容器。

### 语法

```bash
docker attach [OPTIONS] CONTAINER
```

- 要attach上去的容器必须正在运行，可以同时连接上同一个container来共享屏幕（与screen命令的attach类似）。

- 官方文档中说attach后可以通过CTRL-C来detach，但实际上经过我的测试，如果container当前在运行bash，CTRL-C自然是当前行的输入，没有退出；如果container当前正在前台运行进程，如输出nginx的access.log日志，CTRL-C不仅会导致退出容器，而且还stop了。这不是我们想要的，detach的意思按理应该是脱离容器终端，但容器依然运行。好在attach是可以带上--sig-proxy=false来确保CTRL-D或CTRL-C不会关闭容器。

### 实例

1. 容器mynginx将访问日志指到标准输出，连接到容器查看访问信息。

    ```bash
    docker attach --sig-proxy=false mynginx
    ```

## 五、Docker events 命令

### 说明

- **docker events** 从服务器获取实时事件

### 语法

```bash
docker events [OPTIONS]
```

- OPTIONS说明：
  - **-f ：**根据条件过滤事件；
  - **--since ：**从指定的时间戳后显示所有事件;
  - **--until ：**流水时间显示到指定的时间为止；

### 实例

1. 显示docker 2016年7月1日后的所有事件。

    ```bash
    docker events  --since="1467302400"
    ```

## 六、Docker logs 命令

### 说明

- **docker logs** 获取容器的日志

### 语法

```bash
docker logs [OPTIONS] CONTAINER
```

- OPTIONS说明：
  - **-f** 跟踪日志输出
  - **--since**显示某个开始时间的所有日志
  - **-t** 显示时间戳
  - **--tail**仅列出最新N条容器日志

### 实例

1. 跟踪查看容器mynginx的日志输出。

    ```bash
    docker logs -f mynginx
    ```

2. 查看容器mynginx从2016年7月1日后的最新10条日志。

    ```bash
    docker logs --since="2016-07-01" --tail=10 mynginx
    ```

## 七、 Docker wait 命令

### 说明

- **docker wait** 阻塞运行直到容器停止，然后打印出它的退出代码。

### 语法

```bash
docker wait [OPTIONS] CONTAINER [CONTAINER...]
```

### 实例

```bash
docker wait CONTAINER
```

## 八、Docker export 命令

# 说明

- **docker export**将文件系统作为一个tar归档文件导出到STDOUT。

### 语法

```bash
docker export [OPTIONS] CONTAINER
```

- OPTIONS说明：
  - **-o**将输入内容写到文件。

### 实例

1. 将id为a404c6c174a2的容器按日期保存为tar文件。

    ```bash
    runoob@runoob:~$ docker export -o mysql-`date +%Y%m%d`.tar a404c6c174a2
    ```

## 九、Docker port 命令

### 说明

- **docker port**列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。

### 语法

```bash
docker port [OPTIONS] CONTAINER [PRIVATE_PORT[/PROTO]]
```

### 实例

1. 查看容器mynginx的端口映射情况。

    ```bash
    docker port mymysql
    ```

## 十、 容器rootfs命令

### Docker commit 命令

#### 说明

- **docker commit**从容器创建一个新的镜像。

#### 语法

```bash
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

- OPTIONS说明：
  - **-a**提交的镜像作者；
  - **-c**使用Dockerfile指令来创建镜像；
  - **-m**提交时的说明文字；
  - **-p**在commit时，将容器暂停。

#### 实例

1. 将容器a404c6c174a2  保存为新的镜像,并添加提交人信息和说明信息。

    ```bash
    runoob@runoob:~$ docker commit -a "runoob.com" -m "my apache" a404c6c174a2  mymysql:v1
    ```

### Docker cp 命令

#### 说明

- **docker cp**用于容器与主机之间的数据拷贝。

#### 语法

```bash
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
```

- OPTIONS说明：
  - **-L**保持源目标中的链接

#### 实例

1. 将主机/www/runoob目录拷贝到容器96f7f14e99ab的/www目录下。

    ```bash
    docker cp /www/runoob 96f7f14e99ab:/www/
    ```

2. 将主机/www/runoob目录拷贝到容器96f7f14e99ab中，目录重命名为www。

    ```bash
    docker cp /www/runoob 96f7f14e99ab:/www
    ```

3. 将容器96f7f14e99ab的/www目录拷贝到主机的/tmp目录中。

    ```bash
    docker cp  96f7f14e99ab:/www /tmp/
    ```

### Docker diff 命令

#### 说明

- **docker diff** 检查容器里文件结构的更改。

#### 语法

```bash
docker diff [OPTIONS] CONTAINER
```

#### 实例

1. 查看容器mymysql的文件结构更改。

    ```bash
    docker diff mymysql
    ```
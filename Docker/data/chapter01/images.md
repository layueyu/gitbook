# 镜像仓库

## Docker login/logout 命令

- **docker login** 登陆到一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub

- **docker logout** 登出一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub

### 语法

```bash
docker login [OPTIONS] [SERVER]
docker logout [OPTIONS] [SERVER]
```

- OPTIONS说明：
  - **-u**登陆的用户名
  - **-p**登陆的密码

#### 实例

登陆到Docker Hub

```bash
docker login -u 用户名 -p 密码
```

登出Docker Hub

```bash
docker logout
```

## Docker pull 命令

- **docker pull** 从镜像仓库中拉取或者更新指定镜像

### 语法

```bash
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

- OPTIONS说明：
  - **-a**拉取所有 tagged 镜像
  - **--disable-content-trust**忽略镜像的校验,默认开启

### 实例

1. 从Docker Hub下载java最新版镜像。

    ```bash
    docker pull java
    ```

2. 从Docker Hub下载REPOSITORY为java的所有镜像。

    ```bash
    docker pull -a java
    ```

## Docker push 命令

- **docker push** 将本地的镜像上传到镜像仓库,要先登陆到镜像仓库

### 语法

```bash
docker push [OPTIONS] NAME[:TAG]
```

- OPTIONS说明：
  - **--disable-content-trust**忽略镜像的校验,默认开启

### 实例

1. 上传本地镜像myapache:v1到镜像仓库中。

    ```bash
    docker push myapache:v1
    ```

## Docker search 命令

- **docker search** 从Docker Hub查找镜像

### 语法

```bash
docker search [OPTIONS] TERM
```

- OPTIONS说明：
  - **--automated**只列出 automated build类型的镜像；
  - **--no-trunc**显示完整的镜像描述；
  - **-s**列出收藏数不小于指定值的镜像。

### 实例

1. 从Docker Hub查找所有镜像名包含java，并且收藏数大于10的镜像

    ```bash
    runoob@runoob:~$ docker search -s 10 java
    ```

# 本地镜像管理

## Docker images 命令

- **docker images** 列出本地镜像。

### 语法

```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

- OPTIONS说明：
  - **-a**列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层）；
  - **--digests**显示镜像的摘要信息；
  - **-f**显示满足条件的镜像；
  - **--format**指定返回值的模板文件；
  - **--no-trunc**显示完整的镜像信息；
  - **-q**只显示镜像ID。

### 实例

1. 查看本地镜像列表。

    ```bash
    runoob@runoob:~$ docker images
    ```

2. 列出本地镜像中REPOSITORY为ubuntu的镜像列表。

    ```bash
    docker images  ubuntu
    ```

## Docker rmi 命令

- **docker rmi** 删除本地一个或多少镜像。

### 语法

```bash
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

- OPTIONS说明：
  - **-f**强制删除；

  - **--no-prune**不移除该镜像的过程镜像，默认移除；

### 实例

1. 强制删除本地镜像runoob/ubuntu:v4。

    ```bash
    root@runoob:~# docker rmi -f runoob/ubuntu:v4
    ```

## Docker tag 命令

- **docker tag** 标记本地镜像，将其归入某一仓库。

### 语法

```bash
docker tag [OPTIONS] IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]NAME[:TAG]
```

### 实例

1. 将镜像ubuntu:15.10标记为 runoob/ubuntu:v3 镜像。

    ```bash
    docker tag ubuntu:15.10 runoob/ubuntu:v3
    ```

## Docker build 命令

- **docker build**  命令用于使用 Dockerfile 创建镜像。

### 语法

```bash
docker build [OPTIONS] PATH | URL | -
```

- OPTIONS说明：
  - **--build-arg=[]**设置镜像创建时的变量；
  - **--cpu-shares**设置 cpu 使用权重；
  - **--cpu-period**限制 CPU CFS周期；
  - **--cpu-quota**限制 CPU CFS配额；
  - **--cpuset-cpus**指定使用的CPU id；
  - **--cpuset-mems**指定使用的内存 id；
  - **--disable-content-trust**忽略校验，默认开启；
  - **-f**指定要使用的Dockerfile路径；
  - **--force-rm**设置镜像过程中删除中间容器；
  - **--isolation**使用容器隔离技术；
  - **--label=[]**设置镜像使用的元数据；
  - **-m**设置内存最大值；
  - **--memory-swap**设置Swap的最大值为内存+swap，"-1"表示不限swap；
  - **--no-cache**创建镜像的过程不使用缓存；
  - **--pull**尝试去更新镜像的新版本；
  - **--quiet, -q**安静模式，成功后只输出镜像 ID；
  - **--rm**设置镜像成功后删除中间容器；
  - **--shm-size**设置/dev/shm的大小，默认值是64M；
  - **--ulimit**Ulimit配置。
  - **--tag, -t:** 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。
  - **--network:** 默认 default。在构建期间设置RUN指令的网络模式

### 实例

1. 使用当前目录的 Dockerfile 创建镜像，标签为 runoob/ubuntu:v1。

    ```bash
    docker build -t runoob/ubuntu:v1 ./
    ```

2. 使用URL **github.com/creack/docker-firefox** 的 Dockerfile 创建镜像

    ```bash
    docker build github.com/creack/docker-firefox
    ```

3. 也可以通过 -f Dockerfile 文件的位置：

    ```bash
    $ docker build -f /path/to/a/Dockerfile .
    ```

4. 在 Docker 守护进程执行 Dockerfile 中的指令前，首先会对 Dockerfile 进行语法检查，有语法错误时会返回：

    ```bash
    docker build -t test/myapp .
    ```

## Docker history 命令

- **docker history** 查看指定镜像的创建历史。

### 语法

```bash
docker history [OPTIONS] IMAGE
```

- OPTIONS说明：
  - **-H**以可读的格式打印镜像大小和日期，默认为true；
  - **--no-trunc**显示完整的提交记录；
  - **-q**仅列出提交记录ID。

### 实例

1. 查看本地镜像runoob/ubuntu:v3的创建历史。

    ```bash
    docker history runoob/ubuntu:v3
    ```

## Docker save 命令

- **docker save** 将指定镜像保存成 tar 归档文件。

## 语法

```bash
docker save [OPTIONS] IMAGE [IMAGE...]
```

- OPTIONS说明：
  - **-o**输出到的文件。

### 实例

1. 将镜像runoob/ubuntu:v3 生成my_ubuntu_v3.tar文档

    ```bash
    runoob@runoob:~$ docker save -o my_ubuntu_v3.tar runoob/ubuntu:v3
    ```

## Docker import 命令

- **docker import** 从归档文件中创建镜像。

### 语法

```bash
docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]
```

- OPTIONS说明：
  - **-c**应用docker 指令创建镜像；
  - **-m**提交时的说明文字；

### 实例

1. 从镜像归档文件my_ubuntu_v3.tar创建镜像，命名为runoob/ubuntu:v4

    ```bash
    docker import  my_ubuntu_v3.tar runoob/ubuntu:v4  
    ```

## Docker info 命令

- docker info 显示 Docker 系统信息，包括镜像和容器数。。

### 语法

```bash
docker info [OPTIONS]
```

### 实例

1. 查看docker系统信息。

    ```bash
    docker info
    ```

## Docker version 命令

- docker version显示 Docker 版本信息。

### 语法

```bash
docker version [OPTIONS]
```

- OPTIONS说明：
  - **-f**指定返回值的模板文件。

### 实例

1. 显示 Docker 版本信息。

    ```bash
    docker version
    ```
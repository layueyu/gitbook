# web 管理工具

## 一 、Portainer

### 1. 简介

- Portainer是Docker的图形化管理工具，提供状态显示面板、应用模板快速部署、容器镜像网络数据卷的基本操作（包括上传下载镜像，创建容器等操作）、事件日志显示、容器控制台操作、Swarm集群和服务等集中管理和操作、登录用户管理和控制等功能。功能十分全面，基本能满足中小型单位对容器管理的全部需求

### 2. 下载Portainer镜像

  ```bash
  docker pull portainer/portainer
  ```

### 3. 运行Portaniner

  ```bash
  docker run -d -p 19000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name prtainer portainer/portainer
  ```

### 4. 参考文档

- [搭建Portainer可视化界面](https://blog.csdn.net/u011781521/article/details/80469804)
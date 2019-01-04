# 创建一本书

## 初始化一本书

GitBook 可以设置一个样板书：

```shell
gitbook init
```

## 构建

使用构建命令在项目目录下生成一个_book目录，里面的内容为静态站点的资源文件

```shell
gitbook build
```

### Debugging

使用选项 --log=debug和--debug获取更好的错误信息

```shell
gitbook build ./ --log=debug --debug
```

## 启动服务

启动一个web服务，通过 [http://localhost:4000](http://localhost:4000) 可以预览书籍

```shell
gitbook serve
```
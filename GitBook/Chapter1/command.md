# GitBook 命令

**列出 gitbook 所有的命令:**

```bash
gitbook help
```

**输出 gitbook-cli 的帮助信息:**

```bash
gitbook --help
```

**生成静态网页:**

```bash
gitbook build
```

**生成静态网页并运行服务器:**

```bash
gitbook serve
```

**生成时指定gitbook的版本, 本地没有会先下载:**

```bash
gitbook build --gitbook=2.0.1
```

**列出本地所有的gitbook版本:**

```bash
gitbook ls
```

**列出远程可用的gitbook版本:**

```bash
gitbook ls-remote
```

**安装对应的gitbook版本:**

```bash
gitbook fetch 标签/版本号
```

**更新到gitbook的最新版本:**

```bash
gitbook update
```

**卸载对应的gitbook版本:**

```bash
gitbook uninstall 2.0.1
```

**指定log的级别:**

```bash
gitbook build --log=debug
```

**输出错误信息:**

```bash
gitbook builid --debug
```
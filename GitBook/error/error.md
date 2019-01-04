# 常见错误处理

## 一、gitbook serve命令找不到fontsettings.js

- 用gitbook想生成HTML，执行了gitbook serve时报错：Error: ENOENT: no such file or directory, stat 'C:UserscjfGitBookLibraryImportprepare_bookgitbookgitbook-plugin-fontsettingsfontsettings.js'

- 解决办法：

  ```shell
  cd ~/.gitbook/versions/版本/lib/output/website/
  vim copyPluginAssets.js
  删除112行
  ```
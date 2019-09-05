# OSX开发

## Boost库在OSX下配置

[Mac OS下安装Boost库并在Xcode下测试运行](https://blog.csdn.net/waterbinbin/article/details/62438417)

Header Search Paths
/usr/local/Cellar/boost/1.70.0/include

## Xcode配置

### [解决每次运行Xcode都需要输入密码问题](https://blog.csdn.net/qq_32385309/article/details/51809624)

```shell
DevToolsSecurity --status
Developer mode is currently disabled.
DevToolsSecurity --enable
Developer mode is now enabled.
DevToolsSecurity --disable
```

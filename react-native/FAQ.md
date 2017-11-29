# ReactNative常见问题解决

- [ReactNative常见问题解决](#reactnative%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3)
    - [1. 安装问题](#1-%E5%AE%89%E8%A3%85%E9%97%AE%E9%A2%98)

## 1. 安装问题

1. grade-2.4-all.zip下载慢

    到 [此处](http://www.androiddevtools.cn/) 下载grade-2.4-all.zip,然后放到

    ```shell
    C:\Users\[用户名]\.gradle\wrapper\dists\gradle-2.14.1-all\8bnwg5hd3w55iofp58khbp6yv
    ```

2. ADB不能正确启动

    发现Android不能发现genymotion模拟器，同时使用adb shell命令发现错误如下。

    ```shell
    $ adb shell
    adb server version (32) doesn't match this client (35); killing...
    error: could not install *smartsocket* listener: Address already in use
    ADB server didn't ACK
    * failed to start daemon *
    error: cannot connect to daemon
    ```

    原来是genymotion中的adb命令被占用冲突了，直接打开genymotion的Setting，切换到第四
    个标签页(ADB)，选择Use custom Android Sdk tools,然后选择我们开发使用的Sdk路径即可。

3. 